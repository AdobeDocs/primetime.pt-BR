---
description: Ocasionalmente, haverá momentos em que o conteúdo não poderá ser reproduzido. Qualquer número de situações pode causar isso, incluindo erros na pilha de rede do navegador, na camada de transporte, no sistema operacional, no tempo de execução do Flash Player ou no sistema DRM do Primetime.
title: Visão geral de erros de triagem
exl-id: fe94d0a4-4f3c-4b0e-b830-a7a83bac1e85
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Erros de triagem {#triaging-errors}

Ocasionalmente, haverá momentos em que o conteúdo não poderá ser reproduzido. Qualquer número de situações pode causar isso, incluindo erros na pilha de rede do navegador, na camada de transporte, no sistema operacional, no tempo de execução do Flash Player ou no sistema DRM do Primetime.

A primeira etapa de diagnóstico é determinar se o problema se manifesta sem a criptografia DRM introduzida na equação. Tente empacotar o conteúdo, mas instrua o empacotador a não criptografar o conteúdo. Se o problema ainda existir, ele provavelmente se trata de um problema de codificação ou empacotamento do conteúdo, ou de algum lugar na infraestrutura de rede. Se o problema desaparecer quando o conteúdo for empacotado sem criptografia, a falha na reprodução provavelmente se deve a um problema de DRM, e você deve participar da triagem cliente/servidor.

O Primetime DRM (fora do Primetime Cloud DRM) está no mercado há vários anos. Dessa forma, há uma grande variedade de informações de origem comunitária sobre solução de problemas e configuração do Primetime DRM. O Adobe forneceu um fórum para que usuários do Primetime DRM (anteriormente chamado de Adobe Access) agregassem e compartilhassem problemas e resoluções. Para determinar se o problema foi discutido anteriormente, verifique: [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## Triagem de erros do cliente {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

Se o conteúdo não for reproduzido, examine o painel do lado direito dos Players de vídeo de exemplo, que registrarão qualquer `DRMErrorEvent` que ocorre. Se houver um evento de erro, ele se correlacionará com um dos Erros de tempo de execução do Flash Player:

* [Referência de mensagem de erro de cliente DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages); ou
* [Erros de Tempo de Execução do Flash AS3](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) (Problemas de DRM começam em 3300)
