---
description: Este guia fornece informações sobre como desenvolver aplicativos de player de vídeo usando TVSDK para Android, que é implementado em Java.
title: Visão geral do produto, público-alvo e este guia
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Visão geral do produto, público-alvo e este guia {#product-overview-audience-and-this-guide}

Este guia fornece informações sobre como desenvolver aplicativos de player de vídeo usando TVSDK para Android, que é implementado em Java.

<!--<a id="section_FC24E86A2E6442B8A3769160769BBDFA"></a>-->

* Para obter uma lista dos recursos compatíveis com TVSDK, consulte [Recursos do Primetime TVSDK](../../tvsdk-2.7-for-android/overview-prod-audience-guide/c-psdk-android-2.7-overview-of-the-player.md).
* Para obter os requisitos específicos de hardware e software para usar o TVSDK, consulte [Requisitos](../../tvsdk-2.7-for-android/c-psdk-android-2.7-requirements.md).
* Para obter uma lista de APIs disponíveis, consulte [TVSDK Android APIs](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/).

## Visão geral do produto {#section_9664959F25C948878F2F7EF3D360CA95}

O TVSDK inclui descrições de API e amostras de código para ajudar você a integrar recursos avançados de funcionalidade de vídeo, proteção de conteúdo e publicidade ao seu player. Você usa o Java para criar uma interface de usuário do reprodutor de vídeo. O TVSDK ajuda a conectar essa interface de usuário ao seu reprodutor de mídia. Isso permite reproduzir vídeos e anúncios com base em manifestos de mídia. Você também pode usar o TVSDK para recuperar informações sobre o vídeo, lidar com a segurança e controlar e monitorar a reprodução.

## Público-alvo {#section_527860B373734D3BA89FCF5EC1F6DC37}

Este guia pressupõe que você entenda como desenvolver aplicativos e reprodutores de vídeo usando o Java. Você implementa a interface do usuário do reprodutor de vídeo no Java e incorpora os recursos TVSDK necessários.

## Sobre este guia {#section_9A5B2FC506B34B5DB71CA827B307A4D0}

Este guia fornece informações que permitem incorporar recursos do TVSDK em um reprodutor de vídeo usando Java em dispositivos Android.

## Notação de namespace neste guia {#section_8B866054E9ED4B5F99DCA7A681404632}

>[!TIP]
>
>O prefixo [!DNL com.adobe.mediacore] do namespace da API TVSDK geralmente é omitido por motivos de brevidade.
>
>Muitos elementos da API são referenciados sem seu designador de classe pai, se o contexto for claro.