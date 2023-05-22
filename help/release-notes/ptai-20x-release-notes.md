---
title: Notas de versão do PTAI 20.12.1
description: As notas de versão do PTAI descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos no Primetime Ad Insertion no ano de 2020.
exl-id: 47e36e42-b6a0-408c-93da-f63c929396b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 0%

---

# Notas de versão do Primetime Ad Insertion 20.12.1

As notas de versão do Primetime Ad Insertion 20.12.1 descrevem o que é novo ou alterado, problemas resolvidos e problemas conhecidos no Primetime Ad Insertion no ano de 2020.

## Novidades na PTAI 20.12.1

**Quando:** Terça-feira, 08 de dezembro de 2020 das 01:00 às 04:00 Horário do Leste

**Alterações**

* Inclui hotfix para resolver problemas de conectividade intermitente do cliente (5xx) no Ad Insertion do Primetime encontrado em 30 de novembro de 2020.

## Aprimoramentos e correções em versões anteriores

### Versão 20.11.1

**Quando:** Quinta-feira, 5 de novembro de 2020 das 2h às 5h Horário do Leste

**Alterações**

* Atualizações de manutenção do.

### Versão 20.10.2

**Quando:** Quinta-feira, 29 de outubro de 2020 das 12:01 às 06:00, horário do leste dos EUA

**Alterações**

* Atualizações de manutenção do.

### Versão 20.10.1

**Quando:** Terça-feira, 13 de outubro de 2020 das 03:00 às 07:00 Horário do Leste

**Alterações**

* Atualizações de manutenção do.

### Versão 20.9.3

**Quando:** Quarta-feira, 30 de setembro de 2020 às 3:30 às 6:30, horário do leste dos EUA

**Alterações**

* Adição do parâmetro da API do Bootstrap `ptparallelstream`. Isso permite que os clientes com reprodutores que solicitam fluxos de áudio ou vídeo desmesclados do CMAF em paralelo para garantir que os anúncios em faixas de áudio e vídeo sejam consistentes. Defina o valor do parâmetro como true para ativar esse recurso ou omitir para desativar.

### Versão 20.9.2

**Quando:** Terça-feira, 15 de setembro de 2020 das 3:30 às 6:30 Horário do Leste

**Aprimoramentos**

* Suporte fornecido para a inclusão de tipos de anúncios não lineares usando `EXT-X-MARKER` específicos.
Para obter mais informações ou ativar esse recurso, entre em contato com o representante do suporte técnico.

* Forneceu suporte para limitar o tempo geral de resolução do anúncio, se os provedores demorarem muito para responder. Para habilitar a limitação, defina o parâmetro de API de inicialização `ptadtimeout` para um valor em milissegundos.

   >[!NOTE]
   >
   >Esse tempo limite se aplica somente a solicitações de anúncios, não a solicitações de criação de anúncios.

### Versão 20.9.1

**Quando:** Terça-feira, 1 de setembro de 2020 das 3:30 às 7:30 Horário do Leste

**Alterações**

* Correção do problema para clientes que usavam HLS/CMAF, em que EXT-X-MAP às vezes não tinha tokens CDN ou em que as tags EXT-X-MAP às vezes eram implantadas incorretamente na janela do DVR.

### Versão 20.8.4

**Quando:** Quarta-feira, 19 de agosto de 2020 das 03:30 às 07:30 Horário do Leste

**Melhorias e correções**

Atualizações de manutenção do.

### Versão 20.8.1

**Quando:** Terça-feira, 4 de agosto de 2020 das 3:00 às 6:00 Horário do Leste

**Melhorias e correções**

Atualizações de manutenção do.

### Versão 20.7.1

**Quando:** Quinta-feira, 9 de julho de 2020 das 03:00 às 05:00 Horário do Leste dos EUA

**Novos recursos e melhorias**

* Aprimoramento do SCTE35 para usar mensagens de início/fim do anúncio do provedor ou mensagens de início/fim de quebra para identificar a indicação.

* Atualização do cabeçalho X-ADBE-AI-X1 com informações adicionais para ajudar na solução de problemas.

* Agregação de métricas aprimorada.

* Painel do Console SSAI aprimorado para o painel Estatísticas da sessão

### Versão 20.6.2

**Quando:** Quinta-feira, 18 de junho de 2020 das 03:00 às 04:00 Horário do Leste dos EUA

**Aprimoramentos**

Sincronização de fluxo aprimorada para clientes de vídeo que exigem precisão de milissegundos. Entre em contato com o Suporte de Adobe para ativar a precisão de milissegundos para `#EXT-X-PROGRAM-DATE-TIME tags`.

### Versão 20.6.1

**Quando:** Terça-feira, 2 de junho de 2020 das 03:00 às 05:00 Horário do Leste

**Novos recursos**

Entre em contato com o Suporte de Adobe para ativar os seguintes novos recursos através da configuração do lado do servidor:

* Manipulação de manifesto: URLs de segmento e recurso do HLS agora podem ser transformados entre HTTP e HTTPS para aumentar o desempenho, reduzindo os handshakes de TLS em solicitações de back-end. Ele também pode ser usado para unificar fragmentos de anúncio/conteúdo nos mesmos CDNs.

* VOD de formulário longo: APIs aprimoradas para manter a sessão ativa com ativos de VOD de formulário longo.

**Correções de erros**

* Correção de um problema em que os fragmentos WebVTT eram sempre solicitados no protocolo http, independentemente do protocolo original solicitado.

* Correção de um problema em que as tags EXT-X-DISCONTINUITY eram removidas da parte superior da lista de reprodução ao alternar dos anúncios para o conteúdo. Entre em contato com o Suporte do Adobe para ativar essa correção.

### Versão 20.5.1

