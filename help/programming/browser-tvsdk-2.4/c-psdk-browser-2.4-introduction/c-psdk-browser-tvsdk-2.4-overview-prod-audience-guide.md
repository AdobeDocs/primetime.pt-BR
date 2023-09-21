---
description: Este guia fornece informações sobre como desenvolver aplicativos de reprodutor de vídeo usando o TVSDK do navegador.
title: Visão geral e público-alvo do produto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Visão geral e público-alvo do produto{#product-overview-and-audience}

Este guia fornece informações sobre como desenvolver aplicativos de reprodutor de vídeo usando o TVSDK do navegador.

## Visão geral do produto {#section_1C66E736CEFD4246B7C7C99AADD48118}

O Adobe Primetime Software Development Kit (TVSDK do navegador) é um kit de ferramentas que permite adicionar funcionalidade avançada de reprodução de vídeo, proteção de conteúdo e publicidade aos aplicativos de player de vídeo baseados em navegador. O TVSDK do navegador fornece APIs JavaScript para criar aplicativos de vídeo baseados em navegador e inclui suporte para reprodução nos seguintes modos:

* Somente HTML5
* HTML5 com fallback de flash automático
* Flash sempre

Esta versão inclui as APIs TVSDK do navegador e uma implementação de referência de amostra.

### Estrutura da interface

Para ajudar a acelerar o desenvolvimento da interface do usuário para aplicativos de player de vídeo baseados em JavaScript para navegadores, o TVSDK do navegador inclui uma estrutura de interface do usuário que consiste em APIs para:

* Incluir controles padrão da interface do usuário, como reproduzir/pausar, volume etc.
* Adicione (ou remova) facilmente controles avançados de reprodução da interface sem manipular diretamente a estrutura DOM
* Configure facilmente o comportamento dos controles de interface do usuário associados
* Criar controles de interface do usuário personalizados
* Controlar a interface do usuário do player com base nos requisitos

Para obter mais informações sobre as APIs para a estrutura da interface, consulte [Estrutura de interface do usuário para TVSDK do navegador 2.4](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html).

## Público {#section_DFC9DECC2E30426DBBDDEA4E288E666C}

Este guia pressupõe que você entende como desenvolver aplicativos e players de vídeo usando JavaScript. Você pode implementar um reprodutor de vídeo e incorporar recursos TVSDK do navegador.
