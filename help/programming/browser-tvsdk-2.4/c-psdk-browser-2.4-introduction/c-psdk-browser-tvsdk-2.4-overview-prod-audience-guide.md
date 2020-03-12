---
description: Este guia fornece informações sobre como desenvolver aplicativos de player de vídeo usando o Browser TVSDK.
seo-description: Este guia fornece informações sobre como desenvolver aplicativos de player de vídeo usando o Browser TVSDK.
seo-title: Visão geral do produto e público-alvo
title: Visão geral do produto e público-alvo
uuid: 902baabf-5e85-4d9c-8b5a-70ec0842e1bc
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Visão geral do produto e público-alvo{#product-overview-and-audience}

Este guia fornece informações sobre como desenvolver aplicativos de player de vídeo usando o Browser TVSDK.

## Visão geral do produto {#section_1C66E736CEFD4246B7C7C99AADD48118}

O Adobe Primetime Software Development Kit (TVSDK do navegador) é um kit de ferramentas que permite adicionar funcionalidade avançada de reprodução de vídeo, proteção de conteúdo e publicidade aos aplicativos de player de vídeo baseados em navegador. O TVSDK do navegador fornece APIs JavaScript para criar aplicativos de vídeo baseados em navegador e inclui suporte para reprodução nos seguintes modos:

* Somente HTML5
* HTML5 com fallback de flash automático
* Flash sempre

Esta versão inclui as APIs TVSDK do navegador e uma implementação de referência de amostra.

### Estrutura da interface do usuário

Para ajudar a acelerar o desenvolvimento da interface para aplicativos de player de vídeo baseados em JavaScript para navegadores, o TVSDK do navegador inclui uma estrutura de interface que consiste em APIs para:

* Incluir controles padrão da interface do usuário, como reproduzir/pausar, volume e assim por diante
* Adicione (ou remova) facilmente controles de interface de reprodução avançada sem manipular a estrutura DOM diretamente
* Configure facilmente o comportamento para os controles de interface associados
* Criar controles personalizados da interface do usuário
* Pular a interface do usuário do player com base nos requisitos

Para obter mais informações sobre as APIs para a estrutura da interface do usuário, consulte [UI Framework for Browser TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html).

## Público {#section_DFC9DECC2E30426DBBDDEA4E288E666C}

Este guia supõe que você saiba como desenvolver aplicativos e players de vídeo usando JavaScript. Você pode implementar um player de vídeo e incorporar recursos TVSDK do navegador.