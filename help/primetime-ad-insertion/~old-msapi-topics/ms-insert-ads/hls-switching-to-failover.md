---
description: A pilha HLS da Apple oferece suporte à alternância para fluxos de failover/backup se não conseguir recuperar fluxos do conjunto principal. Para dispositivos Apple HLS, para facilitar o failover, você pode sinalizar o servidor manifest para tratar fluxos primários e de failover identificados na lista de reprodução principal como conjuntos dissociados (com seus próprios UUIDs).
title: Facilitando a alternância do reprodutor HLS para fluxos de failover/backup
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# Facilitando a alternância do reprodutor HLS para fluxos de failover/backup {#facilitating-hls-player-switching-to-failover-backup-streams}

A pilha HLS da Apple oferece suporte à alternância para fluxos de failover/backup se não conseguir recuperar fluxos do conjunto principal. Para dispositivos Apple HLS, para facilitar o failover, você pode sinalizar o servidor manifest para tratar fluxos primários e de failover identificados na lista de reprodução principal como conjuntos dissociados (com seus próprios UUIDs).

Para facilitar a alternância para fluxos de failover ou backup em dispositivos Apple HLS, você pode especificar o `ptfailover` no URL do Bootstrap. Se você fornecer esse parâmetro, o servidor de manifesto criará sessões de reprodução separadas (que determinam os anúncios compilados) para cada conjunto de failover.

## Detalhes

Como o SSAI lida com a alternância HLS para failover/backup ao incluir `ptfailover=true` na solicitação Bootstrap:

* Quando uma lista de reprodução principal contiver conjuntos primários e de backup:

   * O servidor de manifesto identifica URLs de fluxo AV para diferentes conjuntos de failover usando o `BANDWIDTH` atributo e a ordem de análise dos URLs de fluxo do AV. Ele cria sessões de reprodução internas separadas (identificadas por UUIDs separados) e cria URLs de fluxo apontando para servidores manifest com as diferentes UUIDs identificando diferentes sessões de reprodução.
   * O servidor de manifesto identifica URLs de fluxo I-Frame para diferentes conjuntos de failover usando o correspondente `RESOLUTION` e a ordem de análise dos URLs de fluxo do I-Frame. O SSAI usa os UUIDs que identificam os fluxos de AV associados para URLs de fluxo I-Frame que apontam para o SSAI.
   * Para esse recurso, o servidor de manifesto só oferece suporte `EXT-X-MEDIA` grupos sem atributos URI na lista de reprodução principal.
   * O servidor de manifesto detecta uma resposta de erro 404 de um CDN com um `X-Object-Too-Old: true` e preserva o código de status e o cabeçalho ao enviar essa resposta ao reprodutor.

* Os anúncios antes da exibição são adicionados apenas ao conjunto principal; eles são completamente desativados nos conjuntos de failover para evitar anúncios antes da exibição errôneos e/ou duplicados quando o reprodutor muda para fluxos de failover.

