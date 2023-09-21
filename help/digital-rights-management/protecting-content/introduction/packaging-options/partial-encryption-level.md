---
title: Nível de criptografia parcial
description: Nível de criptografia parcial
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Nível de criptografia parcial {#partial-encryption-level}

Essa opção de empacotamento especifica se todos os quadros, ou somente um subconjunto de quadros, devem ser criptografados. Há três níveis de criptografia: baixo, médio e alto.

>[!NOTE]
>
>A criptografia parcial se aplica à trilha de vídeo somente em arquivos F4V/MP4.

A criptografia parcial foi projetada para fornecer granularidade aos provedores de conteúdo para codificar o conteúdo em partes. A criptografia de conteúdo adiciona sobrecarga da CPU ao dispositivo que está descriptografando e visualizando o conteúdo. Use criptografia parcial para reduzir a sobrecarga da CPU e, ao mesmo tempo, manter uma proteção muito forte do conteúdo. Um caso motivador para usar esse recurso é o conteúdo que deve ser reproduzido em dispositivos de baixa, média e alta potência.

Devido à natureza da codificação de vídeo, não é necessário criptografar 100% do vídeo para impossibilitá-lo de ser reproduzido se for roubado. A criptografia parcial tem três configurações, baixa, média e alta, e as porcentagens associadas de criptografia dependem de como o vídeo é codificado. Devido a essa dependência de codificação, a porcentagem do conteúdo criptografado está dentro dos seguintes intervalos:

* Alta: criptografa todas as amostras.
* Médio: criptografa um público-alvo para 50% dos dados.
* Baixo: criptografa um público alvo de 20 a 30% dos dados.

Essas configurações foram criadas usando a seguinte regra: qualquer conteúdo criptografado na configuração baixa também é criptografado na configuração média. Isso garante que o mesmo conteúdo distribuído com baixa criptografia por uma parte e distribuído com criptografia média por outra parte não comprometa a proteção do conteúdo.

Exemplo de caso de uso: a redução do nível de criptografia diminui a sobrecarga de descriptografia do cliente e melhora o desempenho de reprodução em máquinas low-end.
