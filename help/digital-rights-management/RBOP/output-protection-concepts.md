---
description: Esta seção fornece uma visão geral conceitual da configuração, opções e significados associados à proteção de saída.
seo-description: Esta seção fornece uma visão geral conceitual da configuração, opções e significados associados à proteção de saída.
seo-title: Conceitos de RBOP
title: Conceitos de RBOP
uuid: fc19c3c9-39a1-4b62-b763-101e5454a01f
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Conceitos de RBOP {#rbop-concepts}

Esta seção fornece uma visão geral conceitual da configuração, opções e significados associados à proteção de saída.

Especifique os requisitos de proteção de saída com base em resolução em uma estrutura JSON hierárquica. *Os requisitos de saída são baseados em pixels.*

No nível mais alto da especificação JSON, é possível definir a resolução máxima de pixels e as restrições de pixel para resoluções especificadas:

* `maxPixel` - A resolução máxima de pixel define a resolução máxima para a qual ocorrerá a descriptografia.
* `pixelConstraints` - As restrições de pixel definem requisitos de saída que devem ser aplicados para uma resolução especificada.

Você associa requisitos de saída a restrições específicas de pixel. Os tipos de requisitos que podem ser associados a uma determinada restrição de pixel incluem restrições para conexões digitais, analógicas e ao ar livre (OTA).

**Saída digital**

O requisito de saída digital pode especificar opções restritivas, como &quot;a proteção de saída digital é obrigatória&quot; ou &quot;a reprodução não é permitida&quot;. Os requisitos de saída também podem especificar opções menos restritivas, como &quot;nenhuma proteção deve ser aplicada&quot; ou &quot;a proteção digital deve ser usada se disponível&quot;.

**Saída analógica**

As conexões de saída analógica são mais simples que a saída digital; Consistem num único requisito de produção.
