---
description: Você pode usar os recursos do sistema de Digital Rights Management do Primetime (DRM) para fornecer acesso seguro ao conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa para a solução integrada Adobe.
title: DRM Widevine
exl-id: 44ab032e-e665-4b63-a08b-54e862894987
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# DRM Widevine {#widevine-drm}

Você pode usar os recursos do sistema de Digital Rights Management do Primetime (DRM) para fornecer acesso seguro ao conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa para a solução integrada Adobe.

Entre em contato com o representante da Adobe para obter as informações mais atualizadas sobre a disponibilidade de soluções de DRM de terceiros.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

Você pode usar o DRM Widevine nativo do Android com fluxos HLS CMAF.

>[!NOTE]
>
> O esquema CTR do Widevine CENC requer no mínimo a versão 4.4 do Android (Nível 19 da API).
>
> O esquema CBCS Widevine exige a versão mínima do Android 7.1 (Nível de API 25).

## Definir detalhes do servidor de licenças {#license-server-details}

Chame o seguinte `com.adobe.mediacore.drm.DRMManager` API antes de carregar o recurso MediaPlayer:

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### Argumentos {#arguments-license-server}

* `drm` - `"com.widevine.alpha"` para Widevine.

* `licenseServerURL` - O URL do servidor de licenças Widevine que recebe solicitações de licença.

* `requestProperties` - Contém cabeçalhos extras a serem incluídos na solicitação de licença de saída.

Por exemplo, ao usar o conteúdo empacotado para o ExpressPlay DRM, use o seguinte código antes de reproduzir:

```java
DRMManager.setProtectionData(
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null);
```

## Fornecer retorno de chamada personalizado {#custom-callback}

Chame o seguinte `com.adobe.mediacore.drm.DRMManager` antes de carregar o recurso MediaPlayer.

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### Argumentos {#arguments-custom-callback}

* `callback` - implementação personalizada do MediaDrmCallback a ser usada em vez do padrão `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

Para obter detalhes, consulte [Documentação da API do Android TVSDK 3.11](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html).

## Buscar caixa PSSH do recurso MediaPlayer carregado no momento {#pssh-box-mediaplayer-resoource}

Chame o seguinte `com.adobe.mediacore.drm.DRMManager` API, de preferência na implementação de retorno de chamada personalizado.

```java
public static byte[] getPSSH()
```

A API retorna a caixa de cabeçalho específica do sistema de proteção associada ao recurso de mídia Widevine carregado.

Uma caixa válida está disponível por curto período (entre a criação da instância de DRM e o carregamento de chaves). `MediaDrmCallback callback executeKeyRequest()` O pode usá-lo para personalizar a obtenção de chaves de licença.

>[!NOTE]
>
> `getPSSH()` A API é compatível somente com instância de player único. Vários players ou o recurso Instant On devem inicializar serialmente para receber a caixa correta.
