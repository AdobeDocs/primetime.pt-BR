---
description: Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode criar um novo a qualquer momento.
seo-description: Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode criar um novo a qualquer momento.
seo-title: Configure as taxas de bits adaptáveis usando ABRControlParameters
title: Configure as taxas de bits adaptáveis usando ABRControlParameters
uuid: 99b7a463-327b-48bf-8244-e41467072b44
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Configure as taxas de bits adaptáveis usando ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}

Você pode definir valores de controle ABR somente com ABRControlParameters, mas pode criar um novo a qualquer momento.

As seguintes condições se aplicam a `ABRControlParameters`:

* Você deve fornecer valores para todos os parâmetros no momento da construção.
* Não é possível alterar valores individuais após o tempo de construção.
* Se os parâmetros especificados estiverem fora do intervalo permitido, um `ArgumentError` será lançado.

1. Determine a política ABR:

   * `ABRControlParameters.CONSERVATIVE_POLICY`
   * `ABRControlParameters.MODERATE_POLICY`
   * `ABRControlParameters.AGGRESSIVE_POLICY`

1. Defina os valores dos parâmetros ABR no construtor `ABRControlParameters` e atribua-os ao Media Player.

   ```js
   var abrParams = new AdobePSDK.ABRControlParameters(); 
   abrParams.initialBitRate = nInitialBitRate; 
   abrParams.minBitRate = nMinBitRate; 
   abrParams.maxBitRate = nMaxBitRate; 
   abrParams.abrPolicy = eABRPolicy; 
   player.abrControlParameters = abrParams;
   ```

