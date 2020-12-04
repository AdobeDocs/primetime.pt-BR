---
description: Esta seção descreve os recursos disponíveis com diferentes versões do Flash Player e TVSDK.
seo-description: Esta seção descreve os recursos disponíveis com diferentes versões do Flash Player e TVSDK.
seo-title: Suporte ao cliente RBOP
title: Suporte ao cliente RBOP
uuid: d1d0f788-7bc1-488c-807e-be47f83725e9
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---


# Suporte ao cliente RBOP {#rbop-client-support}

Esta seção descreve os recursos disponíveis com diferentes versões do Flash Player e TVSDK.

**Despacho**  de erro - As plataformas TVSDK listadas abaixo despacham um erro de tempo de execução de DRM quando a resolução do conteúdo que está sendo reproduzido excede a resolução permitida para a configuração do dispositivo definida na política de DRM:

* Versões de Flash Player de 18 a 20
* Android - Versões
* iOS - Versões

>[!NOTE]
>
>* Todas as plataformas móveis e Flashes suportam o Despacho de erro, no entanto, somente os clientes TVSDK listados acima processam erros relacionados à RBOP.
>* Erros de cliente DRM [relacionados a RBOP](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):
   >    * **3371**  - Resolução malformada baseada em restrições de proteção de saída na licença.
   >    * **3372** - A resolução do conteúdo é maior que a resolução máxima especificada na restrição de proteção de saída. (Isso pode ocorrer se alguém tentar injetar conteúdo para outro dispositivo.)
   >    * **3373** - A resolução do conteúdo é maior do que a resolução especificada pela restrição de proteção de saída atualmente ativa. (Isso significa que teremos que fazer downgrade.)

>



**Redução**  automática - A técnica usada para fazer downscale varia de acordo com a versão da plataforma e do Flash Player:

* Versão 21 do Flash Player: Suporta RBOP com redução automática (comutação inteligente de taxa de bits)
* Firefox versão 38 e posterior no Windows (com CDM do Access): O Adobe baixa automaticamente um fluxo de taxa de bits mais alta para um menor (em vez de baixar um fluxo de nível mais baixo).

>[!NOTE]
>
>Essas plataformas reduzem automaticamente a escala de vídeo e exibem o conteúdo em uma resolução que seja inferior ou igual ao especificado pela política de DRM. Com esse recurso, o conteúdo sempre será reproduzido para o cliente, desde que haja um fluxo disponível que atenda às restrições da política de DRM.

**Proteção**  de saída herdada - os clientes que usam Flashes Player anteriores à versão 18 só podem lidar com restrições de OP herdadas. Os clientes com a versão 18 e posterior do Flash Player podem lidar com restrições de RBOP ou herdadas. Se você estiver configurando restrições de RBOP, também deverá definir restrições de OP herdadas para clientes mais antigos. Para clientes que suportam RBOP, as restrições de RBOP superam as restrições de OP herdadas.
