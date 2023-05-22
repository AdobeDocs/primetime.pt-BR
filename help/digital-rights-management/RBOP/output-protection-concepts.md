---
description: Esta seção fornece uma visão geral conceitual da configuração, das opções e dos significados associados à proteção de saída.
title: Conceitos de RBOP
exl-id: 5b9de292-e060-467d-beca-5f428e45ed69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# Conceitos de RBOP {#rbop-concepts}

Esta seção fornece uma visão geral conceitual da configuração, das opções e dos significados associados à proteção de saída.

Você especifica os requisitos de proteção de saída com base em resolução em uma estrutura JSON hierárquica. *Os requisitos de saída são baseados em pixels.*

No nível mais alto da especificação JSON, você pode definir a resolução máxima de pixels e as restrições de pixels para as resoluções especificadas:

* `maxPixel` - A resolução máxima de pixels define a resolução máxima para a qual ocorrerá a descriptografia.
* `pixelConstraints` - As restrições de pixels definem os requisitos de saída que devem ser aplicados para uma resolução especificada.

Você associa requisitos de saída a restrições de pixel específicas. Os tipos de requisitos que você pode associar a uma determinada restrição de pixel incluem restrições para conexões digitais, analógicas e OTA (Over-the-Air).

**Saída digital**

O requisito de saída digital pode especificar opções restritivas, como &quot;é necessária proteção de saída digital&quot; ou &quot;a reprodução não é permitida&quot;. Os requisitos de saída também podem especificar opções menos restritivas, como &quot;nenhuma proteção deve ser aplicada&quot; ou &quot;proteção digital deve ser usada se estiver disponível&quot;.

**Saída analógica**

As conexões de saída analógica são mais simples do que a saída digital; elas consistem em um único requisito de saída.
