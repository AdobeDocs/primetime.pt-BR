---
description: Alguns anúncios de terceiros (ou anúncios criativos) não podem ser associados ao fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. Como opção, a inserção do anúncio Primetime e o TVSDK podem tentar reempacotar anúncios incompatíveis em vídeos compatíveis do M3U8.
seo-description: Alguns anúncios de terceiros (ou anúncios criativos) não podem ser associados ao fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. Como opção, a inserção do anúncio Primetime e o TVSDK podem tentar reempacotar anúncios incompatíveis em vídeos compatíveis do M3U8.
seo-title: Reempacotar anúncios incompatíveis usando o Adobe Creative Repacking Service
title: Reempacotar anúncios incompatíveis usando o Adobe Creative Repacking Service
uuid: 56a2405d-b395-4fea-820d-343590be7c19
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Reempacotar anúncios incompatíveis usando o Adobe Creative Repacking Service {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Alguns anúncios de terceiros (ou anúncios criativos) não podem ser associados ao fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. Como opção, a inserção do anúncio Primetime e o TVSDK podem tentar reempacotar anúncios incompatíveis em vídeos compatíveis do M3U8.

Os anúncios veiculados de vários terceiros, como um servidor de agência, seu parceiro de inventário ou uma rede de anúncios, geralmente são veiculados em formatos incompatíveis, como o download progressivo de MP4.

Quando o TVSDK encontra um anúncio incompatível pela primeira vez, o player ignora o anúncio e emite uma solicitação para o serviço de reempacotamento de anúncios (CRS), que faz parte do back-end de inserção de anúncios do Primetime, para reempacotar o anúncio em um formato compatível. O CRS tenta gerar execuções M3U8 de taxa múltipla do anúncio e armazena essas execuções no Primetime Content Delivery Network (CDN). Na próxima vez que o TVSDK receber uma resposta de anúncio que aponte para esse anúncio, o player usará a versão M3U8 compatível com HLS do CDN.

Para ativar esse recurso opcional, entre em contato com seu representante da Adobe.

Para obter mais informações sobre o CRS, consulte [Creative Packaging Service (CRS)](../../../dynamic-ad-insertion/creative-repackaging-service/crs-overview.md).

## Suporte a várias CDN para entrega de anúncios CRS {#section_900FDDA5454143718F1EB4C9732C8E1C}

Embora o cenário padrão do Creative Repacking Service (CRS) seja o de usar uma Content Data Network (CDN), você pode implantar ativos CRS em mais de um CDN.

Você pode usar várias CDNs pelos seguintes motivos:

* Um requisito para aumentar a escala para eventos de visualização grandes.
* Um requisito para corresponder a fonte CDN do ativo CRS à fonte CDN do conteúdo principal.

Você pode transformar o URL padrão fornecido pelo CRS usando APIs de Transformador de URL do TVSDK.

Estas são as adições de API no TVSDK:

* `PTURLTransformer` Um protocolo que descreve os métodos necessários para transformar os URLs de anúncio do CRS solicitados pelo TVSDK. Os aplicativos podem implementar este protocolo e fornecer implementações para os métodos necessários.

* `PTDefaultURLTransformer` A instância do transformador de URL padrão criada no TVSDK e que implementa o `PTURLTransformer` protocolo. Os aplicativos podem substituir essa classe ou adicionar um manipulador de transformação de URL posterior. Esse manipulador é útil quando o aplicativo deseja fazer alterações na solicitação de URL após a transformação padrão ter sido aplicada.

* `PTNetworkConfiguration setURLTransformer:defaultTransformer` Um método setter fornecido na instância de `PTNetworkConfiguration` metadados para definir a `PTURLTransformer` implementação.

>[!IMPORTANT]
>
>As implementações do aplicativo devem verificar a `PTURLTransformerInputType` enumeração e apenas transformar URLs do tipo `PTURLTransformerInputTypeCRSCreative` para CRS.

A amostra de código a seguir mostra como seu aplicativo pode alterar o componente host padrão para uma sequência de caracteres diferente (por exemplo, `cdn.mycrsdomain.com`):

```
// The sample code below uses Non-ARC code 
PTNetworkConfiguration *networkConfiguration = [[[PTNetworkConfiguration alloc] init] autorelease]; 
   
PTDefaultURLTransformer *defaultTransformer = [[[PTDefaultURLTransformer alloc] init] autorelease]; 
    [defaultTransformer addPostURLTransformHandler:^NSString *(NSString *url, PTURLTransformerInputType type) { 
        if (type == PTURLTransformerInputTypeCRSCreative) { 
            return [url stringByReplacingOccurrencesOfString:[NSURL URLWithString:url].host  
              withString:@"cdn.mycrsdomain.com"]; 
        } 
            return url; 
    }]; 
  
[networkConfiguration setURLTransformer:defaultTransformer]; 
   
// metadata is the PTMetadata instance set on a PTMediaPlayerItem instance. 
[metadata setMetadata:[self getNetworkConfiguration] forKey:PTNetworkConfigurationMetadataKey];
```
