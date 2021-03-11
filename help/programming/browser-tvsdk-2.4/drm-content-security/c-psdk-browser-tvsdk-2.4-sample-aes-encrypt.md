---
description: Embora o método de criptografia AES-128 criptografe todo o contêiner de fluxo de transporte (TS), incluindo cabeçalhos, a criptografia SAMPLE-AES só criptografa o áudio e parte dos dados de vídeo.
title: Fluxos HLS criptografados por AES de amostra
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# Exemplo de fluxos HLS criptografados por AES{#sample-aes-encrypted-hls-streams}

Embora o método de criptografia AES-128 criptografe todo o contêiner de fluxo de transporte (TS), incluindo cabeçalhos, a criptografia SAMPLE-AES só criptografa o áudio e parte dos dados de vídeo.

Em fluxos criptografados, é identificado um bloco protegido sobre o qual o processo de proteção é concluído. Os blocos protegidos por vídeo H.264 são o corpo de unidades de camada de adaptação de rede (NAL) dos tipos 1 e 5. Um bloco protegido de áudio é um quadro de áudio e o áudio deve estar no formato AAC.

>[!IMPORTANT]
>
>Você deve ter a chave e o vetor de inicialização (IV). O TVSDK do navegador usa a chave e a IV para descriptografar o fluxo antes de reproduzi-lo.

Cada bloco protegido contém um número inteiro de blocos de 16 bytes que são criptografados usando o modo CBC (Cifragem de Bloco) AES-128 sem preenchimento. A CBC ocorre em cada bloco protegido e, no início de cada novo bloco protegido, o IV deve ser reposto para o seu valor original.

Os seguintes codecs são suportados:

* Para vídeo, o H.264 é compatível.
* Para áudio, o AES de amostra é compatível somente com AAC.

