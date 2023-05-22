---
description: Alguns anúncios de terceiros (ou criativos) não podem ser compilados no fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. A inserção de anúncios do Primetime e o TVSDK podem, opcionalmente, tentar reempacotar anúncios incompatíveis em vídeos M3U8 compatíveis.
title: Reempacotar anúncios incompatíveis usando o Serviço de reempacotamento criativo do Adobe
exl-id: 8c3e5baf-1941-4330-a4b7-61ed623dfd5e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Reempacotar anúncios incompatíveis usando o Serviço de reempacotamento criativo do Adobe {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Alguns anúncios de terceiros (ou criativos) não podem ser compilados no fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. A inserção de anúncios do Primetime e o TVSDK podem, opcionalmente, tentar reempacotar anúncios incompatíveis em vídeos M3U8 compatíveis.

Anúncios veiculados por vários terceiros, como um servidor de publicidade de uma agência, um parceiro de inventário ou uma rede de publicidade, geralmente são entregues em formatos incompatíveis, como o MP4 de download progressivo.

Quando o TVSDK encontra um anúncio incompatível pela primeira vez, o reprodutor ignora o anúncio e emite uma solicitação para o serviço de reempacotamento criativo (CRS), que faz parte do back-end de inserção de anúncio do Primetime, para reempacotar o anúncio em um formato compatível. O CRS tenta gerar representações M3U8 de taxa de vários bits do anúncio e armazena essas representações na Rede de entrega de conteúdo (CDN) do Primetime. Na próxima vez que o TVSDK receber uma resposta de anúncio que aponta para esse anúncio, o reprodutor usará a versão M3U8 compatível com HLS do CDN.

Para ativar esse recurso opcional, entre em contato com o representante da Adobe.

Para obter mais informações sobre CRS, consulte [Serviço de empacotamento criativo (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## Suporte a várias CDNs para entrega de anúncios CRS{#multiple-cdn-support-for-crs-ad-delivery}

Embora o cenário padrão do Serviço de reempacotamento criativo (CRS) seja usar uma Rede de dados de conteúdo (CDN), você pode implantar ativos de CRS em mais de uma CDN.

Você pode usar vários CDNs pelos seguintes motivos:

* Um requisito para aumentar a escala de eventos de exibição grandes.
* Um requisito para corresponder a origem CDN do ativo CRS à origem CDN do conteúdo principal.

Você pode transformar o URL padrão fornecido pelo CRS usando APIs de transformação de URL TVSDK.

Estas são as adições de API no TVSDK:

* `URLTransformer` Uma interface que descreve os métodos necessários para transformar os URLs de anúncios CRS solicitados pelo TVSDK. Os aplicativos podem implementar essa interface e fornecer implementações para os métodos necessários.

* `DefaultURLTransformer` A instância do transformador de URL padrão criada no TVSDK e que implementa o `URLTransformer` interface. Os aplicativos podem substituir essa classe ou adicionar um manipulador de transformação de URL de publicação. Esse manipulador é útil quando o aplicativo deseja fazer alterações na solicitação de URL após a transformação padrão ter sido aplicada.

* `NetworkConfiguration.setURLTransformer` Um método setter que é fornecido no `NetworkConfiguration` instância de metadados para definir o `URLTransformer` execução.

>[!IMPORTANT]
>
>As implementações do aplicativo devem verificar o `URLTransformerInputType` enumeração e transformar somente URLs do tipo `URLTransformerInputType.CRSCreative` para CRS.

A amostra de código a seguir mostra como seu aplicativo pode alterar o componente de host padrão para uma string diferente (por exemplo, `cdn.mycrsdomain.com`):

```java
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
DefaultURLTransformer urlTransformer = new DefaultURLTransformer(); 
urlTransformer.addPostURLTransformHandler(new DefaultURLTransformer.URLTransformHandler() { 
    @Override 
    public String call(String url, URLTransformerInputType type) { 
        if (type == URLTransformerInputType.CRSCreative) { 
            try { 
                return url.replaceAll(new java.net.URI(url).getHost(), "cdn.mycrsdomain.com"); 
            } catch (URISyntaxException e) { 
            } 
        } 
        return url; 
    } 
}); 
   
networkConfiguration.setURLTransformer(urlTransformer); 
   
// metadata is the Metadata instance set on a MediaResource instance. 
metadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(), networkConfiguration);
```
