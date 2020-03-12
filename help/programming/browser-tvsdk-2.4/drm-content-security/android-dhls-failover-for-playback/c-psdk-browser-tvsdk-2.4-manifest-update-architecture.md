---
description: Estas são algumas informações e exemplos sobre como o TVSDK do navegador acomoda manifestos mestre atualizados.
seo-description: Estas são algumas informações e exemplos sobre como o TVSDK do navegador acomoda manifestos mestre atualizados.
seo-title: Arquitetura de atualização do manifesto ao vivo
title: Arquitetura de atualização do manifesto ao vivo
uuid: 6f253502-8dec-4b42-9ee1-99ad9bfd6080
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Arquitetura de atualização do manifesto ao vivo{#live-master-manifest-update-architecture}

Estas são algumas informações e exemplos sobre como o TVSDK do navegador acomoda manifestos mestre atualizados.

Por padrão, esse recurso está desativado. Se seu aplicativo o ativar definindo uma frequência de atualização em minutos, as seguintes etapas ocorrem após cada intervalo de atualização:

1. O TVSDK do navegador verifica a última hora e a tag do manifesto mestre para determinar se o arquivo foi atualizado.

   Se a hora e a tag tiverem sido alteradas, o arquivo será considerado como modificado.
1. O TVSDK do navegador analisa e analisa o novo manifesto e toma as medidas apropriadas com base na natureza da atualização.
1. Se a taxa de bits de reprodução atual corresponder à taxa de bits do manifesto modificado, o TVSDK do navegador alternará para o novo perfil.

   O novo perfil pode ser de um servidor diferente ou do mesmo servidor, na mesma taxa de bits. Nesse caso, a transição é suave.
1. Se a taxa de bits de reprodução atual não estiver mais presente no novo manifesto, o TVSDK do navegador tentará encontrar uma taxa de bits no perfil atual que também existe no novo manifesto.

   * Se uma correspondência for encontrada, o player primeiro alterna para o perfil de taxa de bits correspondente no manifesto existente e alterna para o perfil de taxa de bits correspondente no manifesto atualizado. Isso garante que a transição seja suave.
   * Se não houver uma taxa de bits comum entre o manifesto anterior e o novo manifesto, ou se o TVSDK do navegador não puder alternar para a taxa de bits correspondente, o TVSDK do navegador alternará diretamente para o perfil de taxa de bits mais baixo do novo manifesto e usará ABR para alternar para qualquer taxa de bits permitida com base na largura de banda. Isso pode causar uma leve falha na reprodução, mas deve ter impacto mínimo.

1. Se a atualização for bem-sucedida, o TVSDK do navegador enviará um `MediaPlayerItemEvent.MASTER_UPDATED` evento.
1. Se a atualização não for bem-sucedida, a reprodução continuará com a configuração a partir de antes desta atualização.

## Exemplo 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

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

<!-- 

WRITER: Add relref to api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#MASTER_UPDATED

 -->

