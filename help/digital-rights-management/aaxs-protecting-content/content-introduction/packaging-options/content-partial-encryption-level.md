---
title: Nível de criptografia parcial
description: Nível de criptografia parcial
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---


# Nível de criptografia parcial{#partial-encryption-level}

Especifica se todos os quadros, ou apenas um subconjunto de quadros, devem ser criptografados. Há três níveis de criptografia: baixa, média e alta.

>[!NOTE]
>
>Para monitoramento de vídeo somente em arquivos F4V/H.264.

A criptografia parcial foi projetada para fornecer granularidade aos provedores de conteúdo para codificar o conteúdo em partes. A criptografia de conteúdo adiciona a sobrecarga da CPU ao dispositivo que está descriptografando e visualizando o conteúdo. Use a criptografia parcial para reduzir a sobrecarga da CPU, mantendo uma proteção muito forte do conteúdo. Um caso motivador para usar esse recurso é um único conteúdo que deve ser reproduzido em dispositivos de baixa, média e alta potência.

Devido à natureza da codificação de vídeo, não é necessário criptografar 100% do vídeo para torná-lo intocável se roubado. A criptografia parcial tem três configurações, baixa, média e alta, e as porcentagens associadas de criptografia dependem de como o vídeo é codificado. Devido a essa dependência de codificação, a porcentagem do seu conteúdo criptografado fica dentro dos seguintes intervalos:

* Alto: Criptografa todas as amostras.
* Médio: Criptografa um target para 50% dos dados.
* Baixo: Criptografa um target de 20 a 30% dos dados.

Essas configurações foram criadas com a seguinte regra: Qualquer conteúdo criptografado na configuração baixa também é criptografado na configuração média. Isso garante que o mesmo conteúdo distribuído em criptografia baixa por uma parte e distribuído em criptografia média por outra parte não comprometa a proteção do conteúdo.

Exemplo de caso de uso: A redução do nível de criptografia diminui a sobrecarga da descriptografia no cliente e melhora o desempenho da reprodução em máquinas de baixa definição.
