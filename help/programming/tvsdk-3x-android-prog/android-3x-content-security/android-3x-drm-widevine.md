---
description: Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao conteúdo de vídeo. Como alternativa, você pode usar soluções DRM de terceiros como uma alternativa para a solução integrada Adobe.
title: DRM de widevina
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# DRM {#widevine-drm} da janela

Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao conteúdo de vídeo. Como alternativa, você pode usar soluções DRM de terceiros como uma alternativa para a solução integrada Adobe.

Entre em contato com seu representante de Adobe para obter as informações mais atualizadas sobre a disponibilidade de soluções de DRM de terceiros.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

Você pode usar o DRM nativo da Widevine do Android com fluxos HLS CMAF.

>[!NOTE]
>
> O Esquema de CTR CENC de viúva requer o Android versão 4.4 (Nível de API 19).
>
> O Esquema CBCS de Widevine requer a versão mínima 7.1 do Android (Nível de API 25).

## Definir detalhes do servidor de licenças {#license-server-details}

Chame a seguinte API `com.adobe.mediacore.drm.DRMManager` antes de carregar o recurso MediaPlayer:

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### Argumentos {#arguments-license-server}

* `drm` -  `"com.widevine.alpha"` para Widevine.

* `licenseServerURL` - O URL do servidor de licenças do Widevine que recebe solicitações de licença.

* `requestProperties` - Contém cabeçalhos extras para incluir na solicitação de licença de saída.

Por exemplo, ao usar o conteúdo empacotado para o DRM de exibição, use o seguinte código antes de reproduzir:

```java
DRMManager.setProtectionData(
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null);
```

## Fornecer retorno de chamada personalizado {#custom-callback}

Chame a seguinte API `com.adobe.mediacore.drm.DRMManager` antes de carregar o recurso MediaPlayer.

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### Argumentos {#arguments-custom-callback}

* `callback` - implementação personalizada de MediaDrmCallback para usar em vez do padrão  `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

Para obter detalhes, consulte a [documentação da API do Android TVSDK 3.1](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html).

## Buscar caixa PSSH do recurso atual do MediaPlayer {#pssh-box-mediaplayer-resoource} carregado

Chame a seguinte API `com.adobe.mediacore.drm.DRMManager` , preferencialmente na implementação de retorno de chamada personalizada.

```java
public static byte[] getPSSH()
```

A API retorna a Caixa de Cabeçalho Específico do Sistema de Proteção associada ao recurso de mídia Widevine carregado.

Uma caixa válida está disponível por curta duração (entre a criação da instância DRM e o carregamento de chaves). `MediaDrmCallback callback executeKeyRequest()` Você pode usá-lo para personalizar a busca de chaves de licença.

>[!NOTE]
>
> `getPSSH()` A API é compatível somente com uma instância do reprodutor único. Vários players ou o recurso Instant On deve ser inicializado em série para receber a caixa correta.
