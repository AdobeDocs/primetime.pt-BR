---
description: A pilha HLS da Apple oferece suporte à alternância para fluxos de failover/backup se não for possível recuperar fluxos do conjunto principal. Para dispositivos HLS da Apple, para facilitar o failover, você pode sinalizar o servidor de manifesto para tratar fluxos primários e de failover identificados na lista de reprodução principal como conjuntos dissociados (com seus próprios UUIDs).
title: Facilitando a alternância do reprodutor HLS para fluxos de failover/backup
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# Facilitando a alternância do reprodutor HLS para fluxos de failover/backup {#facilitating-hls-player-switching-to-failover-backup-streams}

A pilha HLS da Apple oferece suporte à alternância para fluxos de failover/backup se não for possível recuperar fluxos do conjunto principal. Para dispositivos HLS da Apple, para facilitar o failover, você pode sinalizar o servidor de manifesto para tratar fluxos primários e de failover identificados na lista de reprodução principal como conjuntos dissociados (com seus próprios UUIDs).

Para facilitar a alternância para fluxos de failover ou backup em dispositivos Apple HLS, você pode especificar o parâmetro `ptfailover` no URL do Bootstrap. Se você fornecer esse parâmetro, o servidor de manifesto criará sessões de reprodução separadas (que determinam os anúncios compilados) para cada conjunto de failover.

## Detalhes

Como o SSAI lida com a alternância de HLS para failover/backup quando você inclui `ptfailover=true` na solicitação do Bootstrap:

* Quando uma lista de reprodução principal contém conjuntos primários e de backup:

   * O servidor manifest identifica URLs de fluxo AV para diferentes conjuntos de failover usando o atributo `BANDWIDTH` e a ordem de análise dos URLs de fluxo AV. Ele cria sessões de reprodução internas separadas (identificadas por UUIDs separadas) e cria URLs de fluxo que apontam para servidores de manifesto com as diferentes UUIDs que identificam sessões de reprodução diferentes.
   * O servidor manifest identifica URLs de fluxo de I-Frame para diferentes conjuntos de failover usando o atributo `RESOLUTION` correspondente e a ordem de análise dos URLs de fluxo de I-Frame. O SSAI usa os UUIDs que identificam os fluxos AV associados para URLs de fluxo de I-Frame que apontam para SSAI.
   * Para esse recurso, o servidor de manifesto suporta apenas grupos `EXT-X-MEDIA` sem atributos de URI na lista de reprodução principal.
   * O servidor de manifesto detecta uma resposta de erro 404 de um CDN com um cabeçalho `X-Object-Too-Old: true` e preserva o código de status e o cabeçalho ao enviar essa resposta ao reprodutor.

* Os anúncios precedentes são adicionados apenas ao conjunto principal; eles são completamente desativados nos conjuntos de failover para evitar qualquer anúncio precedente incorreto e/ou duplicado quando o reprodutor muda para fluxos de failover.

