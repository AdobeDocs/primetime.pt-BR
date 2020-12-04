---
description: Alguns anúncios de terceiros (ou anúncios criativos) não podem ser associados ao fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. Como opção, a inserção do anúncio Primetime e o TVSDK podem tentar empacotar novamente anúncios incompatíveis em vídeos compatíveis do M3U8.
seo-description: Alguns anúncios de terceiros (ou anúncios criativos) não podem ser associados ao fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. Como opção, a inserção do anúncio Primetime e o TVSDK podem tentar empacotar novamente anúncios incompatíveis em vídeos compatíveis do M3U8.
seo-title: Reempacotar anúncios incompatíveis usando o serviço de reempacotamento da Creative Adobe
title: Reempacotar anúncios incompatíveis usando o serviço de reempacotamento da Creative Adobe
uuid: 3bc24185-6b19-4660-bf78-5ccdaf14787a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Reempacote anúncios incompatíveis usando o Adobe Creative Repacking Service {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Alguns anúncios de terceiros (ou anúncios criativos) não podem ser associados ao fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. Como opção, a inserção do anúncio Primetime e o TVSDK podem tentar empacotar novamente anúncios incompatíveis em vídeos compatíveis do M3U8.

Os anúncios veiculados de vários terceiros, como um servidor de agência, seu parceiro de inventário ou uma rede de anúncios, geralmente são veiculados em formatos incompatíveis, como o download progressivo de MP4.

Quando o TVSDK encontra um anúncio incompatível pela primeira vez, o player ignora o anúncio e emite uma solicitação para o serviço de reempacotamento de anúncios (CRS), que faz parte do back-end de inserção de anúncios do Primetime, para reempacotar o anúncio em um formato compatível. O CRS tenta gerar execuções M3U8 de taxa múltipla do anúncio e armazena essas execuções no Primetime Content Delivery Network (CDN). Na próxima vez que o TVSDK receber uma resposta de anúncio que aponte para esse anúncio, o player usará a versão M3U8 compatível com HLS do CDN.

Para ativar este recurso opcional, entre em contato com seu representante de Adobe.

Para obter mais informações sobre o CRS, consulte [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## Suporte a vários CDN para delivery de anúncio CRS {#multiple-cdn-support-for-crs-ad-delivery}

Embora o cenário padrão do Creative Repacking Service (CRS) seja o de usar uma Content Data Network (CDN), você pode implantar ativos CRS em mais de um CDN.

Você pode usar várias CDNs pelos seguintes motivos:

* Um requisito para aumentar a escala de eventos de visualização grandes.
* Um requisito para corresponder a fonte CDN do ativo CRS à fonte CDN do conteúdo principal.

Você pode transformar o URL padrão fornecido pelo CRS usando APIs de Transformador de URL do TVSDK.

Estas são as adições de API no TVSDK:

* `URLTransformer` Uma interface que descreve os métodos necessários para transformar os URLs de anúncio do CRS solicitados pelo TVSDK. Os aplicativos podem implementar essa interface e fornecer implementações para os métodos necessários.

* `DefaultURLTransformer` A instância do transformador de URL padrão criada no TVSDK e que implementa a  `URLTransformer` interface. Os aplicativos podem substituir essa classe ou adicionar um manipulador de transformação de URL posterior. Esse manipulador é útil quando o aplicativo deseja fazer alterações na solicitação de URL após a transformação padrão ter sido aplicada.

* `NetworkConfiguration.urlTransformer` Um método setter fornecido na instância de  `NetworkConfiguration` metadados para definir a  `URLTransformer` implementação.

>[!IMPORTANT]
>
>As implementações do aplicativo devem verificar a lista discriminada `URLTransformerInputType` e apenas transformar URLs do tipo `URLTransformerInputType.CRSCreative` para CRS.

A amostra de código a seguir mostra como seu aplicativo pode alterar o componente host padrão para uma sequência de caracteres diferente (por exemplo, `cdn.mycrsdomain.com`):

```
var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   
var urlTransformer:DefaultURLTransformer = new DefaultURLTransformer(); 
urlTransformer.addPostURLTransformHandler(function (url:String, type:String) { 
    if (type == URLTransformerInputType.CRSCreative) { 
        return url.replace(URLUtil.getServerName(url), "cdn.mycrsdomain.com"); 
    } 
    return url; 
}); 
  
networkConfiguration.urlTransformer = urlTransformer; 
   
// metadata is the Metadata instance set on a MediaResource instance. 
metadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                     networkConfiguration);
```
