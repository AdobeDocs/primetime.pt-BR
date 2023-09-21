---
description: O TVSDK pode detectar informações de reprodução alteradas em manifestos m3u8 principais para transmissão ao vivo e atualizar as informações de reprodução enquanto o fluxo está sendo reproduzido. O TVSDK é compatível com um conjunto dinâmico de perfis de taxa de bits à medida que os perfis aparecem ou desaparecem do manifesto principal, incluindo taxas de bits de perfil não sobrepostas entre as atualizações.
title: Atualização ao vivo do manifesto principal
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# Atualização ao vivo do manifesto principal{#live-master-manifest-update}

O TVSDK pode detectar informações de reprodução alteradas em manifestos m3u8 principais para transmissão ao vivo e atualizar as informações de reprodução enquanto o fluxo está sendo reproduzido. O TVSDK é compatível com um conjunto dinâmico de perfis de taxa de bits à medida que os perfis aparecem ou desaparecem do manifesto principal, incluindo taxas de bits de perfil não sobrepostas entre as atualizações.

Os seguintes recursos são compatíveis:

* Contagem de perfis (aumentando ou diminuindo)
* Taxas de bits de perfil (sobreposição ou não sobreposição)
* Perfis com URLs nos mesmos servidores (ou diferentes)
* Qualquer estrutura de failover

Todas as seguintes condições devem ser atendidas:

* O fluxo está ativo.
* A hora e a tag mudam.
* Todas as informações de representação permanecem as mesmas (exceto que os URLs podem variar).
* As informações de acesso do DRM permanecem inalteradas.
* Segmentos são empacotados ao redor do mesmo PTS e limites de quadro em um pequeno intervalo de erro.

## Arquitetura de atualização ao vivo do manifesto principal {#section_32254A0F684B4960ACC33BF6B1AEF6F1}

Estas são algumas informações e exemplos sobre como o TVSDK acomoda manifestos principais atualizados.

Por padrão, esse recurso está desativado. Se o aplicativo a ativar definindo uma frequência de atualização em minutos, as seguintes etapas ocorrerão após cada intervalo de atualização:

1. O TVSDK verifica a hora e a tag da última modificação do manifesto principal para determinar se o arquivo foi atualizado.

   Se a hora e a tag tiverem sido alteradas, o arquivo será considerado como modificado.
1. O TVSDK analisa e analisa o novo manifesto e toma as medidas apropriadas com base na natureza da atualização.
1. Se a taxa de bits da reprodução atual corresponder à taxa de bits do manifesto modificado, o TVSDK mudará para o novo perfil.

   O novo perfil pode ser de um servidor diferente ou do mesmo servidor, com a mesma taxa de bits. Nesse caso, a transição é suave.
1. Se a taxa de bits de reprodução atual não estiver mais presente no novo manifesto, o TVSDK tentará encontrar uma taxa de bits no perfil atual que também exista no novo manifesto.

   * Se uma correspondência for encontrada, o reprodutor primeiro alterna para o perfil de taxa de bits correspondente no manifesto existente e alterna para o perfil de taxa de bits correspondente no manifesto atualizado. Isso garante que a transição seja tranquila.
   * Se não houver uma taxa de bits em comum entre o manifesto anterior e o novo manifesto, ou se o TVSDK não puder alternar para a taxa de bits correspondente, o TVSDK alternará diretamente para o perfil de taxa de bits mais baixa do novo manifesto e usará o ABR para alternar para qualquer taxa de bits permitida com base na largura de banda. Isso pode causar uma pequena falha na reprodução, mas deve ter impacto mínimo.

1. Se a atualização for bem-sucedida, o TVSDK enviará um `MediaPlayerItemEvent.MASTER_UPDATED` evento.
1. Se a atualização não for bem-sucedida, a reprodução continuará com a configuração de antes dessa atualização.

### Exemplo 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

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

## Usar atualização ao vivo do manifesto principal {#section_34AC4A9751DB4B7C8561302C6A59A1C4}

Você pode ativar esse recurso e verificar eventos relacionados.

1. Para ativar as atualizações ao vivo do manifesto principal, defina a frequência de atualização (em minutos) definindo o `NetworkConfiguration.masterUpdateInterval` propriedade.
1. Como opção, rastreie as atualizações bem-sucedidas do manifesto ouvindo o `MediaPlayerItemEvent.MASTER_UPDATED` evento.
