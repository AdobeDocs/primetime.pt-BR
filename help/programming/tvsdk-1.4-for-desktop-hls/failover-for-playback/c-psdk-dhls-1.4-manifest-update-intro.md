---
description: O TVSDK pode detectar informações alteradas de reprodução em manifestos mestres m3u8 para transmissão ao vivo e atualizar as informações de reprodução enquanto o fluxo está sendo reproduzido. O TVSDK suporta um conjunto dinâmico de perfis de taxa de bits à medida que os perfis aparecem ou desaparecem do manifesto mestre, incluindo taxas de bits de perfil não sobrepostas entre atualizações.
seo-description: O TVSDK pode detectar informações alteradas de reprodução em manifestos mestres m3u8 para transmissão ao vivo e atualizar as informações de reprodução enquanto o fluxo está sendo reproduzido. O TVSDK suporta um conjunto dinâmico de perfis de taxa de bits à medida que os perfis aparecem ou desaparecem do manifesto mestre, incluindo taxas de bits de perfil não sobrepostas entre atualizações.
seo-title: Atualização do manifesto mestre em tempo real
title: Atualização do manifesto mestre em tempo real
uuid: 44f8adc2-0538-4c5d-8e39-55f661d8540b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Atualização do manifesto mestre em tempo real{#live-master-manifest-update}

O TVSDK pode detectar informações alteradas de reprodução em manifestos mestres m3u8 para transmissão ao vivo e atualizar as informações de reprodução enquanto o fluxo está sendo reproduzido. O TVSDK suporta um conjunto dinâmico de perfis de taxa de bits à medida que os perfis aparecem ou desaparecem do manifesto mestre, incluindo taxas de bits de perfil não sobrepostas entre atualizações.

Os seguintes recursos são suportados:

* Contagem de perfis (aumentando ou diminuindo)
* Taxas de bits do perfil (sobrepostas ou não sobrepostas)
* Perfis com URLs nos mesmos (ou diferentes) servidores
* Qualquer estrutura de failover

Todas as seguintes condições devem ser cumpridas:

* O fluxo é ao vivo.
* A hora e a tag mudam.
* Todas as informações de execução permanecem as mesmas (exceto que os URLs podem variar).
* As informações de acesso do DRM permanecem as mesmas.
* Os segmentos são empacotados ao redor dos mesmos PTS e limites de quadros em um pequeno intervalo de erros.

## Arquitetura de atualização do manifesto ao vivo {#section_32254A0F684B4960ACC33BF6B1AEF6F1}

Estas são algumas informações e exemplos sobre como o TVSDK acomoda manifestos mestre atualizados.

Por padrão, esse recurso está desativado. Se seu aplicativo o ativar definindo uma frequência de atualização em minutos, as seguintes etapas ocorrem após cada intervalo de atualização:

1. O TVSDK verifica a hora e a tag da última modificação do manifesto mestre para determinar se o arquivo foi atualizado.

   Se a hora e a tag tiverem sido alteradas, o arquivo será considerado como modificado.
1. O TVSDK analisa e analisa o novo manifesto e toma as medidas apropriadas com base na natureza da atualização.
1. Se a taxa de bits de reprodução atual corresponder à taxa de bits do manifesto modificado, o TVSDK alterna para o novo perfil.

   O novo perfil pode ser de um servidor diferente ou do mesmo servidor, na mesma taxa de bits. Nesse caso, a transição é suave.
1. Se a taxa de bits de reprodução atual não estiver mais presente no novo manifesto, o TVSDK tenta encontrar uma taxa de bits no perfil atual que também existe no novo manifesto.

   * Se uma correspondência for encontrada, o player primeiro alterna para o perfil de taxa de bits correspondente no manifesto existente e alterna para o perfil de taxa de bits correspondente no manifesto atualizado. Isso garante que a transição seja suave.
   * Se não houver uma taxa de bits comum entre o manifesto anterior e o novo manifesto, ou se o TVSDK não puder alternar para a taxa de bits correspondente, o TVSDK alternará diretamente para o perfil de taxa de bits mais baixa do novo manifesto e usará ABR para alternar para qualquer taxa de bits permitida com base na largura de banda. Isso pode causar uma leve falha na reprodução, mas deve ter impacto mínimo.

1. Se a atualização for bem-sucedida, o TVSDK despachará um `MediaPlayerItemEvent.MASTER_UPDATED` evento.
1. Se a atualização não for bem-sucedida, a reprodução continuará com a configuração a partir de antes desta atualização.

### Exemplo 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

As seguintes taxas de bits são de transmissão ao vivo:

* 500k
* 900k
* 2100k

O fluxo de 2100k tem alguns problemas, então ele precisa ser reiniciado. O manifesto principal é atualizado para conter apenas 500 k e 900 k. Pouco depois, os usuários que assistem a esse programa a 2100k experimentarão uma mudança de taxa de bits para 900k. Os usuários assistindo a 900k continuam assistindo a 900k. Posteriormente, o fluxo de 2100k é retomado e é adicionado novamente ao manifesto mestre. Um pouco depois, os usuários que estão assistindo a 900k e têm a largura de banda são mudados para 2100k.

### Exemplo 2 {#example_485E9A9F373D454CADE5395DEC734E5D}

As seguintes taxas de bits são de transmissão ao vivo:

* 500k
* 900k
* 2100k

Todas essas taxas de bits precisam ser reiniciadas. Há dois fluxos temporais para isso, de 400k e 1500k. Os usuários passam para 400k, que é a menor taxa de bits da nova configuração. Alguns dos usuários mudam para 1500k quando sua largura de banda é suficiente. Posteriormente, as taxas de três bits serão geradas novamente e o manifesto mestre será atualizado. Os usuários alternam automaticamente para assistir a 500k, que é a largura de banda mais baixa no manifesto revisado (original). Um pouco mais tarde, os usuários passam para a largura de banda mais alta (900k ou 1200k) que sua rede permite.

## Usar atualização do manifesto mestre ativo {#section_34AC4A9751DB4B7C8561302C6A59A1C4}

Você pode ativar esse recurso e verificar eventos relacionados.

1. Para ativar as atualizações do manifesto mestre ativo, defina a frequência de atualização (em minutos) definindo a `NetworkConfiguration.masterUpdateInterval` propriedade.
1. Como opção, rastreie atualizações de manifesto bem-sucedidas ao acompanhar o `MediaPlayerItemEvent.MASTER_UPDATED` evento.

