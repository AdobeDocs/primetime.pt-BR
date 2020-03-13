---
description: Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode criar um novo a qualquer momento.
seo-description: Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode criar um novo a qualquer momento.
seo-title: Configure as taxas de bits adaptáveis usando ABRControlParameters
title: Configure as taxas de bits adaptáveis usando ABRControlParameters
uuid: c877c5cc-ad72-46dc-afc4-d41ee097a9a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Configure as taxas de bits adaptáveis usando ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}

Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode criar um novo a qualquer momento.

As seguintes condições aplicam-se a `ABRControlParameters`:

* Você deve fornecer valores para todos os parâmetros no momento da construção.
* Não é possível alterar valores individuais após o tempo de construção.
* Se os parâmetros especificados estiverem fora do intervalo permitido, um `ArgumentError` será lançado.

1. Decida sobre as taxas de bits inicial, mínima e máxima.
1. Determine a política ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Defina os valores dos parâmetros ABR no `ABRControlParameters` construtor e atribua-os ao Media Player.

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

