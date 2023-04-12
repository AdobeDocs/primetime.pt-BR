---
title: Transmitindo informações do cliente (dispositivo, conexão e aplicativo)
description: Transmitindo informações do cliente (dispositivo, conexão e aplicativo)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 0%

---


# Transmitindo informações do cliente (dispositivo, conexão e aplicativo) {#pass-client-info}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.


## Escopo {#pass-client-info-scope}

Este documento agrega detalhes e livros de cookies para transmitir informações do cliente (dispositivo, conexão e aplicativo) de um aplicativo do programador para APIs REST ou SDKs de autenticação da Adobe Primetime.

Os benefícios de fornecer informações sobre os clientes são:

* A capacidade de habilitar corretamente a Autenticação de Base Doméstica (HBA) no caso de alguns tipos de dispositivos e MVPDs que podem suportar HBAs.
* A capacidade de aplicar TTLs adequadamente no caso de alguns tipos de dispositivo (por exemplo, configurar TTLs mais longos para sessões de autenticação em dispositivos conectados à TV).
* A capacidade de agregar adequadamente métricas de negócios em relatórios detalhados por tipos de dispositivo usando o ESM (Entitlement Service Monitoring).
* Desbloqueia a capacidade de aplicar corretamente várias regras de negócios (por exemplo, degradação) em tipos específicos de dispositivos.

## Visão geral {#pass-client-info-overview}

As informações do cliente consistem em:

* **Dispositivo** informações sobre os atributos de hardware e software do dispositivo de onde o usuário está tentando consumir o conteúdo do Programador.
* **Conexão** informações sobre os atributos de conexão do dispositivo de onde o usuário está se conectando aos serviços de Autenticação da Adobe Primetime e/ou aos serviços do Programador (por exemplo, implementações de servidor para servidor).
* **Aplicativo** informações sobre o aplicativo registrado de onde o usuário está tentando consumir o conteúdo do Programador.

As informações do cliente são um objeto JSON criado com chaves apresentadas na tabela a seguir.

>[!NOTE]
>
>O seguinte **teclas** são **mandatory** a ser enviado no objeto JSON de informações do cliente: **modelo**, **osName**.
>
>As seguintes chaves têm **restrito** valores: `primaryHardwareType`, `osName`, `osFamily`, `browserName`, `browserVendor`, `connectionSecure`.

|  | Chave | Restrito | Descrição | Valores possíveis |
|---|---|---|---|---|
|  | primaryHardwareType | # Sim | O tipo de hardware principal do dispositivo. | # Os valores são restritos: Camera DataCollectionTerminal Desktop EmbeddedNetworkModule e eReader GamesConsole GeolocationTracker Óculos MediaPlayer MobilePhone PaymentTerminal Plug-inModem SetTopBox TV Tablet WirelessHotspot Wristwatch Desconhecido |
| #mandatory | modelo | Não | O nome do modelo do dispositivo. | Por exemplo, iPhone, SM-G930V, AppleTV, etc. |
|  | version | Não | A versão do dispositivo. | Por exemplo, 2.0.1, etc. |
|  | fabricante | Não | A empresa/organização de fabricação do dispositivo. | Por exemplo, Samsung, LG, ZTE, Huawei, Motorola, Apple, etc. |
|  | vendor | Não | A empresa/organização que vende o dispositivo. | Por exemplo, Apple, Samsung, LG, Google, etc. |
| #mandatory | osName | # Sim | O nome do sistema operacional (SO) do dispositivo. | # Os valores são restritos: Android Chrome OS Linux Mac OS X OpenBSD Roku OS Windows iOS tvOS webOS |
|  | osFamily | Sim | O nome do grupo do sistema operacional (SO) do dispositivo. | # Os valores são restritos: Android BSD Linux PlayStation OS Roku OS Symbian Tizen Windows iOS macOS tvOS webOS |
|  | osVendor | Não | O fornecedor do sistema operacional (SO) do dispositivo. | Amazon Apple Google LG Microsoft Mozilla Nintendo Nokia Roku Samsung Tizen Projeto Sony |
|  | osVersion | Não | A versão do sistema operacional (SO) do dispositivo. | Por exemplo, 10.2, 9.0.1, etc. |
|  | browserName | # Sim | O nome do navegador. | # Os valores são restritos: Navegador Android Chrome Edge Firefox Internet Explorer Opera Safari SeaMonkey Navegador Symbian |
|  | browserVendor | # Sim | A empresa/organização do navegador. | # Os valores são restritos: Amazon Apple Google Microsoft Motorola Mozilla Netscape Nintendo Nokia Samsung Sony Ericsson |
|  | browserVersion | Não | A versão do navegador do dispositivo. | por exemplo, 60.0.3112 |
|  | userAgent | Não | O agente do usuário do dispositivo. | por exemplo, Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/602.4.8 (KHTML, como Gecko) Versão/10.0.3 Safari/602.4.8 |
|  | displayWidth | Não | A largura física da tela do dispositivo. |  |
|  | displayHeight | Não | A altura física da tela do dispositivo. |  |
|  | displayPpi | Não | A densidade física de pixels da tela do dispositivo. | por exemplo, 294 |
|  | diagonalScreenSize | Não | A dimensão diagonal da tela física do dispositivo, em polegadas. | Por exemplo, 5.5, 10.1 |
|  | connectionIp | Não | O IP do dispositivo usado para enviar solicitações HTTP. | por exemplo, 8.8.4.4 |
|  | connectionPort | Não | A porta do dispositivo usada para enviar solicitações HTTP. | por exemplo, 53124 |
|  | connectionType | Não | O tipo de conexão de rede. | Por exemplo, WiFi, LAN, 3G, 4G, 5G |
|  | connectionSecure | # Sim | O status de segurança da conexão de rede. | # Os valores são restritos: true - no caso de uma rede segura false - no caso de um hot spot público |
|  | applicationId | Não | O identificador exclusivo do aplicativo. | por exemplo, CNN |

