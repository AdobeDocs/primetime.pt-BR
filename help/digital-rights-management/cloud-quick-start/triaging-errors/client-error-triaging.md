---
description: Ocasionalmente, haverá momentos em que o conteúdo não poderá ser reproduzido. Qualquer número de situações pode causar isso, incluindo erros na pilha de rede do navegador, camada de transporte, sistema operacional, tempo de execução do Flash Player ou sistema DRM Primetime.
seo-description: Ocasionalmente, haverá momentos em que o conteúdo não poderá ser reproduzido. Qualquer número de situações pode causar isso, incluindo erros na pilha de rede do navegador, camada de transporte, sistema operacional, tempo de execução do Flash Player ou sistema DRM Primetime.
seo-title: Visão geral dos erros de teste
title: Visão geral dos erros de teste
uuid: 44b4ab0e-5f08-44b0-bcb5-a869f6add69b
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Erros de teste {#triaging-errors}

Ocasionalmente, haverá momentos em que o conteúdo não poderá ser reproduzido. Qualquer número de situações pode causar isso, incluindo erros na pilha de rede do navegador, camada de transporte, sistema operacional, tempo de execução do Flash Player ou sistema DRM Primetime.

A primeira etapa de diagnóstico é determinar se o problema se manifesta sem a criptografia DRM introduzida na equação. Tente empacotar o conteúdo, mas instrua o empacotador a não criptografar o conteúdo. Se o problema ainda existir, é provável que haja um problema na codificação ou empacotamento do conteúdo, ou em algum lugar na infraestrutura de rede. Se o problema desaparecer quando o conteúdo for empacotado sem criptografia, a falha na reprodução provavelmente se deve a um problema de DRM e você deve se envolver na triagem de cliente/servidor.

O DRM Primetime (fora do DRM da Primetime Cloud) está no mercado há vários anos. Dessa forma, há uma grande variedade de informações de origem comunitária sobre solução de problemas e configuração do DRM Primetime. A Adobe forneceu um fórum para usuários do Primetime DRM (anteriormente chamado de Adobe Access) para agregar e compartilhar problemas e resoluções. Para determinar se seu problema foi discutido anteriormente, verifique: [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## Teste de erro do cliente {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

Se o conteúdo não for reproduzido, examine o painel do lado direito dos Players de vídeo de amostra, que registrarão qualquer `DRMErrorEvent` item que ocorrer. Se houver um evento de erro, ele se correlacionará a um dos erros de tempo de execução do Flash Player:

* [Referência](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)de mensagem de erro do cliente DRM; ou
* [Erros](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) do AS3 Flash Runtime (problemas do DRM iniciam em 3300)

