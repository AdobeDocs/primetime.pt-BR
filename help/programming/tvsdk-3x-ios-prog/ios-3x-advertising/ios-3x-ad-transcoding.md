---
description: Alguns anúncios de terceiros (ou criativos) não podem ser compilados no fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. A inserção de anúncios do Primetime e o TVSDK podem, opcionalmente, tentar reempacotar anúncios incompatíveis em vídeos M3U8 compatíveis.
title: Reempacotar anúncios incompatíveis usando o Serviço de reempacotamento criativo do Adobe
exl-id: 86a8bd94-4de0-4aba-b6ee-4e0e1ee864c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Reempacotar anúncios incompatíveis usando o Serviço de reempacotamento criativo do Adobe {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Alguns anúncios de terceiros (ou criativos) não podem ser compilados no fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. A inserção de anúncios do Primetime e o TVSDK podem, opcionalmente, tentar reempacotar anúncios incompatíveis em vídeos M3U8 compatíveis.

Anúncios veiculados por vários terceiros, como um servidor de publicidade de uma agência, um parceiro de inventário ou uma rede de publicidade, geralmente são entregues em formatos incompatíveis, como o MP4 de download progressivo.

Quando o TVSDK encontra um anúncio incompatível pela primeira vez, o reprodutor ignora o anúncio e emite uma solicitação para o serviço de reempacotamento criativo (CRS), que faz parte do back-end de inserção de anúncio do Primetime, para reempacotar o anúncio em um formato compatível. O CRS tenta gerar representações M3U8 de taxa de vários bits do anúncio e armazena essas representações na Rede de entrega de conteúdo (CDN) do Primetime. Na próxima vez que o TVSDK receber uma resposta de anúncio que aponta para esse anúncio, o reprodutor usará a versão M3U8 compatível com HLS do CDN.

Para ativar esse recurso opcional, entre em contato com o representante da Adobe.

## Suporte a várias CDNs para entrega de anúncios CRS {#section_900FDDA5454143718F1EB4C9732C8E1C}

Embora o cenário padrão do Serviço de reempacotamento criativo (CRS) seja usar uma Rede de dados de conteúdo (CDN), você pode implantar ativos de CRS em mais de uma CDN.

Você pode usar vários CDNs pelos seguintes motivos:

* Um requisito para aumentar a escala de eventos de exibição grandes.
* Um requisito para corresponder a origem CDN do ativo CRS à origem CDN do conteúdo principal.

Você pode transformar o URL padrão fornecido pelo CRS usando APIs de transformação de URL TVSDK.

Estas são as adições de API no TVSDK:

* `PTURLTransformer` Um protocolo que descreve os métodos necessários para transformar os URLs de anúncios CRS solicitados pelo TVSDK. Os aplicativos podem implementar esse protocolo e fornecer implementações para os métodos necessários.

* `PTDefaultURLTransformer` A instância do transformador de URL padrão criada no TVSDK e que implementa o `PTURLTransformer` protocolo. Os aplicativos podem substituir essa classe ou adicionar um manipulador de transformação de URL de publicação. Esse manipulador é útil quando o aplicativo deseja fazer alterações na solicitação de URL após a transformação padrão ter sido aplicada.

* `PTNetworkConfiguration setURLTransformer:defaultTransformer` Um método setter que é fornecido no `PTNetworkConfiguration` instância de metadados para definir o `PTURLTransformer` execução.

>[!IMPORTANT]
>
>As implementações do aplicativo devem verificar o `PTURLTransformerInputType` enumeração e transformar somente URLs do tipo `PTURLTransformerInputTypeCRSCreative` para CRS.

A amostra de código a seguir mostra como seu aplicativo pode alterar o componente de host padrão para uma string diferente (por exemplo, `cdn.mycrsdomain.com`):

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
