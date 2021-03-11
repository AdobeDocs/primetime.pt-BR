---
description: Esta seção fornece uma visão geral conceitual da configuração, opções e significados associados à proteção de saída.
title: Conceitos de RBOP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# Conceitos de RBOP {#rbop-concepts}

Esta seção fornece uma visão geral conceitual da configuração, opções e significados associados à proteção de saída.

Especifique seus requisitos de proteção de saída com base em resolução em uma estrutura JSON hierárquica. *Os requisitos de saída são baseados em pixels.*

No nível mais alto da especificação JSON, você pode definir a resolução máxima de pixels e as restrições de pixel para resoluções especificadas:

* `maxPixel` - A resolução máxima de pixel define a resolução máxima para a qual ocorrerá a descriptografia.
* `pixelConstraints` - As restrições de pixels definem os requisitos de saída que devem ser aplicados para uma resolução especificada.

Você associa requisitos de saída a restrições específicas de pixel. Os tipos de requisitos que você pode associar a uma determinada restrição de pixel incluem restrições para conexões digitais, analógicas e ao ar livre (OTA).

**Saída digital**

O requisito de saída digital pode especificar opções restritivas, como &quot;é necessária proteção de saída digital&quot; ou &quot;a reprodução não é permitida&quot;. Os requisitos de saída também podem especificar opções menos restritivas, como &quot;não deve ser aplicada qualquer proteção&quot; ou &quot;a proteção digital deve ser utilizada se estiver disponível&quot;.

**Saída analógica**

As ligações de saída analógica são mais simples do que a saída digital; Consistem num único requisito de produção.
