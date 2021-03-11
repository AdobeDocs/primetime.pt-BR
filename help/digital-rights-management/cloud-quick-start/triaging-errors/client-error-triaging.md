---
description: Ocasionalmente, haverá momentos em que o conteúdo não poderá ser reproduzido. Qualquer número de situações pode causar isso, incluindo erros na pilha de rede do navegador, na camada de transporte, no sistema operacional, no tempo de execução do Flash Player ou no sistema de DRM do Primetime.
title: Visão geral dos erros de teste
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Teste de erros {#triaging-errors}

Ocasionalmente, haverá momentos em que o conteúdo não poderá ser reproduzido. Qualquer número de situações pode causar isso, incluindo erros na pilha de rede do navegador, na camada de transporte, no sistema operacional, no tempo de execução do Flash Player ou no sistema de DRM do Primetime.

A primeira etapa de diagnóstico é determinar se o problema se manifesta sem a criptografia de DRM introduzida na equação. Tente empacotar o conteúdo, mas instrua o empacotador a não criptografar o conteúdo. Se o problema ainda existir, é provável que haja um problema na codificação ou embalagem do conteúdo ou em algum lugar na infraestrutura de rede. Se o problema desaparecer quando o conteúdo for empacotado sem criptografia, a falha da reprodução provavelmente se deve a um problema de DRM e você deve participar do armazenamento de dados do cliente/servidor.

O DRM do Primetime (fora do DRM da Primetime Cloud) está no mercado há vários anos. Dessa forma, há uma grande variedade de informações fornecidas pela comunidade sobre solução de problemas e configuração do DRM do Primetime. O Adobe forneceu um fórum para usuários do Primetime DRM (antigo Adobe Access) para agregar e compartilhar problemas e resoluções. Para determinar se seu problema foi discutido anteriormente, verifique: [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## Acionamento do erro do cliente {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

Se o conteúdo não for reproduzido, examine o painel do lado direito dos Players de vídeo de amostra, que registrará qualquer `DRMErrorEvent` que ocorrer. Se houver um evento de erro, ele estará correlacionado a um dos Erros de tempo de execução do Flash Player :

* [Referência](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages) de mensagem de erro do cliente DRM; ou
* [Erros](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html)  de tempo de execução do Flash AS3 (problemas de DRM começam em 3300)

