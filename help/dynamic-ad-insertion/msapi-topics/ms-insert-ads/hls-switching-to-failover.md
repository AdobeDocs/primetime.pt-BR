---
description: A pilha HLS da Apple oferece suporte à alternância para fluxos de failover/backup se não puder recuperar fluxos do conjunto principal. Para dispositivos HLS da Apple, para facilitar o failover, você pode sinalizar o servidor manifest para tratar os fluxos primários e de failover identificados na lista de reprodução principal como conjuntos dissociados (com seus próprios UUIDs).
seo-description: A pilha HLS da Apple oferece suporte à alternância para fluxos de failover/backup se não puder recuperar fluxos do conjunto principal. Para dispositivos HLS da Apple, para facilitar o failover, você pode sinalizar o servidor manifest para tratar os fluxos primários e de failover identificados na lista de reprodução principal como conjuntos dissociados (com seus próprios UUIDs).
seo-title: Facilitando a alternância do player HLS para fluxos de failover/backup
title: Facilitando a alternância do player HLS para fluxos de failover/backup
uuid: 2fea8a51-e4cb-4fc9-82d5-6305a1d96603
translation-type: tm+mt
source-git-commit: 6863b63c7fa0068c3c5060fb946515c6cc5e3bff
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Facilitando a alternância do player HLS para fluxos de failover/backup {#facilitating-hls-player-switching-to-failover-backup-streams}

A pilha HLS da Apple oferece suporte à alternância para fluxos de failover/backup se não puder recuperar fluxos do conjunto principal. Para dispositivos HLS da Apple, para facilitar o failover, você pode sinalizar o servidor manifest para tratar os fluxos primários e de failover identificados na lista de reprodução principal como conjuntos dissociados (com seus próprios UUIDs).

Para facilitar a alternância para fluxos de failover ou backup em dispositivos Apple HLS, você pode especificar o parâmetro `ptfailover` no URL do Bootstrap. Se você fornecer esse parâmetro, o servidor manifest criará sessões de reprodução separadas (que determinam os anúncios agrupados) para cada conjunto de failover.

## Detalhes

Como o SSAI lida com a alternância de HLS para failover/backup quando você inclui `ptfailover=true` na solicitação do Bootstrap:

* Quando uma lista de reprodução principal contém conjuntos primários e de backup:

   * O servidor manifest identifica URLs de fluxo AV para diferentes conjuntos de failover usando o atributo `BANDWIDTH` e a ordem de análise dos URLs de fluxo AV. Cria sessões de reprodução internas separadas (identificadas por UUIDs separadas) e cria URLs de fluxo apontando para servidores de manifesto com diferentes UUIDs identificando diferentes sessões de reprodução.
   * O servidor manifest identifica URLs de fluxo I-Frame para diferentes conjuntos de failover usando o atributo `RESOLUTION` correspondente e a ordem de análise dos URLs de fluxo I-Frame. O SSAI usa os UUIDs que identificam os fluxos AV associados para URLs de fluxo de I-Frame apontando para SSAI.
   * Para este recurso, o servidor manifest suporta apenas grupos `EXT-X-MEDIA` sem atributos URI na lista de reprodução principal.
   * O servidor manifest detecta uma resposta de erro 404 de um CDN com um cabeçalho `X-Object-Too-Old: true` e preserva o código de status e o cabeçalho ao enviar essa resposta ao player.

* Os anúncios anteriores são adicionados apenas ao conjunto principal; eles são completamente desabilitados nos conjuntos de failover para evitar anúncios anteriores errados e/ou duplicados quando o player muda para fluxos de failover.

