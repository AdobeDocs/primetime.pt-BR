---
title: Transmissão de informações do cliente (dispositivo, conexão e aplicativo)
description: Transmissão de informações do cliente (dispositivo, conexão e aplicativo)
exl-id: 0b21ef0e-c169-48ff-ac01-25411cfece1e
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 0%

---

# Transmissão de informações do cliente (dispositivo, conexão e aplicativo) {#pass-client-info}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.


## Escopo {#pass-client-info-scope}

Este documento agrega detalhes e manuais para transmitir informações do cliente (dispositivo, conexão e aplicativo) de um aplicativo do programador para APIs REST de autenticação do Adobe Primetime ou SDKs.

Os benefícios de fornecer informações aos clientes são:

* A capacidade de habilitar adequadamente a Autenticação da Base Inicial (HBA) no caso de alguns tipos de dispositivos e MVPDs que possam oferecer suporte a HBA.
* A capacidade de aplicar corretamente TTLs no caso de alguns tipos de dispositivos (por exemplo, configurar TTLs mais longos para sessões de autenticação em dispositivos conectados a TV).
* A capacidade de agregar adequadamente as métricas de negócios em relatórios detalhados entre tipos de dispositivos usando o ESM (Entitlement Service Monitoring, monitoramento do serviço de qualificação).
* Desbloqueia a capacidade de aplicar corretamente várias regras de negócios (por exemplo, degradação) em tipos específicos de dispositivos.

## Visão geral {#pass-client-info-overview}

As informações do cliente consistem em:

* **Dispositivo** Informações sobre os atributos de hardware e software do dispositivo de onde o usuário está tentando consumir o conteúdo do Programador.
* **Conexão** informações sobre os atributos de conexão do dispositivo a partir do qual o usuário está se conectando aos serviços de autenticação da Adobe Primetime e/ou aos serviços do programador (por exemplo, implementações de servidor para servidor).
* **Aplicativo** informações sobre o aplicativo registrado de onde o usuário está tentando consumir o conteúdo do Programador.

As informações do cliente são um objeto JSON criado com chaves apresentadas na tabela a seguir.

>[!NOTE]
>
>As seguintes **chaves** são **obrigatório** para ser enviado no objeto JSON de informações do cliente: **modelo**, **osName**.
>
>As seguintes chaves têm **restrito** valores: `primaryHardwareType`, `osName`, `osFamily`, `browserName`, `browserVendor`, `connectionSecure`.

|  | Chave | Restrito | Descrição | Valores possíveis |
|---|---|---|---|---|
|  | primaryHardwareType | # Sim | O tipo de hardware principal do dispositivo. | # Os valores são restritos: Camera DataCollectionTerminal Desktop EmbeddedNetworkModule eReader GamesConsole GeolocationTracker Glasses MediaPlayer MobilePhone PaymentTerminal PluginModem SetTopBox TV Tablet WirelessHotspot Wristwatch Unknown |
| #mandatory | modelo | Não | O nome do modelo do dispositivo. | Por exemplo, iPhone, SM-G930V, Apple TV etc. |
|  | version | Não | A versão do dispositivo. | Por exemplo, 2.0.1, etc. |
|  | fabricante | Não | A empresa/organização de fabricação do dispositivo. | Por exemplo, Samsung, LG, ZTE, Huawei, Motorola, Apple, etc. |
|  | fornecedor | Não | A empresa/organização de venda do dispositivo. | Por exemplo, Apple, Samsung, LG, Google, etc. |
| #mandatory | osName | # Sim | O nome do sistema operacional do dispositivo. | # Os valores são restritos: Android Chrome OS Linux Mac OS X OpenBSD Roku OS Windows iOS tvOS webOS |
|  | osFamily | Sim | O nome do grupo do Sistema Operacional (SO) do dispositivo. | # Os valores são restritos: Android BSD Linux PlayStation OS Roku OS Symbian Tizen Windows iOS macOS tvOS webOS |
|  | osVendor | Não | O fornecedor do sistema operacional do dispositivo. | Amazon Apple Google LG Microsoft Mozilla Nintendo Nokia Roku Samsung Projeto Sony Tizen |
|  | osVersion | Não | A versão do sistema operacional do dispositivo. | Por exemplo, 10.2, 9.0.1, etc. |
|  | browserName | # Sim | O nome do navegador. | # Os valores são restritos: Navegador Android Chrome Edge Firefox Internet Explorer Opera Safari SeaMonkey Symbian Browser |
|  | browserVendor | # Sim | A empresa/organização de construção do navegador. | # Os valores são restritos: Amazon Apple Google Microsoft Motorola Mozilla Netscape Nintendo Nokia Samsung Sony Ericsson |
|  | browserVersion | Não | A versão do navegador do dispositivo. | ex: 60.0.3112 |
|  | userAgent | Não | O agente do usuário do dispositivo. | por exemplo, Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/602.4.8 (KHTML, como Gecko) Versão/10.0.3 Safari/602.4.8 |
|  | displayWidth | Não | A largura da tela física do dispositivo. |  |
|  | displayHeight | Não | A altura da tela física do dispositivo. |  |
|  | displayPpi | Não | A densidade de pixels da tela física do dispositivo. | por exemplo, 294 |
|  | diagonalScreenSize | Não | A dimensão diagonal da tela física do dispositivo em polegadas. | Por exemplo, 5.5, 10.1 |
|  | connectionIp | Não | O IP do dispositivo usado para enviar solicitações HTTP. | Por exemplo, 8.8.4.4 |
|  | connectionPort | Não | A porta do dispositivo usada para enviar solicitações HTTP. | por exemplo, 53124 |
|  | connectionType | Não | O tipo de conexão de rede. | por exemplo, WiFi, LAN, 3G, 4G, 5G |
|  | connectionSecure | # Sim | O status de segurança da conexão de rede. | # Os valores são restritos: true - no caso de uma rede segura false - no caso de um hot spot público |
|  | applicationId | Não | O identificador exclusivo do aplicativo. | por exemplo, CNN |

