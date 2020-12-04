---
description: Embora o método de criptografia AES-128 criptografe todo o container de transmissão (TS), incluindo cabeçalhos, a criptografia SAMPLE-AES só criptografa o áudio e parte dos dados de vídeo.
seo-description: Embora o método de criptografia AES-128 criptografe todo o container de transmissão (TS), incluindo cabeçalhos, a criptografia SAMPLE-AES só criptografa o áudio e parte dos dados de vídeo.
seo-title: Exemplo de fluxos HLS criptografados por AES
title: Exemplo de fluxos HLS criptografados por AES
uuid: 32c1f87b-eb81-4e1c-92ea-ec37260a7ecb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Exemplo de fluxos HLS criptografados por AES{#sample-aes-encrypted-hls-streams}

Embora o método de criptografia AES-128 criptografe todo o container de transmissão (TS), incluindo cabeçalhos, a criptografia SAMPLE-AES só criptografa o áudio e parte dos dados de vídeo.

Em fluxos criptografados, um bloco protegido é identificado sobre o qual o processo de proteção é concluído. Os blocos protegidos por vídeo H.264 são o corpo dos tipos 1 e 5 das unidades de camada de adaptação de rede (NAL). Um bloco protegido de áudio é um quadro de áudio e o áudio deve estar no formato AAC.

>[!IMPORTANT]
>
>Você deve ter a chave e o vetor de inicialização (IV). O TVSDK do navegador usa a chave e o IV para descriptografar o fluxo antes de reproduzi-lo.

Cada bloco protegido contém um número inteiro de blocos de 16 bytes que são criptografados usando o modo CBC (cipher block-chaining) AES-128 sem preenchimento. A CBC ocorre em cada bloco protegido e, no start de cada novo bloco protegido, a IV deve ser redefinida para o seu valor original.

Os seguintes codecs são suportados:

* Para vídeo, o H.264 é compatível.
* Para áudio, o AES de amostra é compatível somente com AAC.

