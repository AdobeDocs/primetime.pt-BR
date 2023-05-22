---
description: Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode construir um novo a qualquer momento.
title: Configurar taxas de bits adaptáveis usando ABRControlParameters
exl-id: 787e962c-371f-4ac8-ae13-8b38a230593f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Configurar taxas de bits adaptáveis usando ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}

Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode construir um novo a qualquer momento.

As seguintes condições se aplicam a `ABRControlParameters`:

* Você deve fornecer valores para todos os parâmetros no momento da construção.
* Não é possível alterar valores individuais após o tempo de construção.
* Se os parâmetros especificados estiverem fora do intervalo permitido, uma variável `ArgumentError` é lançado.

1. Decida sobre as taxas de bits inicial, mínima e máxima.
1. Determine a política ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Defina os valores do parâmetro ABR no `ABRControlParameters` e atribua-os ao reprodutor de mídia.

   ```java
   public ABRControlParameters(int initialBitRate, 
     int minBitRate, 
     int maxBitRate, 
     ABRControlParameters.ABRPolicy abrPolicy, 
     int minTrickPlayBitRate, 
     int maxTrickPlayBitRate, 
     int maxTrickPlayBandwidthUsage, 
     int maxPlayoutRate);
   ```
