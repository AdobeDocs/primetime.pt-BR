---
description: Embora o método de criptografia AES-128 criptografe todo o container de fluxo de transporte (TS), incluindo cabeçalhos, a criptografia SAMPLE-AES criptografa apenas o áudio e parte dos dados de vídeo.
title: Exemplo de fluxos HLS criptografados com AES
exl-id: 04bda50f-5ca4-4a00-bb5a-97259a2cb005
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Exemplo de fluxos HLS criptografados com AES{#sample-aes-encrypted-hls-streams}

Embora o método de criptografia AES-128 criptografe todo o container de fluxo de transporte (TS), incluindo cabeçalhos, a criptografia SAMPLE-AES criptografa apenas o áudio e parte dos dados de vídeo.

Em fluxos criptografados, um bloco protegido é identificado sobre o qual o processo de proteção é concluído. Os blocos protegidos por vídeo H.264 são o corpo dos tipos 1 e 5 das unidades de camada de adaptação de rede (NAL). Um bloco de áudio protegido é um quadro de áudio, e o áudio deve estar no formato AAC.

>[!IMPORTANT]
>
>Você deve ter a chave e o vetor de inicialização (IV). O TVSDK do navegador usa a chave e o IV para descriptografar o fluxo antes de reproduzi-lo.

Cada bloco protegido contém um inteiro de blocos de 16 bytes que são criptografados usando o modo CBC (Encadeamento de Blocos de Criptografia) AES-128 sem preenchimento. O CBC ocorre em cada bloco protegido e, no início de cada novo bloco protegido, o IV deve ser redefinido para seu valor original.

Os seguintes codecs são compatíveis:

* Para vídeo, o H.264 é compatível.
* Para áudio, o sample-AES é compatível somente com o AAC.
