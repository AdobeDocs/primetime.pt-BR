---
description: Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode construir um novo a qualquer momento.
title: Configurar taxas de bits adaptáveis usando ABRControlParameters
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Configure as taxas de bits adaptáveis usando ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}

Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode construir um novo a qualquer momento.

As seguintes condições se aplicam a `ABRControlParameters`:

* No momento da construção, você deve fornecer valores para todos os parâmetros.
* Após a construção, não é possível alterar valores individuais.
* Se os parâmetros especificados estiverem fora do intervalo permitido, um `ArgumentError` será lançado.

1. Determine as taxas de bits inicial, mínima e máxima.
1. Determine a política ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Defina os valores dos parâmetros ABR no construtor `ABRControlParameters` e atribua os valores ao Media Player.

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

