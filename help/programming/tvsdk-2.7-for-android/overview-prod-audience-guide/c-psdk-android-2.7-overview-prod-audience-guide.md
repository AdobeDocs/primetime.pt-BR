---
description: Este guia fornece informações sobre como desenvolver aplicativos de reprodutor de vídeo usando o TVSDK para Android, que é implementado em Java.
title: Visão geral do produto, público-alvo e este guia
exl-id: 3dfef60a-5547-494b-9bbe-74eb0440ec92
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Visão geral do produto, público-alvo e este guia {#product-overview-audience-and-this-guide}

Este guia fornece informações sobre como desenvolver aplicativos de reprodutor de vídeo usando o TVSDK para Android, que é implementado em Java.

<!--<a id="section_FC24E86A2E6442B8A3769160769BBDFA"></a>-->

* Para obter uma lista dos recursos compatíveis com o TVSDK, consulte [Recursos do Primetime TVSDK](../../tvsdk-2.7-for-android/overview-prod-audience-guide/c-psdk-android-2.7-overview-of-the-player.md).
* Para obter os requisitos específicos de hardware e software para usar o TVSDK, consulte [Requisitos](../../tvsdk-2.7-for-android/c-psdk-android-2.7-requirements.md).
* Para obter uma lista de APIs disponíveis, consulte [APIs do Android TVSDK](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/).

## Visão geral do produto {#section_9664959F25C948878F2F7EF3D360CA95}

O TVSDK inclui descrições de API e amostras de código para ajudar você a integrar recursos avançados de funcionalidade de vídeo, proteção de conteúdo e publicidade ao seu reprodutor. Use o Java para criar uma interface de usuário do reprodutor de vídeo. O TVSDK ajuda a conectar essa interface do usuário ao seu reprodutor de mídia. Isso permite reproduzir vídeos e anúncios com base em manifestos de mídia. Você também pode usar o TVSDK para recuperar informações sobre o vídeo, manipular a segurança, controlar e monitorar a reprodução.

## Público {#section_527860B373734D3BA89FCF5EC1F6DC37}

Este guia pressupõe que você entende como desenvolver aplicativos e players de vídeo usando Java. Você implementa a interface do usuário do player de vídeo em Java e incorpora os recursos TVSDK necessários.

## Sobre este guia {#section_9A5B2FC506B34B5DB71CA827B307A4D0}

Este guia fornece informações que permitem incorporar recursos do TVSDK em um reprodutor de vídeo usando Java em dispositivos Android.

## Notação de namespace neste guia {#section_8B866054E9ED4B5F99DCA7A681404632}

>[!TIP]
>
>O prefixo do namespace da API TVSDK [!DNL com.adobe.mediacore] O geralmente é omitido por motivos de brevidade.
>
>Muitos elementos da API são referenciados sem o designador de classe principal se o contexto for claro.