## Referências de API {#api-ref}

Esta seção apresenta a API responsável por manipular informações do cliente ao usar as APIs REST de autenticação da Adobe Primetime ou SDKs.

### REST API {#rest-api}

Os serviços de Autenticação da Adobe Primetime oferecem suporte para o recebimento de informações do cliente das seguintes maneiras:

* Como um **cabeçalho: &quot;X-Device-Info&quot;**
* Como um **parâmetro de consulta: &quot;device_info&quot;**
* Como um **parâmetro de publicação: &quot;device_info&quot;**

>[!IMPORTANT]
>
>Nos três cenários, a carga do cabeçalho ou parâmetro deve ser **Codificado em Base64 e codificado em URL**.

**SDK**

#### SDK do JavaScript {#js-sdk}

O SDK do JavaScript do AccessEnabler cria por padrão um objeto JSON de informações do cliente, que será passado para os serviços de autenticação da Adobe Primetime, a menos que seja substituído.

O SDK JavaScript do AccessEnabler é compatível **somente substituição** a chave &quot;applicationId&quot; do objeto JSON de informações do cliente por meio do [setRequestor](/help/authentication/javascript-sdk-api-reference.md#setrequestor(inRequestorID,endpoints,options))do *applicationId* parâmetro de opções.

>[!CAUTION]
>
>A variável `applicationId` O valor do parâmetro deve ser um valor de sequência de caracteres de texto sem formatação.
>Se o aplicativo Programmer decidir passar o applicationId, o restante das chaves de informações do cliente ainda será calculado pelo SDK JavaScript do AccessEnabler.

#### iOS/tvOS SDK {#ios-tvos-sdk}

O SDK iOS/tvOS do AccessEnabler cria por padrão um objeto JSON de informações do cliente, que será passado para os serviços de autenticação da Adobe Primetime, a menos que seja substituído.

O SDK AccessEnabler iOS/tvOS é compatível **substituição de todo o** objeto JSON de informações do cliente por meio do [setOptions](/help/authentication/iostvos-sdk-api-reference.md#setoptions)parâmetro device_info de.

>[!CAUTION]
>
>A variável *device_info* o valor do parâmetro deve ser um **Codificado em Base64** *NSString* valor.
>
>Caso o aplicativo Programador decida passar o *device_info*, todas as chaves de informações do cliente computadas pelo SDK iOS/tvOS do AccessEnabler serão substituídas. Portanto, é muito importante calcular e transmitir os valores para o maior número possível de chaves. Para obter mais detalhes sobre a implementação, consulte [Visão geral](#pass-client-info-overview) tabela e o [Guia do iOS/tvOS](#ios-tvos).

#### Android/FireOS SDK {#and-fire-os-sdk}

A variável `AccessEnabler` O SDK do Android/FireOS cria por padrão um objeto JSON de informações do cliente, que será passado para os serviços de autenticação da Adobe Primetime, a menos que seja substituído.

A variável `AccessEnabler` Suporte ao SDK do Android/FireOS **substituição de todo o** objeto JSON de informações do cliente por meio do [setOptions](/help/authentication/android-sdk-api-reference.md#setOptions)s/[setOptions](/help/authentication/amazon-fireos-native-client-api-reference.md#fire_setOption)do `device_info` parâmetro.

>[!NOTE]
>
>A variável `device_info` o valor do parâmetro deve ser um **Codificado em Base64** Valor da string.

>[!IMPORTANT]
>
>Caso o aplicativo Programador decida passar o `device_info`, todas as chaves de informações do cliente calculadas pelo `AccessEnabler` O Android/FireOS SDK será substituído. Portanto, é muito importante calcular e transmitir os valores para o maior número possível de chaves. Para obter mais detalhes sobre a implementação, consulte [Visão geral](#pass-client-info-overview) tabela e o [Android](#android) e [FireOS](#fire-tv) guia.

## Cookbooks {#cookbooks}

Esta seção apresenta um guia para criar o objeto JSON de informações do cliente no caso de diferentes tipos de dispositivos.

>[!IMPORTANT]
>
>As chaves marcadas com  **!** são obrigatórios para serem enviados.

### Android {#android}

As informações do dispositivo podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (exemplo) |
|---|---------------|-----------------------------|---------------|
| ! | modelo | Build.MODEL | GT-I9505 |
|  | fornecedor | Build.BRAND | samsung |
|  | fabricante | Build.MANUFACTURER | samsung |
| ! | version | Build.DEVICE | jflet |
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
As informações do dispositivo, da conexão e do aplicativo devem ser adicionadas ao mesmo objeto JSON. Posteriormente, o objeto resultante deve ser **Codificado em Base64**. Além disso, no caso de REST APIs de autenticação do Adobe Primetime, o valor deve ser **URL codificado**.

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

As informações do dispositivo podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (por exemplo) |
|---|---------------|-----------------------------|--------------|
| ! | modelo | Build.MODEL | AFTM |
|  | fornecedor | Build.BRAND | Amazon |
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
As informações do dispositivo, da conexão e do aplicativo devem ser adicionadas ao mesmo objeto JSON. Posteriormente, o objeto resultante deve ser **Codificado em Base64**. Além disso, no caso de REST APIs de autenticação do Adobe Primetime, o valor deve ser **URL codificado**.

>[!NOTE]
**Recursos:**
* classe pública [Build](https://developer.android.com/reference/android/os/Build.html){target=_blank} na documentação dos desenvolvedores do Android.
* [Identificação de dispositivos FireTV](https://developer.amazon.com/docs/fire-tv/identify-amazon-fire-tv-devices.html){target=_blank}


### iOS/tvOS {#ios-tvos}

As informações do dispositivo podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (exemplo) |
|---|---------------|------------------------|--------------|
| ! | modelo | uname.machine | iPhone |
|  | fornecedor | codificado | Apple |
|  | fabricante | codificado | Apple |
| ! | version | uname.machine | 8,1 |
|  | displayWidth | UIScreen.mainScreen | 320 |
|  | displayHeight | UIScreen.mainScreen | 568 |
| ! | osName | UIDevice.systemName | iOS |
| ! | osVersion | UIDevice.systemVersion | 10.2 |

As informações de conexão podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (exemplo) |
|---|------------------|-------------------------------------------|--------------|
| ! | connectionType | [Capacidade de alcance currentReachabilityStatus] |  |
|  | connectionSecure |  |  |


As informações do aplicativo podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (exemplo) |
|---|---------------|-----------|--------------|
|  | applicationId | codificado | CNN |

>[!IMPORTANT]
As informações do dispositivo, da conexão e do aplicativo devem ser adicionadas ao mesmo objeto JSON. Posteriormente, o objeto resultante deve ser codificado na Base64. Além disso, no caso das REST APIs de autenticação da Adobe Primetime, o valor deve ser codificado no URL.

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
* [Sobre acessibilidade](https://developer.apple.com/library/archive/samplecode/Reachability/Introduction/Intro.html){target=_blank}


### Roku {#roku}

As informações do dispositivo podem ser construídas da seguinte maneira:

| Chave | Origem | Valor (exemplo) |  |
|-----|---------------|--------------------------------------------|-----------------|
| ! | modelo | codificado | &quot;Roku&quot; |
|  | fornecedor | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;, &quot;Roku&quot; |
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
|  | connectionSecure | codificado | true se a conexão for com fio |

As informações do aplicativo podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (exemplo) |
|---|---------------|-----------|--------------|
|  | applicationId | codificado | CNN |

>[!IMPORTANT]
As informações do dispositivo, da conexão e do aplicativo devem ser adicionadas ao mesmo objeto JSON. Posteriormente, o objeto resultante deve ser **Codificado em Base64**. Além disso, no caso das REST APIs de autenticação da Adobe Primetime, o valor deve ser codificado no URL.

>[!NOTE]
Para obter mais informações, consulte [ifDeviceInfo](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md)

### XBOX 1/360 {#xbox}

As informações do dispositivo podem ser construídas da seguinte maneira:

|  | Chave | Origem | Valor (exemplo) |
|---|---|---|---|
| ! | modelo | EasClientDeviceInformation.SystemProductName |  |
|  | fornecedor | codificado | Microsoft |
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
As informações do dispositivo, da conexão e do aplicativo devem ser adicionadas ao mesmo objeto JSON. Posteriormente, o objeto resultante deve ser **Codificado em Base64**. Além disso, no caso de REST APIs de autenticação do Adobe Primetime, o valor deve ser **URL codificado**.

**Recursos**

* [Classe EasClientDeviceInformation](https://docs.microsoft.com/en-us/uwp/api/windows.security.exchangeactivesyncprovisioning.easclientdeviceinformation?view=winrt-22000)
* [Classe DisplayInformation](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.display.displayinformation?view=winrt-22000)