## Referências de API {#api-ref}

Esta seção apresenta a API responsável por lidar com informações do cliente ao usar APIs REST ou SDKs de autenticação do Adobe Primetime.

### REST API {#rest-api}

O suporte aos serviços de autenticação da Adobe Primetime recebe as informações do cliente das seguintes maneiras:

* Como um **cabeçalho: &quot;X-Device-Info&quot;**
* Como um **parâmetro de consulta: &quot;device_info&quot;**
* Como um **parâmetro de publicação: &quot;device_info&quot;**

>[!IMPORTANT]
>
>Nos três cenários, a carga do cabeçalho ou parâmetro deve ser **Codificado em base64 e codificado em URL**.

**SDK**

#### SDK do JavaScript {#js-sdk}

O SDK JavaScript do AccessEnabler cria, por padrão, um objeto JSON de informações do cliente, que será passado para os serviços de autenticação da Adobe Primetime, a menos que substituído.

O SDK do JavaScript do AccessEnabler é compatível com **substituição somente** a chave &quot;applicationId&quot; do objeto JSON de informações do cliente por meio do [setRequestor](/help/authentication/javascript-sdk-api-reference.md#setrequestor(inRequestorID,endpoints,options))&#39;s *applicationId* parâmetro de opções.

>[!CAUTION]
>
>O `applicationId` o valor do parâmetro deve ser um valor de string de texto simples.
>Caso o aplicativo Programador decida passar o applicationId, o restante das chaves de informações do cliente ainda será calculado pelo SDK JavaScript do AccessEnabler.

#### SDK do iOS/tvOS {#ios-tvos-sdk}

O SDK do AccessEnabler iOS/tvOS cria por padrão um objeto JSON de informações do cliente, que será passado para os serviços de autenticação da Adobe Primetime, a menos que substituído.

O SDK do AccessEnabler iOS/tvOS é compatível **substituição do todo** objeto JSON de informações do cliente por meio do [setOptions](/help/authentication/iostvos-sdk-api-reference.md#setoptions)parâmetro device_info de .

>[!CAUTION]
>
>O *device_info* o valor do parâmetro deve ser um **Codificado em Base64** *NSString* valor.
>
>Caso o aplicativo do programador decida passar o *device_info*, todas as chaves de informações do cliente computadas pelo SDK do AccessEnabler iOS/tvOS serão substituídas. Portanto, é muito importante calcular e transmitir os valores para o máximo possível de chaves. Para obter mais detalhes sobre a implementação, consulte o [Visão geral](#pass-client-info-overview) e a [Guia do iOS/tvOS](#ios-tvos).

#### Android/FireOS SDK {#and-fire-os-sdk}

O `AccessEnabler` O Android/FireOS SDK cria por padrão um objeto JSON de informações do cliente, que será passado para os serviços de autenticação da Adobe Primetime, a menos que substituído.

O `AccessEnabler` Suporte ao Android/FireOS SDK **substituição do todo** objeto JSON de informações do cliente por meio do [setOptions](/help/authentication/android-sdk-api-reference.md#setOptions)&#39;s/[setOptions](/help/authentication/amazon-fireos-native-client-api-reference.md#fire_setOption)&#39;s `device_info` parâmetro.

>[!NOTE]
>
>O `device_info` o valor do parâmetro deve ser um **Codificado em Base64** Valor da string.

>[!IMPORTANT]
>
>Caso o aplicativo do programador decida passar o `device_info`, depois todas as chaves de informações do cliente computadas pela variável `AccessEnabler` O Android/FireOS SDK será substituído. Portanto, é muito importante calcular e transmitir os valores para o máximo possível de chaves. Para obter mais detalhes sobre a implementação, consulte o [Visão geral](#pass-client-info-overview) e a [Android](#android) e [FireOS](#fire-tv) livro de receitas.

## Livros {#cookbooks}

Esta seção apresenta um guia para criar as informações do cliente Objeto JSON no caso de tipos de dispositivos diferentes.

>[!IMPORTANT]
>
>As teclas marcadas com  **!** são obrigatórias para serem enviadas.

### Android {#android}

As informações do dispositivo podem ser construídas da seguinte forma:

|  | Chave | Origem | Valor (exemplo) |
|---|---------------|-----------------------------|---------------|
| ! | modelo | Build.MODEL | GT-I9505 |
|  | vendor | Build.BRAND | samsung |
|  | fabricante | Build.MANUFACTURER | samsung |
| ! | version | Build.DEVICE | jflte |
|  | displayWidth | DisplayMetrics.widthPixels | 600 |
|  | displayHeight | DisplayMetrics.heightPixels | 800 |
| ! | osName | codificado | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.0.1 |

As informações de conexão podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (exemplo) |
|---|---|---|---|
| ! | connectionType | `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>` `getSystemService(Context.CONNECTIVITY_SERVICE).getActiveNetworkInfo().getType()` | `"WIFI","BLUETOOTH","MOBILE","ETHERNET","VPN","DUMMY","MOBILE_DUN","WIMAX","notAccessible"` |
|  | connectionSecure |  |  |

As informações do aplicativo podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (exemplo) |
|---|---------------|-----------|--------------|
|  | applicationId | codificado | CNN |

>[!IMPORTANT]
As informações do dispositivo, da conexão e do aplicativo devem ser adicionadas ao mesmo objeto JSON. Depois, o objeto resultante deve ser **Codificado em Base64**. Além disso, no caso de APIs REST de autenticação da Adobe Primetime, o valor deve ser **URL codificado**.

**Código de exemplo**

```JAVA
private JSONObject computeClientInformation() {
     String LOGGING_TAG = "DefineClass.class";
  
     JSONObject clientInformation = new JSONObject();

     String connectionType;

     try {
          ConnectivityManager cm = (ConnectivityManager) getContext().getSystemService(CONNECTIVITY_SERVICE);
          NetworkInfo activeNetwork = cm.getActiveNetworkInfo();

          if (activeNetwork != null && activeNetwork.isConnectedOrConnecting()) {
              switch (activeNetwork.getType()) {
                    case ConnectivityManager.TYPE_WIFI: {
                        connectionType = "WIFI";
                        break;
                    }
                    case ConnectivityManager.TYPE_BLUETOOTH: {
                        connectionType = "BLUETOOTH";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE: {
                        connectionType = "MOBILE";
                        break;
                    }
                    case ConnectivityManager.TYPE_ETHERNET: {
                        connectionType = "ETHERNET";
                        break;
                    }
                    case ConnectivityManager.TYPE_VPN: {
                        connectionType = "VPN";
                        break;
                    }
                    case ConnectivityManager.TYPE_DUMMY: {
                        connectionType = "DUMMY";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE_DUN: {
                        connectionType = "MOBILE_DUN";
                        break;
                    }
                    case ConnectivityManager.TYPE_WIMAX: {
                        connectionType = "WIMAX";
                        break;
                    }
                    default:
                       connectionType = ConnectivityManager.EXTRA_OTHER_NETWORK_INFO;
              }
          } else {
                connectionType = ConnectivityManager.EXTRA_NO_CONNECTIVITY;
          }
     } catch (Exception e) {
          connectionType = "notAccessible";
     }

     try {
          clientInformation.put("model",Build.MODEL);
          clientInformation.put("vendor", Build.BRAND);
          clientInformation.put("manufacturer",Build.MANUFACTURER);
          clientInformation.put("version",Build.DEVICE);
          clientInformation.put("osName","Android");
          clientInformation.put("osVersion",Build.VERSION.RELEASE);
          clientInformation.put("connectionType",connectionType);
          clientInformation.put("applicationId","CNN");
     } catch (JSONException e) {
          Log.e(LOGGING_TAG, e.getMessage());
     }

     return Base64.encodeToString(clientInformation.toString().getBytes(), Base64.NO_WRAP);
}
```

>[!NOTE]
**Recursos:**
* classe pública [build](https://developer.android.com/reference/android/os/Build.html){target=_blank} na documentação dos desenvolvedores Java.


### FireTV {#fire-tv}

As informações do dispositivo podem ser construídas da seguinte forma:

|  | Chave | Origem | Valor (por exemplo) |
|---|---------------|-----------------------------|--------------|
| ! | modelo | Build.MODEL | AFTM |
|  | vendor | Build.BRAND | Amazon |
|  | fabricante | Build.MANUFACTURER | Amazon |
| ! | version | Build.DEVICE | montoya |
|  | displayWidth | DisplayMetrics.widthPixels |  |
|  | displayHeight | DisplayMetrics.heightPixels |  |
| ! | osName | codificado | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.1.1 |

As informações de conexão podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (exemplo) |
|---|------------------|--------|---------------|
| ! | connectionType |  |  |
|  | connectionSecure |  |  |

As informações do aplicativo podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (exemplo) |
|---|---------------|-----------|--------------|
|  | applicationId | codificado | CNN |

>[!IMPORTANT]
As informações do dispositivo, da conexão e do aplicativo devem ser adicionadas ao mesmo objeto JSON. Depois, o objeto resultante deve ser **Codificado em Base64**. Além disso, no caso de APIs REST de autenticação da Adobe Primetime, o valor deve ser **URL codificado**.

>[!NOTE]
**Recursos:**
* classe pública [Criar](https://developer.android.com/reference/android/os/Build.html){target=_blank} na documentação dos desenvolvedores do Android.
* [Identificação de dispositivos FireTV](https://developer.amazon.com/docs/fire-tv/identify-amazon-fire-tv-devices.html){target=_blank}


### iOS/tvOS {#ios-tvos}

As informações do dispositivo podem ser construídas da seguinte forma:

|  | Chave | Origem | Valor (exemplo) |
|---|---------------|------------------------|--------------|
| ! | modelo | uname.machine | iPhone |
|  | vendor | codificado | Apple |
|  | fabricante | codificado | Apple |
| ! | version | uname.machine | 8,1 |
|  | displayWidth | UIScreen.mainScreen | 320 |
|  | displayHeight | UIScreen.mainScreen | 568 |
| ! | osName | UIDevice.systemName | iOS |
| ! | osVersion | UIDevice.systemVersion | 10.2 |

As informações de conexão podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (exemplo) |
|---|------------------|-------------------------------------------|--------------|
| ! | connectionType | [Acessível currentReachabilityStatus] |  |
|  | connectionSecure |  |  |


As informações do aplicativo podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (exemplo) |
|---|---------------|-----------|--------------|
|  | applicationId | codificado | CNN |

>[!IMPORTANT]
As informações do dispositivo, da conexão e do aplicativo devem ser adicionadas ao mesmo objeto JSON. Posteriormente, o objeto resultante deve ser codificado em Base64. Além disso, no caso de APIs REST de autenticação da Adobe Primetime, o valor deve ser codificado no URL.

**Código de exemplo**

```C
+ (NSString *)computeClientInformation {        
        struct utsname u;
        uname(&u);

        NSString *hardware = [NSString stringWithCString:u.machine encoding:NSUTF8StringEncoding];

        UIDevice *device = [UIDevice currentDevice];

        NSString *deviceType;

        switch (UI_USER_INTERFACE_IDIOM()) {
            case UIUserInterfaceIdiomPhone:
                deviceType = @"MobilePhone";
                break;
            case UIUserInterfaceIdiomPad:
                deviceType = @"Tablet";
                break;
            case UIUserInterfaceIdiomTV:
                deviceType = @"TV";
                break;
            default:
                deviceType = @"Unknown";
        }

        CGRect screenRect = [[UIScreen mainScreen] bounds];
        NSNumber *screenWidth = @((float) screenRect.size.width);
        NSNumber *screenHeight = @((float) screenRect.size.height);

        Reachability *reachability = [Reachability reachabilityForInternetConnection];
        [reachability startNotifier];

        NetworkStatus status = [reachability currentReachabilityStatus];

        NSString *connectionType;

        if (status == NotReachable) {
            connectionType = @"notConnected";
        } else if (status == ReachableViaWiFi) {
            connectionType = @"WiFi";
        } else if (status == ReachableViaWWAN) {
            connectionType = @"cellular";
        }

        NSMutableDictionary *clientInformation = [@{
                @"type": deviceType,
                @"model": device.model,
                @"vendor": @"Apple",
                @"manufacturer": @"Apple",
                @"version": [hardware stringByReplacingOccurrencesOfString:device.model withString:@""],
                @"osName": device.systemName,
                @"osVersion": device.systemVersion,
                @"displayWidth": screenWidth,
                @"displayHeight": screenHeight,
                @"connectionType": connectionType,
                @"applicationId": @"CNN" 
        } mutableCopy];

        NSError *error;
        NSData *jsonData = [NSJSONSerialization dataWithJSONObject:clientInformation options:NSJSONWritingPrettyPrinted error:&error];
        NSString *base64Encoded = [jsonData base64EncodedStringWithOptions:0];

        return base64Encoded;
}
```

>[!NOTE]
**Recursos:**
* [UIDevice](https://developer.apple.com/documentation/uikit/uidevice#//apple_ref/occ/cl/UIDevice){target=_blank}
* [uname](https://man7.org/linux/man-pages/man2/uname.2.html){target=_blank}
* [Sobre a acessibilidade](https://developer.apple.com/library/archive/samplecode/Reachability/Introduction/Intro.html){target=_blank}


### Roku {#roku}

As informações do dispositivo podem ser construídas da seguinte forma:

| Chave | Origem | Valor (exemplo) |  |
|-----|---------------|--------------------------------------------|-----------------|
| ! | modelo | codificado | &quot;Roku&quot; |
|  | vendor | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;, &quot;Roku&quot; |
|  | fabricante | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;, &quot;Roku&quot; |
| ! | version | ifDeviceInfo.GetModelDetails().ModelNumber | &quot;5303X&quot; |
|  | displayWidth | ifDeviceInfo.GetDisplaySize().w | 1920 |
|  | displayHeight | ifDeviceInfo.GetDisplaySize().h | 1080 |
| ! | osName | codificado | &quot;Roku&quot; |
| ! | osVersion | ifDeviceInfo.getVersion() |  |

As informações de conexão podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (exemplo) |
|---|---|---|---|
| ! | connectionType | ifDeviceInfo.GetConnectionType() | &quot;WifiConnection&quot;, &quot;WiredConnection&quot; |
|  | connectionSecure | codificado | true se a conexão estiver com fio |

As informações do aplicativo podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (exemplo) |
|---|---------------|-----------|--------------|
|  | applicationId | codificado | CNN |

>[!IMPORTANT]
As informações do dispositivo, da conexão e do aplicativo devem ser adicionadas ao mesmo objeto JSON. Depois, o objeto resultante deve ser **Codificado em Base64**. Além disso, no caso de APIs REST de autenticação da Adobe Primetime, o valor deve ser codificado no URL.

>[!NOTE]
Para obter mais informações, consulte [ifDeviceInfo](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md)

### XBOX 1/360 {#xbox}

As informações do dispositivo podem ser construídas da seguinte forma:

|  | Chave | Origem | Valor (exemplo) |
|---|---|---|---|
| ! | modelo | EasClientDeviceInformation.SystemProductName |  |
|  | vendor | codificado | Microsoft |
|  | fabricante | codificado | Microsoft |
| ! | version | EasClientDeviceInformation.SystemHardwareVersion |  |
|  | displayWidth | DisplayInformation.ScreenWidthInRawPixels | 1920 |
|  | displayHeight | DisplayInformation.ScreenHeightInRawPixels | 1080 |
| ! | osName | EasClientDeviceInformation.OperatingSystem |  |
| ! | osVersion | EasClientDeviceInformation.SystemFirmwareVersion |  |

As informações de conexão podem ser construídas da seguinte maneira:

|  | Chave | Origem | Exemplo |
|---|---|---|---|
| ! | connectionType |  |  |
|  | connectionSecure | NetworkAuthenticationType | &quot;Nenhum&quot;, &quot;Wpa&quot; etc |

As informações do aplicativo podem ser construídas da seguinte maneira:

| Chave | Origem | Valor (exemplo) |
|---|---|---|
| applicationId | codificado | CNN |

>[!IMPORTANT]
As informações do dispositivo, da conexão e do aplicativo devem ser adicionadas ao mesmo objeto JSON. Depois, o objeto resultante deve ser **Codificado em Base64**. Além disso, no caso de APIs REST de autenticação da Adobe Primetime, o valor deve ser **URL codificado**.

**Recursos**

* [Classe EasClientDeviceInformation](https://docs.microsoft.com/en-us/uwp/api/windows.security.exchangeactivesyncprovisioning.easclientdeviceinformation?view=winrt-22000)
* [Classe DisplayInformation](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.display.displayinformation?view=winrt-22000)


