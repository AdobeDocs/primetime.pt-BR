---
title: Perguntas frequentes
description: Perguntas frequentes
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Perguntas frequentes {#faq}

* Com que frequência ocorrem alterações na ECI?
   * Sempre que um novo cliente DRM de Adobe é lançado, um registro de dispositivo ECI é adicionado.

* Qual é o tamanho dos arquivos ECI?
   * Normalmente, têm menos de 1 Kilobyte por registro de dispositivo.

* O que acontece se o servidor não tiver um registro de dispositivo ECI?
   * Essa classe específica de clientes não poderá se individualizar em relação ao On Premises Individualization Server e os erros serão registrados nos arquivos de log.

* O que acontece se as CRLs de um servidor expirarem?
   * O servidor deixará de funcionar corretamente e os erros serão registrados nos arquivos de log.
