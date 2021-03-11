---
description: Este guia fornece informações sobre como desenvolver aplicativos do reprodutor de vídeo usando o Browser TVSDK.
title: Visão geral e público-alvo do produto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Visão geral do produto e público-alvo{#product-overview-and-audience}

Este guia fornece informações sobre como desenvolver aplicativos do reprodutor de vídeo usando o Browser TVSDK.

## Visão geral do produto {#section_1C66E736CEFD4246B7C7C99AADD48118}

O Adobe Primetime Software Development Kit (Browser TVSDK) é um kit de ferramentas que permite adicionar funcionalidades avançadas de reprodução de vídeo, proteção de conteúdo e publicidade aos aplicativos de player de vídeo baseados em navegador. O TVSDK do navegador fornece APIs de JavaScript para criar aplicativos de vídeo baseados em navegador e inclui o suporte a reprodução nos seguintes modos:

* Somente HTML5
* HTML5 com fallback de flash automático
* Flash always

Esta versão inclui as APIs TVSDK do navegador e uma amostra da implementação de referência.

### Estrutura da interface do usuário

Para ajudar a acelerar o desenvolvimento da interface do usuário para aplicativos de player de vídeo baseados em JavaScript para navegadores, o TVSDK do navegador inclui uma estrutura de interface do usuário que consiste em APIs para:

* Incluir controles padrão da interface do usuário, como reproduzir/pausar, volume e assim por diante
* Adicione (ou remova) com facilidade controles da interface do usuário de reprodução avançada sem manipular a estrutura do DOM diretamente
* Configure facilmente o comportamento dos controles da interface do usuário associados
* Criar controles de interface personalizados
* Pular a interface do usuário do reprodutor com base nos requisitos

Para obter mais informações sobre as APIs da estrutura da interface do usuário, consulte [Estrutura da interface do usuário para Browser TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html).

## Público-alvo {#section_DFC9DECC2E30426DBBDDEA4E288E666C}

Este guia pressupõe que você entenda como desenvolver aplicativos e players de vídeo usando JavaScript. Você pode implementar um reprodutor de vídeo e incorporar os recursos TVSDK do navegador.