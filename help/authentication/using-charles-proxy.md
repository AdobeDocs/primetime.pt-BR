---
title: Uso do proxy Charles
description: Uso do proxy Charles
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Uso do proxy Charles {#using-charles-proxy}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.


**Charles:** <http://charlesproxy.com>

 
## Baixar, instalar e começar a usar o Charles Proxy {#download-install-and-get-stared-with-charles-proxy}

- **Baixar** - <http://www.charlesproxy.com/download/>
- **Instalar** - <http://www.charlesproxy.com/documentation/installation/>
- **Introdução** - <http://www.charlesproxy.com/documentation/getting-started/>

 
## Guias Estrutura x Sequência {#structure-vs-sequence-tabs}

Há duas maneiras diferentes de visualizar o tráfego:

1. **Estrutura** - As solicitações são agrupadas por host
1. **Sequência** - As solicitações são listadas na ordem em que são chamadas


## SSL e certificados {#ssl-and-certificates}

Ativar proxy SSL `\[ *Proxy -\> Proxy Settings... -\> SSL* \]`

Marque a caixa de seleção &quot;Ativar proxy SSL&quot; e adicione todos os locais HTTPS.


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/ProxySettings.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/SSLSettings.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AddHttpsLocations.PNG)



- Proxies SSL - <http://www.charlesproxy.com/documentation/proxying/ssl-proxying/>
- Certificados SSL - <http://www.charlesproxy.com/documentation/using-charles/ssl-certificates/>
- Criação de proxy SSL em dispositivos móveis - Consulte abaixo.

 
## Ignorar / Excluir hosts {#ignore-/-exclude-hosts}

Se a saída se tornar muito desorganizada, é possível optar por ignorar ou excluir locais. Você pode ignorar ou excluir locais seguindo um destes procedimentos:

- Clique com o botão direito do mouse nas solicitações que deseja ignorar e selecione &quot;Ignorar&quot;
- Adicionar manualmente as localizações a serem excluídas `\[ *Proxy -\> Recording Settings... -\> Exclude* \]`

 
## Spoofing DNS {#dns-spoffing}

`\[ *Tools -\> DNS Spoofing...* \]`

 

A falsificação de DNS é muito útil ao tentar redirecionar uma solicitação para um IP diferente, especialmente ao trabalhar com dispositivos móveis:

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/DNSSpoofing.PNG)

<http://www.charlesproxy.com/documentation/tools/dns-spoofing/>

 
## Mapear remoto {#map-remote}

`\[ *Tools -\> Map Remote...* \]`

 

Com o mapa remoto, você pode redirecionar uma solicitação de &quot;entrada&quot; para um terminal diferente. O caso de uso mais comum para esse recurso é &quot;Mapear&quot; `AccessEnabler.swf` para `AccessEnablerDebug.swf:`

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/MapRemote.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/MapRemoteAdd.PNG)

<http://www.charlesproxy.com/documentation/tools/map-remote/>

 

## Proxy reverso {#reverse-proxy}

<http://www.charlesproxy.com/documentation/proxying/reverse-proxy/>

## Celular {#mobile}

### Usar o Charles em um dispositivo iOS (iPhone / iPad) {#use-charles-on-an-ios-device-(iphone-/-ipad)}

#### Conexão SSL da iPhone {#ssl-connection-from-iphone}

Navegue até <http://charlesproxy.com/charles.crt> do seu dispositivo iOS.  Isso iniciará a caixa de diálogo de instalação do certificado:

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate1\(1\).PNG)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate2\(1\).PNG)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate3.PNG)

 </br>

Clique em `\[ *Install*... *Install*... *Done* \]` para concluir a instalação do certificado.

<http://www.charlesproxy.com/documentation/faqs/ssl-connections-from-within-iphone-applications/>

 

#### Uso do Charles de um dispositivo iOS {#using-charles-from-an-ios-device}

No seu dispositivo iOS, selecione `\[ *Settings* -\> *Wi-FI* -\> (*YOUR\_WIFI\_NETWORK)* \]`. Clique na pequena seta azul ao lado da rede, vá para HTTP Proxy e selecione &quot;Manual&quot;: 


 </br>

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy1.png)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy2.PNG)


 </br>
Aqui você precisa especificar o IP e a porta da máquina em que você está executando o Charles. <span style="line-height: 1.6em;">Agora, se você abrir o Safari no dispositivo iOS e tentar abrir uma página da Web, deverá receber o seguinte pop-up na máquina que está executando o Charles:
 
 </br>

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy3.PNG)

</br>
Clique em "Permitir" para permitir que o dispositivo use o Charles para proxy em todas as solicitações.

<http://www.charlesproxy.com/documentation/faqs/using-charles-from-an-iphone/>


#### iOS - Confiar em quaisquer certificados {#ios-trust-any-certificates}

<http://stackoverflow.com/questions/933331/how-to-use-nsurlconnection-to-connect-with-ssl-for-an-untrusted-cert>

#### Erro de autenticação do iOS - não é possível encontrar adobepass.ios.app

<https://tve.zendesk.com/entries/22135907-ios-authentication-error-adobepass-ios-app-cannot-be-found>


## Usar o Charles para Android

<http://jaanus.com/post/17476995356/debugging-http-on-an-android-phone-or-tablet-with>

<http://www.charlesproxy.com/documentation/configuration/browser-and-system-configuration>


Navegue até [Charles proxy](http://charlesproxy.com/charles.crt) do seu dispositivo Android.
