---
title: API do Bootstrap
description: null
translation-type: tm+mt
source-git-commit: aa43834fea161c537c448b7616c9bd8f779d1a74
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---


# API do Bootstrap {#bootstrap-api}

Parâmetros obrigatóriosGerar um bootstrap

## Descrição do parâmetro {#parameter-description}

| parâmetro | descrição | formatos |
|---|---|---|
| pabimode | Permite a inserção [](ad-insertion-live-linear-stream.md#partial-ad-break-support) parcial de anúncios para fluxos ao vivo. Valores possíveis:true para ativar omit para desativar (padrão desativado) | HLS/DASH |
| plataforma | Duração (em segundos) da janela de pesquisa e decisão do anúncio — até que ponto o Primetime Ad Insertion procurará dicas do anúncio quando um usuário do DVR ingressar no fluxo. Um valor de zero desativará a decisão de anúncio intermediário no manifesto inicial, com a decisão sendo retomada somente após a primeira atualização. Esse parâmetro é útil para desativar a inserção de anúncios em sessões que podem durar apenas alguns segundos (também conhecido como mudança de canal). Valores possíveis:string numérica 0-1800 (padrão 1800) | Somente HLS |
| ptassetid | ID exclusiva do conteúdo atribuído e mantido pelo editor.  Obrigatório quando usado em conjunto com o Akamai Ad Scaler. | HLS/DASH |
| ptcdn | Lista de um ou mais CDNs para hospedar ativos transcodificados. Para obter mais informações, consulte Suporte [](multi-cdn-support.md)a vários CDN. Valores possíveis: akamai, level3, lnw (redes de luz fundamental), comcastPor padrão, as CDNs Primetime Ad Insertion são usadas | HLS/DASH |
| ptcueformat | O formato especificado de tags para executar a decisão de anúncio (por exemplo, scte35). Valores possíveis: exemplo, dpiscte35, elemental Para formatos de sinalização personalizados, entre em contato com seu representante de conta técnica para obter o valor a ser usado no caso de uso | HLS/DASH |
| failover de canal | Sinaliza o servidor manifest para identificar fluxos primários e de failover especificados na lista de reprodução principal e para tratá-los como conjuntos de disjunção. Isso facilita o failover e evita erros de tempo. (Somente para dispositivos Apple HLS.) Para obter mais informações, consulte [Facilitando a alternância de reprodutor HLS](hls-switching-to-failover.md) | Somente HLS |
| tímulo | Se ativada, uma solicitação de anúncio separada é feita para cada valor encontrado em um ativo VOD.  Por padrão, o Primetime Ad Insertion tentará coletar todas as informações disponíveis e enviá-las para o servidor de publicidade em uma solicitação. Valores possíveis:true para ativar omit para desativar (padrão desativado) | HLS/DASH |
| pttagds | Permite a injeção de tags EXT-X-DISCONTINUITY-SEQUENCE em cabeçalhos HLS.Valores possíveis:true para ativar omit para desativar (padrão desativado) | Somente HLS |
| linha cronológica | Uma string contendo a linha do tempo desejada para o posicionamento e o conteúdo do anúncio, que substitui e quebra no fluxo de conteúdo. [ Consulte Formato de linha do tempo VOD ] | HLS/DASH |
| token | Habilita esquemas de proteção de token de autorização de fragmento/segmento de conteúdo para CDNs Valores possíveis: akamai, lnw (iluminação), ctl (ligação central) (a tokenização padrão está desativada) | HLS/DASH |
| modo de rastreamento | Habilitar esquemas de rastreamento de anúncio:Valores possíveis:simples para rastreamento de anúncios do lado do cliente para simples simplificação do rastreamento de anúncios do lado do servidor para rastreamento híbrido de anúncios do cliente/servidor (por padrão, nenhum rastreamento de anúncio é realizado) | HLS/DASH |
| pttrackingversion |  |  |
| ptadtimeout (como em 20.9.2) |  |  |
| ptparallelstream (como em 20.9.3) |  |  |
