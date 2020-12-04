---
seo-title: Nível parcial de criptografia
title: Nível parcial de criptografia
uuid: dbd9ce92-c829-4cad-9ac4-c57bd4f70345
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Nível de criptografia parcial {#partial-encryption-level}

Essa opção de empacotamento especifica se todos os quadros, ou apenas um subconjunto de quadros, devem ser criptografados. Há três níveis de criptografia: baixa, média e alta.

>[!NOTE]
>
>A criptografia parcial se aplica à faixa de vídeo somente em arquivos F4V/MP4.

A criptografia parcial é projetada para fornecer granularidade aos provedores de conteúdo para codificar o conteúdo em partes. A criptografia de conteúdo adiciona a sobrecarga da CPU ao dispositivo que está descriptografando e exibindo o conteúdo. Use a criptografia parcial para reduzir a sobrecarga da CPU e, ao mesmo tempo, manter uma proteção muito forte do conteúdo. Um caso motivador para usar esse recurso é um único conteúdo que deve ser reproduzido em dispositivos de baixa, média e alta potência.

Devido à natureza da codificação de vídeo, não é necessário criptografar 100% do vídeo para torná-lo intocável se for roubado. A criptografia parcial tem três configurações, baixa, média e alta, e as porcentagens associadas de criptografia dependem de como o vídeo é codificado. Devido a essa dependência de codificação, a porcentagem do conteúdo criptografado está dentro dos seguintes intervalos:

* Alto: Criptografa todas as amostras.
* Médio: Criptografa um público alvo de 50% dos dados.
* Baixo: Criptografa um público alvo de 20 a 30% dos dados.

Essas configurações foram projetadas usando a seguinte regra: Qualquer conteúdo criptografado na configuração inferior também é criptografado na configuração média. Isso garante que o mesmo conteúdo distribuído com baixa criptografia por uma parte e distribuído com criptografia média por outra parte não comprometa a proteção do conteúdo.

Exemplo de caso de uso: A redução do nível de criptografia diminui a sobrecarga da descriptografia no cliente e melhora o desempenho da reprodução em máquinas de baixa definição.
