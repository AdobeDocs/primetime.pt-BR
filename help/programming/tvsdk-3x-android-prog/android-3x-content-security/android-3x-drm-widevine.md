---
description: Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao seu conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa à solução integrada da Adobe.
seo-description: Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao seu conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa à solução integrada da Adobe.
seo-title: DRM widevine
title: DRM widevine
uuid: 3a5fd786-4319-4e92-83b6-0f5328df6a44
translation-type: tm+mt
source-git-commit: ddcdf38fb7a77b7609a21bbdf6b32188b917e22c

---


# DRM widevine {#widevine-drm}

Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao seu conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa à solução integrada da Adobe.

Entre em contato com seu representante da Adobe para obter as informações mais atualizadas sobre a disponibilidade de soluções de DRM de terceiros.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

Você pode usar o Android native Widevine DRM com fluxos HLS CMAF.

>[!NOTE]
>
> O Esquema CENC CTR de widevine requer a versão 4.4 mínima do Android (API nível 19).
>
> O Esquema CBCS da Widevine requer a versão mínima 7.1 do Android (API nível 25).

## Definir detalhes do servidor de licenças {#license-server-details}

Chame a seguinte API antes de carregar o recurso MediaPlayer: `com.adobe.mediacore.drm.DRMManager`

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### Argumentos {#arguments-license-server}

* `drm` - `"com.widevine.alpha"` Widevine.

* `licenseServerURL` - O URL do servidor de licenças do Widevine que recebe solicitações de licença.

* `requestProperties` - Contém cabeçalhos adicionais para incluir na solicitação de licença de saída.

Por exemplo, ao usar o conteúdo empacotado para o DRM de apresentação, use o seguinte código antes de reproduzir:

```java
DRMManager.setProtectionData(
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null);
```

## Fornecer retorno de chamada personalizado {#custom-callback}

Chame a seguinte API antes de carregar o recurso MediaPlayer. `com.adobe.mediacore.drm.DRMManager`

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### Argumentos {#arguments-custom-callback}

* `callback` - implementação personalizada de MediaDrmCallback para usar em vez do padrão `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

Para obter detalhes, consulte Referência da API 3.11.

## Buscar caixa PSSH do recurso atual carregado do MediaPlayer {#pssh-box-mediaplayer-resoource}

Chame a seguinte API, de preferência na implementação de retorno de chamada personalizada. `com.adobe.mediacore.drm.DRMManager`

```java
public static byte[] getPSSH()
```

A API retorna a Caixa de cabeçalho específico do sistema de proteção associada ao recurso de mídia do Widevine carregado.

Uma caixa válida está disponível por curta duração (entre a criação da instância do DRM e o carregamento das chaves). `MediaDrmCallback callback executeKeyRequest()` pode usá-lo para personalizar a busca de chaves de licença.

>[!NOTE]
>
> `getPSSH()` A API é compatível apenas com uma instância de player único. Vários players ou o recurso Instant On deve ser inicializado em série para receber a caixa correta.