**Quando:** Terça-feira, 5 de maio de 2020 das 04:00 às 05:00 Horário do Leste

* Correção de um problema para garantir que os cabeçalhos CORS corretos fossem fornecidos quando os cabeçalhos If-Modified-Since eram enviados.

* Correções de erros no painel CRS.

* Atualizações de manutenção do.

### Versão 20.3.4

**Quando:** Quarta-feira, 1 de abril de 2020 das 03:00 às 04:00, horário do leste dos EUA

* Correção de um problema que fazia com que as legendas ficassem fora de sincronia após a inserção de anúncios em VOD/ WebVTT.

* Atualizações de segurança.

### Versão 20.3.3

**Quando:** Quinta-feira, 26 de março de 2020, das 03:00 às 04:00, horário do leste dos EUA

* As respostas SSAI 4XX e 5XX agora fornecem corretamente cabeçalhos relacionados ao CORS, permitindo que os clientes de visualização da Web javascript entre domínios leiam com êxito as respostas de erro.

* Correção de um problema com cabeçalhos X-Forwarded-For, em que os endereços IPv6 não eram corretamente codificados por URL quando passados para os servidores de publicidade.

* Correção de um problema com fluxos de áudio CMAF/desmesclados, em que, em determinados cenários, os números EXT-X-MEDIA-SEQUENCE eram incrementados incorretamente.

### Versão 20.3.2

**Quando:** Quarta-feira, 11 de março de 2020 das 05:30 às 07:00, horário do leste dos EUA

* Melhorias no manuseio de sinal SCTE35.

* Atualizações de manutenção do.

### Versão 20.3.1

**Quando:** Quinta-feira, 05 de março de 2020 das 02:30 às 04:30, horário do leste dos EUA

* Melhorias de desempenho:

   * Adição de suporte de cache para manifestos m3u8 de principal/mídia. Esses manifestos agora respondem ao Cache-Control: cabeçalhos públicos e Max-Age, que geralmente podem melhorar o desempenho de início de vídeo.

   * Adição de suporte para forçar a busca de criações https por http, o que também pode melhorar o desempenho da inicialização de vídeo.

* Correções de segurança e manutenção.

### Versão 20.2.1

**Quando:** Quinta-feira, 13 de fevereiro de 2020 das 04:30 às 05:30 Horário do Leste

* Adição de suporte para compilação de ativos de anúncio que contêm vários fluxos somente de áudio com base em idioma/codec/taxa de bits.
* Pequenos aprimoramentos de desempenho e atualizações de manutenção.

### Versão 20.1.3

**Quando:** Terça-feira, 28 de janeiro de 2020 das 2h às 3h Horário do Leste

* **VMAP com suporte FER para nbc CueFormat**

   Converter dicas do fluxo FER em parâmetros de substituição de linha do tempo FW, quando `ptcueformat=nbc` é usada e o fluxo é um fluxo de VOD com dicas em manifesto e anúncios incorporados.

* Limpe o campo user-agent no Cabeçalho HTTP antes de encaminhar para provedores de anúncios/CDN de terceiros.

* Filtre caracteres de controle/não imprimíveis (código ASCII &lt; 32) dos cabeçalhos HTTP do agente do usuário antes de enviar para o Auditude e outros provedores de anúncios, CDNs. O Ad-Call do Auditude usado para falhar esses cabeçalhos inválidos.

* Remova objetos V1 antigos de grupos do NetStorage para manter a contagem de objetos dentro dos limites seguros do Akamai.

### Versão 20.1.2 (Hotfix)

**Quando:** Segunda-feira, 20 de janeiro de 2020, das 02:00 às 03:00, horário do leste dos EUA

* Atualizações de manutenção do.

### Versão 20.1.1

**Quando:** Quarta-feira, 15 de janeiro de 2020 das 04:00 às 05:00, horário do leste dos EUA

* O Serviço de reempacotamento criativo agora oferece inserção mais rápida de anúncios, bloqueando automaticamente a listagem de criações malformadas.

* Adição do suporte da fase 1 para o novo formato SCTE 35 cue na inserção de anúncios do lado do servidor.

* Atualizações de manutenção.

## Problemas resolvidos {#Resolved-issues}

Quando a resolução está associada a um problema relatado, uma referência do Zendesk é exibida. Por exemplo, `ZD#xxxxx`.

**PTAI 20.9.1**

* Correção do problema para clientes que usavam HLS/CMAF, em que EXT-X-MAP às vezes não tinha tokens CDN ou em que as tags EXT-X-MAP às vezes eram implantadas incorretamente na janela do DVR.

**PTAI 20.6.1**

* `WebVTT` os fragmentos sempre foram solicitados no protocolo http, independentemente do protocolo original solicitado.

* `EXT-X-DISCONTINUITY` as tags são removidas da parte superior da lista de reprodução ao alternar dos anúncios para o conteúdo. Entre em contato com o Suporte do Adobe para ativar essa correção.

**PTAI 20.5.1**

* Problemas com cabeçalhos CORS quando cabeçalhos If-Modified-Since são enviados.

* Problemas no painel CRS.

**PTAI 20.3.4**

* Problema que fez com que as legendas ficassem fora de sincronia após a inserção do anúncio em VOD/ WebVTT.

**PTAI 20.3.3**

* Problema com cabeçalhos X-Forwarded-For, em que os endereços IPv6 não estavam corretamente codificados por URL quando passados para os servidores de publicidade.

* Problema com fluxos de áudio CMAF/desmisto, em que, em determinados cenários, os números EXT-X-MEDIA-SEQUENCE são incrementados incorretamente em determinados cenários

## Problemas conhecidos e limitações

**PTAI 20.10.1**

Nenhuma limitação nova adicionada.
