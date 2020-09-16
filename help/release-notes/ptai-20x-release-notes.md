---
title: Notas de versão do PTAI 20.9.2
description: As notas de versão PTAI 20.9.2 descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos no Primetime Dynamic Ad Insertion no ano 2020.
translation-type: tm+mt
source-git-commit: e3d2811e40bc34bfdaacdab1529fa9b01e416a98
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 0%

---


# Notas de versão do Primetime Dynamic Ad Insertion 20.9.2

As notas de versão do Dynamic Ad Insertion 20.9.2 descrevem o que é novo ou alterado, os problemas resolvidos e os problemas conhecidos no Primetime Dynamic Ad Insertion no ano 2020.

## Novidades do PTAI 20.9.2

**Quando:** terça-feira, 15 de setembro de 2020, das 3:30 às 6:30 Hora do Leste

**Aprimoramentos**

* Suporte fornecido para a inclusão de tipos de anúncios não lineares usando `EXT-X-MARKER` tags.
Para obter mais informações ou ativar esse recurso, entre em contato com o representante do suporte técnico.

* Fornecido suporte para limitar o tempo geral de resolução do anúncio, se os provedores demorarem muito para responder. Para ativar a limitação, defina o parâmetro da API de inicialização como `ptadtimeout` um valor em milissegundos.

   >[!NOTE]
   >
   >Esse tempo limite se aplica somente às solicitações de anúncio, não às solicitações de anúncio.

### Aprimoramentos e correções nas versões anteriores

#### Versão 20.9.1

**Quando:** terça-feira, 1 de setembro de 2020, das 3:30 às 7:30, horário do leste

**Alterações**

* Correção do problema para clientes que usavam HLS/CMAF, onde EXT-X-MAP às vezes não possuíam tokens CDN ou tags EXT-X-MAP às vezes eram implantadas incorretamente na janela do DVR.

#### Versão 20.8.4

**Quando:** quarta-feira, 19 de agosto de 2020, das 03h30 às 07h30, horário do leste

**Aprimoramentos e correções**

Atualizações de manutenção.

#### Versão 20.8.1

**Quando:** terça-feira, 4 de agosto de 2020, das 3:00 às 6:00 Hora do Leste

**Aprimoramentos e correções**

Atualizações de manutenção.

#### Versão 20.7.1

**Quando:** quinta-feira, 9 de julho de 2020, das 03:00 às 05:00 Hora do Leste

**Novos recursos e melhorias**

* Aprimoramento do SCTE35 para usar mensagens de Start/término do anúncio do provedor ou de Start/término para identificar a dica.

* Atualização do cabeçalho X-ADBE-AI-X1 com informações adicionais para ajudar a solucionar problemas.

* Agregação de métricas aprimorada.

* Painel do console SSAI aprimorado para o painel Estatísticas da sessão

#### Versão 20.6.2

**Quando:** quinta-feira, 18 de junho de 2020, das 03h00 às 04h00, horário do leste

**Aprimoramentos**

Sincronização de fluxo aprimorada para clientes de vídeo que exigem precisão de milissegundos. Entre em contato com o suporte ao Adobe para ativar a precisão de milissegundos para `#EXT-X-PROGRAM-DATE-TIME tags`.

#### Versão 20.6.1

**Quando:** terça-feira, 2 de junho de 2020, das 03:00 às 05:00 Hora do Leste

**Novos recursos**

Entre em contato com o Suporte ao Adobe para ativar os seguintes novos recursos por meio da configuração do servidor:

* Manipulação manifesta: Os URLs de segmento e recurso HLS agora podem ser transformados entre HTTP e HTTPS para aumentar o desempenho, reduzindo os handshakes TLS em solicitações de back-end. Também pode ser usado para unificar fragmentos de anúncio/conteúdo nos mesmos CDNs.

* VOD de forma longa: Aprimoramento das APIs para manter a sessão em funcionamento com ativos VOD de forma longa.

**Correções de erros**

* Correção de um problema em que fragmentos WebVTT eram sempre solicitados sob protocolo http, independentemente do protocolo original solicitado.

* Correção de um problema em que as tags EXT-X-DISCONTINUITY eram removidas da parte superior da lista de reprodução ao alternar dos anúncios para o conteúdo. Entre em contato com o suporte ao Adobe para ativar essa correção.

#### Versão 20.5.1

**Quando:** terça-feira, 5 de maio de 2020 das 04:00 às 05:00 Hora do Leste

* Correção de um problema para garantir que cabeçalhos CORS corretos sejam fornecidos quando cabeçalhos If-Modifiados-Since são enviados.

* Correções de erros no painel CRS.

* Atualizações de manutenção.

#### Versão 20.3.4

**Quando:** quarta-feira, 1 de abril de 2020, das 03:00 às 04:00, horário do leste

* Corrigido um problema que fazia com que as legendas ficassem fora de sincronização após a inserção do anúncio no VOD/ WebVTT.

* Atualizações de segurança.

#### Versão 20.3.3

