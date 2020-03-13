---
description: Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode criar um novo a qualquer momento.
seo-description: Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode criar um novo a qualquer momento.
seo-title: Configure as taxas de bits adaptáveis usando ABRControlParameters
title: Configure as taxas de bits adaptáveis usando ABRControlParameters
uuid: 283ccd3d-535b-43ca-8ca5-82d12df31798
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Configure as taxas de bits adaptáveis usando ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}

Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode criar um novo a qualquer momento.

As seguintes condições aplicam-se a `ABRControlParameters`:

* No momento da construção, você deve fornecer valores para todos os parâmetros.
* Após a construção, não é possível alterar valores individuais.
* Se os parâmetros especificados estiverem fora do intervalo permitido, um `ArgumentError` será lançado.

1. Determine as taxas de bits inicial, mínima e máxima.
1. Determine a política ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Defina os valores dos parâmetros ABR no `ABRControlParameters` construtor e atribua os valores ao Media Player.

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
