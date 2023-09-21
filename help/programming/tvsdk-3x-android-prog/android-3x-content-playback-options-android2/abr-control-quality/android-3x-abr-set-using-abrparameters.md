---
description: Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode construir um novo a qualquer momento.
title: Configurar taxas de bits adaptáveis usando ABRControlParameters
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Configurar taxas de bits adaptáveis usando ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}

Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode construir um novo a qualquer momento.

As seguintes condições se aplicam a `ABRControlParameters`:

* No momento da construção, você deve fornecer valores para todos os parâmetros.
* Após a construção, não é possível alterar valores individuais.
* Se os parâmetros especificados estiverem fora do intervalo permitido, uma variável `ArgumentError` é lançado.

1. Determine as taxas de bits inicial, mínima e máxima.
1. Determine a política ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Defina os valores do parâmetro ABR no `ABRControlParameters` e atribua os valores ao Reprodutor de mídia.

   ```
   public ABRControlParameters(int initialBitRate, 
     int minBitRate, 
     int maxBitRate, 
     ABRControlParameters.ABRPolicy abrPolicy, 
     int minTrickPlayBitRate, 
     int maxTrickPlayBitRate, 
     int maxTrickPlayBandwidthUsage, 
     int maxPlayoutRate);
   ```
