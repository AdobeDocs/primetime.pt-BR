---
description: Esta seção descreve os recursos disponíveis com diferentes versões do Flash Player e TVSDK.
title: Suporte ao cliente RBOP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Suporte a Cliente RBOP {#rbop-client-support}

Esta seção descreve os recursos disponíveis com diferentes versões do Flash Player e TVSDK.

**Despacho de erro**  - As plataformas TVSDK listadas abaixo despacham um erro de tempo de execução de DRM quando a resolução do conteúdo que está sendo reproduzido excede a resolução permitida para a configuração do dispositivo definida na política de DRM:

* Versões 18 a 20 do Flash Player
* Android - Versões
* iOS - Versões

>[!NOTE]
>
>* Todas as plataformas móveis e Flash suportam o Despacho de erro, no entanto, somente os clientes TVSDK listados acima processam erros relacionados a RBOP.
>* [Erros de cliente DRM relacionados a RBOP](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):
   >    * **3371**  - Resolução malformada com base nas restrições de proteção de saída na licença.
   >    * **3372**  - A resolução do conteúdo é maior que a resolução máxima especificada na restrição de proteção de saída. (Isso pode ocorrer se alguém tentar injetar conteúdo destinado a outro dispositivo.)
   >    * **3373**  - A resolução do conteúdo é maior do que a resolução especificada pela restrição de proteção de saída atualmente ativa. (Isso significa que teremos que fazer o downgrade.)

>



**Redução automática**  - A técnica usada para fazer o downscale varia de acordo com a versão da plataforma e do Flash Player:

* Versão 21 do Flash Player: Suporta RBOP com Descarga Automática (switching inteligente de taxa de bits)
* Firefox versão 38 e posterior no Windows (com CDM de acesso): O Adobe baixa automaticamente um fluxo de taxa de bits mais alto para um menor (em vez de baixar um fluxo de nível mais baixo).

>[!NOTE]
>
>Essas plataformas reduzem automaticamente o vídeo e exibem o conteúdo em uma resolução que é menor ou igual ao especificado pela política de DRM. Com esse recurso, o conteúdo sempre será reproduzido para o cliente, desde que haja um fluxo disponível que atenda às restrições da política de DRM.

**Proteção de saída herdada**  - os clientes que usam Flashes Player anteriores à versão 18 só podem lidar com restrições de OP herdadas. Clientes com Flash Player versão 18 e posterior podem lidar com restrições de RBOP ou herdadas. Se você estiver definindo restrições de RBOP, também deverá definir restrições de OP herdadas para clientes mais antigos. Para clientes que oferecem suporte para RBOP, as restrições de RBOP superam as restrições de OP herdadas.