**Quando:** quinta-feira, 26 de março de 2020, das 03h00 às 04h00, horário do leste

* As respostas SSAI 4XX e 5XX agora fornecem corretamente cabeçalhos relacionados ao CORS, permitindo que clientes de exibição da Web javascript entre domínios leiam com êxito respostas de erro.

* Correção de um problema com cabeçalhos X-Forwarded-For, em que os endereços IPv6 não eram corretamente codificados por URL quando passados para os servidores de publicidade.

* Correção de um problema com fluxos de áudio CMAF/descompilados, em que, em certos cenários, os números EXT-X-MEDIA-SEQUENCE aumentavam incorretamente.

#### Versão 20.3.2

**Quando:** quarta-feira, 11 de março de 2020, das 05:30 às 07:00 Hora do Leste

* Melhorias no tratamento do sinal SCTE35.

* Atualizações de manutenção.

#### Versão 20.3.1

**Quando:** quinta-feira, 5 de março de 2020, das 02h30 às 04h30, horário do leste

* Melhorias no desempenho:

   * Adicionado suporte de cache para manifestos m3u8 principais/de mídia. Esses manifestos agora respondem ao Cache-Control: cabeçalhos public e Max-Age, que geralmente podem melhorar o desempenho do start de vídeo.

   * Adição de suporte para forçar a busca de criações https em http, o que também pode melhorar o desempenho do start de vídeo.

* Correções de segurança e manutenção.

#### Versão 20.2.1

**Quando:** quinta-feira, 13 de fevereiro de 2020, das 04:30 às 05:30, horário do leste

* Adicionado suporte para a sutura de ativos de anúncios que contêm vários fluxos somente de áudio com base no idioma/codec/taxa de bits.
* Pequenas melhorias de desempenho e atualizações de manutenção.

#### Versão 20.1.3

**Quando:** terça-feira, 28 de janeiro de 2020, das 2h00 às 03h00, horário do leste

* **VMAP com suporte FER para nbc CueFormat**

   Converta dicas do fluxo FER em parâmetros de substituição de linha do tempo FW quando `ptcueformat=nbc` são usadas e o fluxo é um fluxo VOD com dicas no manifesto e anúncios integrados.

* Limpe o campo user-agent no cabeçalho HTTP antes de encaminhar para provedores de anúncios de terceiros/ CDN.

* Filtre os caracteres de controle/não imprimíveis (código ASCII &lt; 32) dos cabeçalhos HTTP agente-usuário antes de enviar para o Auditude e outros provedores de anúncios, CDNs. Auditude Ad-Call usado para falhar em cabeçalhos inválidos.

* Expurgue objetos V1 antigos de grupos NetStorage para manter a contagem de objetos dentro dos limites seguros do Akamai.

#### Versão 20.1.2 (Hotfix)

**Quando:** segunda-feira, 20 de janeiro de 2020, das 02h00 às 03h00, horário do leste

* Atualizações de manutenção.

#### Versão 20.1.1

**Quando:** quarta-feira, 15 de janeiro de 2020, das 04:00 às 05:00, horário do leste

* O Creative Repacking Service agora oferece inserção de anúncios mais rápida bloqueando automaticamente a listagem de anúncios malformados.

* Adicionado suporte de fase 1 para o novo formato de sinalização SCTE 35 na inserção de anúncios no servidor.

* Atualizações de manutenção.

## Problemas resolvidos {#Resolved-issues}

Quando a resolução estiver associada a um problema reportado, uma referência do Zendesk será exibida. Por exemplo, `ZD#xxxxx`.

**PTAI 20.9.1**

* Correção do problema para clientes que usavam HLS/CMAF, onde EXT-X-MAP às vezes não possuíam tokens CDN ou tags EXT-X-MAP às vezes eram implantadas incorretamente na janela do DVR.

**PTAI 20.6.1**

* `WebVTT` fragmentos sempre foram solicitados sob protocolo http, independentemente do protocolo original solicitado.

* `EXT-X-DISCONTINUITY` as tags são removidas da parte superior da lista de reprodução ao alternar de anúncios para conteúdo. Entre em contato com o suporte ao Adobe para ativar essa correção.

**PTAI 20.5.1**

* Problemas com cabeçalhos CORS quando os cabeçalhos If-Modifique-Since são enviados.

* Problemas no painel CRS.

**PTAI 20.3.4**

* Problema que fazia com que as legendas ficassem fora de sincronização após a inserção do anúncio no VOD/ WebVTT.

**PTAI 20.3.3**

* Problema com cabeçalhos X-Forwarded-For, nos quais os endereços IPv6 não eram corretamente codificados por URL quando passados para os servidores de publicidade.

* Problema com fluxos de áudio CMAF/descompilados, em que, em certos cenários, os números EXT-X-MEDIA-SEQUENCE aumentam incorretamente em certos cenários

## Problemas conhecidos e limitações

**PTAI 20.3.3**

Nenhuma nova limitação foi adicionada.
