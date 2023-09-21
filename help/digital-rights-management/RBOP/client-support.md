---
description: Esta seção descreve os recursos disponíveis com diferentes versões do Flash Player e TVSDK.
title: Suporte a cliente RBOP
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Suporte a cliente RBOP {#rbop-client-support}

Esta seção descreve os recursos disponíveis com diferentes versões do Flash Player e TVSDK.

**Despacho de erro** - As plataformas TVSDK listadas abaixo despacham um Erro de Tempo de Execução DRM quando a resolução do conteúdo que está sendo reproduzido excede a resolução permitida para a configuração do dispositivo definida na política DRM:

* Flash Player versões 18 a 20
* Android - Versões
* iOS - Versões

>[!NOTE]
>
>* Todas as plataformas móveis e de Flash suportam o Despacho de Erros, no entanto, apenas os clientes TVSDK listados acima processam erros relacionados a RBOP.
>* Relacionados com RBOP [Erros de cliente DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):
>    * **3371** - Resolução malformada com base em restrições de proteção de saída na licença.
>    * **3372** - A resolução do conteúdo é maior que a resolução máxima especificada na restrição de proteção de saída. (Isso pode ocorrer se alguém tentar injetar conteúdo destinado a outro dispositivo.)
>    * **3373** - A resolução do conteúdo é maior do que a resolução especificada pela restrição de proteção de saída atualmente ativa. (Isso significa que teremos que fazer downgrade.)
>

**Downscaling automático** - A técnica usada para fazer downscale varia de acordo com a plataforma e a versão do Flash Player:

* Flash Player versão 21: suporta RBOP com redução automática (switching inteligente da taxa de bits)
* Firefox versão 38 e posterior no Windows (com Access CDM): o Adobe faz o downgrade automático de um fluxo de taxa de bits mais alto para um mais baixo (em vez de baixar um fluxo de nível mais baixo).

>[!NOTE]
>
>Essas plataformas diminuem automaticamente o tamanho do vídeo e exibem o conteúdo em uma resolução menor ou igual à especificada pela política de DRM. Com esse recurso, o conteúdo sempre será reproduzido de volta ao cliente, desde que haja um fluxo disponível que atenda às restrições da política de DRM.

**Proteção de saída herdada** - Os clientes que usam Flashes Player anteriores à versão 18 só podem lidar com restrições de OP herdadas. Os clientes com Flash Player versão 18 e posterior podem lidar com restrições herdadas ou RBOP. Se você estiver definindo restrições de RBOP, também deverá definir restrições de OP herdadas para clientes mais antigos. Para clientes que oferecem suporte a RBOP, as restrições de RBOP superam as restrições de OP herdadas.
