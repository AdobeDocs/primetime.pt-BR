---
title: Notas de versão do TVSDK 2.1 PlayStation 4
description: As Notas de versão do TVSDK 2.1 para PlayStation 4 descrevem os recursos suportados e os problemas conhecidos no TVSDK 2.1 PlayStation 4 .
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# Notas de versão do TVSDK 2.1 PlayStation 4 {#tvsdk-playstation-release-notes}

As Notas de versão do TVSDK 2.1 para PlayStation 4 descrevem os recursos suportados e os problemas conhecidos no TVSDK 2.1 PlayStation 4 .

## Problemas resolvidos {#resolved-issues}

Aqui estão os problemas resolvidos para o TVSDK 2.1 para PlayStation 4:

**Versão 2.1.0.638**

* **PTPLAY-10439:**
Quando o link de anúncio do invólucro do VMAP foi interrompido, o player ficava preso no estado Preparação (não estava enviando `onComplete` para o chamador).

* **PTPLAY-10179:**
  `creativeRepackaging` e `fallbackOnInvalidCreative` Os valores de agora estão desativados por padrão. Além disso, quando o `creativeRepackaging` sinalizador foi definido, mas não `creativeRepackaging` foi fornecido o formato, a variável `onRepackagingComplete` O estava sendo chamado quantas vezes havia anúncios no ad break, fazendo com que os ad breaks fossem criados várias vezes.

* **Zendesk #10304**: a variável de ativação/desativação da veiculação de anúncios não foi inicializada. Agora inicializamos a variável de `DataSetEntry's` ator.

* **PTPLAY-10318:**
Foi introduzido o suporte para modo de segundo plano.
* **Zendesk # 17409:**
Ao entrar no modo de execução de truque, voltar para o modo de reprodução normal e, novamente, para o modo de reprodução de truque, a posição de reprodução estava pulando.
* **PTPLAY-9552:**
Após analisar os arquivos XML de resposta, o código de erro 1108 agora é enviado por ping sempre que não há anúncios presentes.
* **PTPLAY-9551:**
Quando não há ad break após o processamento do Auditude, o CRS chama **onPrefetchComplete** que diminui o groupCount. Como não há ad break, a variável **groupCount** é 0 e decrementado por 1. Anteriormente, o **groupCount** foi **uint32_t** por causa do qual costumava mudar para o valor máximo. Isso é agora **int32_t**.

**Versão 2.1.0.621**

* **Zendesk #4555**
Problemas de memória instantâneos erros de carregamento principais - `MediaItemLoader` Correção de falha que ocorria ao lançar `mediaitemloader`

* **Zendesk #17223**
2.x CSAI: nem todos os URLs de rastreamento de anúncios são acionados
   * Alguns anúncios VAST que, por sua vez, apontavam para um anúncio em linha não tinham URLs de rastreamento.
   * Quando há várias tags de impressão em um anúncio no VAST XML, somente o primeiro url de impressão foi salvo e o restante foi ignorado. Agora, todos os urls de impressão serão salvos e enviados por ping posteriormente.
* **Zendesk #17224**
O agente do usuário PS4 move as informações do primetime até o final da sequência de caracteres do usuário
* **Zendesk #17226**
2.x CSAI: nem todos os anúncios foram compilados.\
  A correção é para indicar que a linha do tempo foi alterada devido a operações insertBy ou eraseBy e o período muda de acordo.

* **Zendesk #17284**
  [Todas as plataformas] As legendas ocultas não são exibidas.\
  HLS - suporte para o `EXT-X-MEDIA-TIME` para arquivos de legenda VTT.

* **Zendesk #17889**
Reprodução &quot;Látea&quot; no PS4\
  deslocamento correto aplicado (para conversão de cores)

* **Zendesk #17954**
Lógica de fallback de anúncio + manipulação vazia vasta\
  Correção do problema se um dos invólucros Vast estivesse vazio, o analisador Vast era usado para continuar processando o invólucro.

* **Zendesk #17807**
Não é possível passar do espaço vazio Igual ao Zendesk #3103

* **Zendesk #17865**
Lógica de fallback no PS4 e XBox One\
  Igual ao Zendesk #3103

**Versão 2.1.0.591**

* **Zendesk #3767**
Trecho de código de anúncio PS4, A resolução de anúncios falha ao processar redirecionamentos VMAP.
* **Zendesk #4096**
PS4 CSAI: Falha de segmentação Corrigida uma falha quando o TVSDK lança falha de segmentação quando a biblioteca de anúncios está processando uma resposta VMAP.

* **Zendesk #4161**
O trickplay 16x no final do filme congela o deadlock fixo que acontece quando o trickplay retorna à reprodução normal

* **Zendesk #4208**
Falha aleatória quando Legendas ocultas são ativadas Vazamento de memória fixa quando as legendas ocultas foram ativadas

* **Zendesk #4213**
PS4 CSAI: Alterar a sequência padrão user-agent para todas as chamadas relacionadas a anúncios A sequência user-agent é criada usando a mesma sequência UA que o navegador está usando + adicionar sequência Primetime

* **PTPLAY-7675** (interno) Os anúncios transcodificados não estão reproduzindo O reempacotamento criativo estava falhando quando ele foi chamado em uma resposta VMAP ou VAST. A correção é apenas ler o arquivo de mídia do anúncio em vez de ler do ativo no caso de anúncios vastos.

* **PTPLAY-7895** (interno) Quando `allowMultipleAds=false`, nenhum anúncio é reproduzido Corrigido erro onde `allowMultipleAds` parâmetro não estava sendo seguido corretamente.

* **PTPLAY-7896** (interno) Os anúncios estão sendo reproduzidos fora da ordem de sequência em PS4 Corrigido problema onde os anúncios não estavam na ordem em que os anúncios apareciam nas respostas XML.

* O PS4 TVSDK foi testado novamente em um miniaplicativo em vez de em um jogo.

**Versão 2.1.0.563**

* **Zendesk #3868**
O TVSDK é compatível com o Playstation SDK 2.5 O TVSDK agora é integrado ao SDK do Playstation 2.5.

* **Zendesk #4093**
Pares de valores-chave targetingInfo na solicitação de anúncios Pt.\
  Um caractere de nova linha que separa os pares chave/valor foi adicionado.

## Recursos compatíveis {#supported-features}

Os seguintes recursos são suportados no TVSDK 2.1 para PlayStation 4:

**Versão 2.1.0.621**

* Fallback de anúncios, encadeamento de Daisy na lógica de seleção de anúncios (Zendesk #3103) Para anúncios VAST (criações) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo MIME inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback

**Versão 2.1.0.538**

* Reprodução de VOD do HLS, incluindo reproduzir, pausar, buscar
* Transmissão adaptável da taxa de bits
* Reprodução de conteúdo criptografado com conteúdo protegido por Primetime DRM e AES padrão
* Inserção de anúncios no lado do cliente com comportamentos de anúncio padrão e perdão de anúncios
* Reempacotamento criativo
* Legendas ocultas WebVTT
* Instantâneo com posição inicial personalizada
* Jogo de truques com avanço rápido e retrocesso rápido
* redirecionamento 302

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
