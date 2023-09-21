---
description: Estas são algumas informações e exemplos sobre como o TVSDK do navegador acomoda manifestos mestres atualizados.
title: Arquitetura de atualização ao vivo do manifesto principal
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---

# Arquitetura de atualização ao vivo do manifesto principal{#live-master-manifest-update-architecture}

Estas são algumas informações e exemplos sobre como o TVSDK do navegador acomoda manifestos mestres atualizados.

Por padrão, esse recurso está desativado. Se o aplicativo a ativar definindo uma frequência de atualização em minutos, as seguintes etapas ocorrerão após cada intervalo de atualização:

1. O TVSDK do navegador verifica a hora e a tag da última modificação do manifesto mestre para determinar se o arquivo foi atualizado.

   Se a hora e a tag tiverem sido alteradas, o arquivo será considerado como modificado.
1. O TVSDK do navegador analisa e analisa o novo manifesto e toma as medidas apropriadas com base na natureza da atualização.
1. Se a taxa de bits de reprodução atual corresponder à taxa de bits do manifesto modificado, o TVSDK do navegador mudará para o novo perfil.

   O novo perfil pode ser de um servidor diferente ou do mesmo servidor, com a mesma taxa de bits. Nesse caso, a transição é suave.
1. Se a taxa de bits de reprodução atual não estiver mais presente no novo manifesto, o TVSDK do navegador tentará encontrar uma taxa de bits no perfil atual que também existe no novo manifesto.

   * Se uma correspondência for encontrada, o reprodutor primeiro alterna para o perfil de taxa de bits correspondente no manifesto existente e alterna para o perfil de taxa de bits correspondente no manifesto atualizado. Isso garante que a transição seja tranquila.
   * Se não houver uma taxa de bits em comum entre o manifesto anterior e o novo manifesto, ou se o TVSDK do navegador não puder alternar para a taxa de bits correspondente, o TVSDK do navegador alternará diretamente para o perfil de taxa de bits mais baixa do novo manifesto e usará o ABR para alternar para qualquer taxa de bits permitida com base na largura de banda. Isso pode causar uma pequena falha na reprodução, mas deve ter impacto mínimo.

1. Se a atualização for bem-sucedida, o TVSDK do navegador enviará um `MediaPlayerItemEvent.MASTER_UPDATED` evento.
1. Se a atualização não for bem-sucedida, a reprodução continuará com a configuração de antes dessa atualização.

## Exemplo 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

As seguintes taxas de bits estão transmitindo ao vivo:

* 500k
* 900k
* 2100k

O fluxo do 2100k tem alguns problemas, portanto, precisa ser reiniciado. O manifesto mestre foi atualizado para conter apenas 500k e 900k. Pouco tempo depois, os usuários que assistirem a este programa a 2100k terão uma taxa de bits de mudança para 900k. Os usuários que assistem a 900k continuam assistindo a 900k. Posteriormente, o fluxo do 2100k é retomado e adicionado novamente ao manifesto principal. Um tempo depois, os usuários que estão assistindo a 900k, e têm a largura de banda, são comutados para 2100k.

### Exemplo 2 {#example_485E9A9F373D454CADE5395DEC734E5D}

As seguintes taxas de bits estão transmitindo ao vivo:

* 500k
* 900k
* 2100k

Todas essas taxas de bits precisam ser reiniciadas. Há dois fluxos temporais configurados para isso, de 400k e 1500k. Os usuários são comutados para 400k, que é a taxa de bits mais baixa da nova configuração. Alguns dos usuários são comutados para 1500k quando sua largura de banda é suficiente. Posteriormente, as taxas de três bits são revertidas e o manifesto principal é atualizado. Os usuários alternam automaticamente de volta para assistir a 500k, que é a largura de banda mais baixa no manifesto revisado (original). Um tempo depois, os usuários são comutados para a largura de banda mais alta (900k ou 1200k) permitida pela rede.

<!-- 

WRITER: Add relref to api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#MASTER_UPDATED

 -->
