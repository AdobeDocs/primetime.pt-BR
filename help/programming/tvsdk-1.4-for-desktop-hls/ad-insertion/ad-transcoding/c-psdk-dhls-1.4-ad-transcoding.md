---
description: Alguns anúncios de terceiros (ou criações) não podem ser compilados no fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. Como opção, a inserção de anúncios do Primetime e o TVSDK podem tentar reempacotar anúncios incompatíveis em vídeos compatíveis com o M3U8.
title: Reempacotar anúncios incompatíveis usando o Serviço de reempacotamento de criação do Adobe
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# Reempacote anúncios incompatíveis usando o Serviço de reempacotamento de criação do Adobe {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Alguns anúncios de terceiros (ou criações) não podem ser compilados no fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. Como opção, a inserção de anúncios do Primetime e o TVSDK podem tentar reempacotar anúncios incompatíveis em vídeos compatíveis com o M3U8.

Anúncios veiculados em vários terceiros, como uma agência e servidor, seu parceiro de inventário ou uma rede de anúncios, geralmente são entregues em formatos incompatíveis, como o download progressivo de MP4.

Quando o TVSDK encontra um anúncio incompatível pela primeira vez, o reprodutor ignora o anúncio e emite uma solicitação para o CRS (creative repackaging service), que faz parte do back-end de inserção de anúncio do Primetime, para reempacotar o anúncio em um formato compatível. O CRS tenta gerar representações M3U8 de taxa de bits múltipla do anúncio e armazena essas representações na Rede de entrega de conteúdo (CDN) do Primetime. Na próxima vez em que o TVSDK receber uma resposta de anúncio que aponte para esse anúncio, o reprodutor usará a versão M3U8 compatível com HLS da CDN.

Para ativar esse recurso opcional, entre em contato com o representante do Adobe.

Para obter mais informações sobre CRS, consulte [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## Suporte a várias CDNs para entrega de anúncios CRS {#multiple-cdn-support-for-crs-ad-delivery}

Embora o cenário padrão do Creative Repackaging Service (CRS) seja usar uma Rede de dados de conteúdo (CDN), é possível implantar ativos do CRS em mais de uma CDN.

Você pode usar vários CDNs pelos seguintes motivos:

* Um requisito para dimensionar para eventos de exibição grandes.
* Um requisito para corresponder a fonte CDN do ativo CRS à fonte CDN do conteúdo principal.

Você pode transformar o URL padrão fornecido pelo CRS usando APIs de Transformador de URL do TVSDK.

Estas são as adições da API no TVSDK:

* `URLTransformer` Uma interface que descreve os métodos necessários para transformar os URLs de anúncio do CRS solicitados pelo TVSDK. Os aplicativos podem implementar essa interface e fornecer implementações para os métodos necessários.

* `DefaultURLTransformer` A instância do transformador de URL padrão, criada no TVSDK e que implementa a  `URLTransformer` interface. Os aplicativos podem substituir essa classe ou adicionar um manipulador de transformação pós-URL. Esse manipulador é útil quando o aplicativo deseja fazer alterações na solicitação de URL após a aplicação da transformação padrão.

* `NetworkConfiguration.urlTransformer` Um método setter fornecido na instância de  `NetworkConfiguration` metadados para definir a  `URLTransformer` implementação.

>[!IMPORTANT]
>
>As implementações do aplicativo devem verificar a lista discriminada `URLTransformerInputType` e apenas transformar URLs do tipo `URLTransformerInputType.CRSCreative` para CRS.

A amostra de código a seguir mostra como seu aplicativo pode alterar o componente de host padrão para uma string diferente (por exemplo, `cdn.mycrsdomain.com`):

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
