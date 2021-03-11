---
title: Notas de versão do TVSDK 2.1 PlayStation 4
description: As Notas de versão do TVSDK 2.1 para PlayStation 4 descrevem os recursos compatíveis e os problemas conhecidos no TVSDK 2.1 PlayStation 4 .
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---


# Notas de versão do TVSDK 2.1 PlayStation 4 {#tvsdk-playstation-release-notes}

As Notas de versão do TVSDK 2.1 para PlayStation 4 descrevem os recursos compatíveis e os problemas conhecidos no TVSDK 2.1 PlayStation 4 .

## Problemas resolvidos {#resolved-issues}

Estes são os problemas resolvidos para TVSDK 2.1 para PlayStation 4:

**Versão 2.1.0.638**

* **PTPLAY-10439:**
Quando o link de anúncio do invólucro VMAP estava quebrado, o reprodutor estava ficando preso no estado Preparando (não estava enviando) 
`onComplete` para o chamador).

* **PTPLAY-10179:**

   `creativeRepackaging` Os  `fallbackOnInvalidCreative` valores e agora estão incorretos por padrão. Além disso, quando o sinalizador `creativeRepackaging` era definido, mas nenhum formato `creativeRepackaging` era fornecido, o `onRepackagingComplete` era chamado tantas vezes quanto havia anúncios no ad break, fazendo com que os ad breaks fossem criados várias vezes.

* **Zendesk nº 10304**: A variável de ativação/desativação do anúncio forveness não foi inicializada. Agora inicializamos a variável do operador `DataSetEntry's`.

* **PTPLAY-10318:**
foi introduzido o suporte para o modo em segundo plano.
* **Zendesk # 17409:**
ao entrar no modo de reprodução de truque, em seguida, voltar ao modo de reprodução normal e, em seguida, entrar novamente no modo de reprodução de truque, a posição de reprodução estava pulando.
* **PTPLAY-9552:**
depois de analisar os arquivos XML de resposta, o código de erro 1108 agora é pingado sempre que não há anúncios presentes.
* **PTPLAY-9551:**
Quando não há interrupção de anúncio após o processamento do Auditude, o CRS chama 
**** onPrefetchComplete, que diminui groupCount. Como não há ad break, o **groupCount** é 0 e diminuído em 1. Anteriormente, **groupCount** era **uint32_t**, pelo que costumava alterar para o valor máximo. Agora é **int32_t**.

**Versão 2.1.0.621**

* **Zendesk # 4555**
Instant on Memory Problemas de carregamento inicial - Erros de carregamento instantâneo 
`MediaItemLoader` Correção de falha ao lançar  `mediaitemloader`

* **Zendesk #17223**
2.x CSAI: Nem todos os URLs de rastreamento de anúncios são acionados
   * Alguns anúncios VAST, que, por sua vez, apontavam para um anúncio em linha, não possuíam urls de rastreamento.
   * Quando há várias marcas de impressão em um anúncio no VAST XML, somente o primeiro url de impressão foi salvo e o restante foi ignorado. Agora, todos os urls de impressão serão salvos e colados posteriormente.
* **Zendesk #17224**
Agente do usuário PS4 para mover informações do tempo de vida útil para o fim do UAString
* **Zendesk #17226**
2.x CSAI: Nem todos os anúncios compilados.
\
   Correção para indicar que a linha do tempo foi alterada devido às operações insertBy ou apagarBy e fazer a mudança de período de acordo.

* **Zendesk nº 17284**
   [Todas as ] plataformasAs legendas ocultas não são exibidas.\
   HLS - suporte para a tag `EXT-X-MEDIA-TIME` para arquivos de legenda VTT.

* **Zendesk #17889**
Reprodução &quot;leitosa&quot; no PS4
\
   yoffset correto aplicado (para conversão de cores)

* **Zendesk #17954**
Lógica de fallback de anúncio + manipulação de objetos vazios
\
   Correção do problema se um dos invólucros Vast estava vazio, o analisador Vast usado para continuar processando o invólucro.

* **Zendesk #17807**
Não pode ultrapassar o vasto campo vazio Igual ao Zendesk #3103

* **Zendesk #17865**
Lógica de fallback no PS4 e XBox One
\
   Igual ao Zendesk nº 3103

**Versão 2.1.0.591**

* **Snippet de código de anúncio do Zendesk # 3767**
PS4, a resolução do anúncio falha ao processar redirecionamentos do VMAP.
* **Zendesk #4096**
PS4 CSAI: Falha de segmentação Correção de falha quando o TVSDK gera falha de segmentação quando a biblioteca de anúncios está processando uma resposta VMAP.

* **O Zendesk #4161**
Trickplay 16x no final do filme congela o impasse corrigido que acontecia quando a reprodução de trickplay retorna à reprodução normal

* **Zendesk #4208**
Travamento aleatório quando as legendas ocultas são ativadas Vazamento de memória fixa quando as legendas ocultas são ativadas

* **Zendesk nº 4213**
PS4 CSAI: Alterar a sequência padrão do agente do usuário para todas as chamadas relacionadas a anúncios A sequência de agente do usuário é criada usando a mesma sequência de caracteres UA que o navegador está usando + adicionar cadeia de caracteres do Primetime

* **PTPLAY-7675**  (interno) Os anúncios transcodificados não estão reproduzindo Reempacotamento Criativo estava falhando quando foi chamado em uma resposta VMAP ou VAST. A correção é apenas ler o arquivo de mídia do anúncio em vez de ler do ativo no caso de anúncios grandes.

* **PTPLAY-7895**  (interno) Quando  `allowMultipleAds=false`, nenhum anúncio reproduz um erro fixo, onde o  `allowMultipleAds` parâmetro não estava sendo seguido corretamente.

* **PTPLAY-7896**  (interno) Os anúncios estão sendo reproduzidos da ordem de sequência em um problema PS4 corrigido em que os anúncios não estavam na ordem em que apareciam nas respostas XML.

* PS4 TVSDK retestado em um mini aplicativo em vez de jogo.

**Versão 2.1.0.563**

* **Zendesk #3868**
O TVSDK é compatível com o SDK do Playstation 2.5 O TVSDK agora foi criado com o SDK do Playstation 2.5.

* **Zendesk #4093**
targetingInfo pares de valores-chave na solicitação de anúncios de página.
\
   Um caractere de nova linha que separa os pares chave/valor foi adicionado.

## Recursos compatíveis {#supported-features}

Os seguintes recursos são compatíveis com o TVSDK 2.1 para PlayStation 4:

**Versão 2.1.0.621**

* Fallback do anúncio, encadeamento de margarida na lógica de seleção do anúncio (Zendesk nº 3103)
Para anúncios VAST (criações) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo MIME inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar.Você pode configurar alguns aspectos do comportamento de fallback

**Versão 2.1.0.538**

* Reprodução de VOD do HLS, incluindo reprodução, pausa, busca
* Fluxo adaptável de taxa de bits
* Reprodução de conteúdo criptografado com conteúdo protegido por AES do Primetime DRM e baunilha
* Inserção de anúncio do lado do cliente com comportamentos de anúncio padrão e perdão de anúncios
* Reembalagem criativa
* Legendas ocultas da WebVTT
* Instantâneo com posição inicial personalizada
* Brincadeiras de truque com avanço rápido e retrocesso rápido
* 302 redirecionamento

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .