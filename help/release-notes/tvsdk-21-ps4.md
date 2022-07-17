---
title: Notas de versão do TVSDK 2.1 PlayStation 4
description: As Notas de versão do TVSDK 2.1 para PlayStation 4 descrevem os recursos compatíveis e os problemas conhecidos no TVSDK 2.1 PlayStation 4 .
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 32af3fe4-c730-41f6-a558-987bd14c9bae
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
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
Quando o link de anúncio do wrapper VMAP estava quebrado, o reprodutor estava ficando preso no estado Preparando (não estava enviando) 
`onComplete` para o chamador).

* **PTPLAY-10179:**

   `creativeRepackaging` e `fallbackOnInvalidCreative` agora estão desligados por padrão. Além disso, quando a variável `creativeRepackaging` sinalizador foi definido, mas não `creativeRepackaging` foi fornecido, a variável `onRepackagingComplete` O estava sendo chamado tantas vezes quanto havia anúncios no ad break, fazendo com que os ad breaks fossem criados várias vezes.

* **Zendesk nº 10304**: A variável de ativação/desativação do anúncio forveness não foi inicializada. Agora inicializamos a variável de `DataSetEntry's` ctor.

* **PTPLAY-10318:**
O suporte para o modo em segundo plano foi introduzido.
* **Zendesk # 17409:**
Ao entrar no modo de reprodução de truque, em seguida, voltar ao modo de reprodução normal e, em seguida, entrar novamente no modo de reprodução de truque, a posição da reprodução estava pulando.
* **PTPLAY-9552:**
Após analisar os arquivos XML de resposta, o código de erro 1108 agora é pingado sempre que não há anúncios presentes.
* **PTPLAY-9551:**
Quando não há interrupção de anúncio após o processamento do Auditude, o CRS chama 
**onPrefetchComplete** que diminui groupCount. Como não há ad break, a variável **groupCount** é 0 e diminuído em 1. Anteriormente, o **groupCount** was **uint32_t** devido ao qual costumava mudar para o valor máximo. Isso é agora **int32_t**.

**Versão 2.1.0.621**

* **Zendesk nº 4555**
Instantâneo em problemas de memória com erros de carregamento à esquerda - 
`MediaItemLoader` Correção de falha ao lançar `mediaitemloader`

* **Zendesk nº 17223**
CSAI 2.x: Nem todos os URLs de rastreamento de anúncios são acionados
   * Alguns anúncios VAST, que, por sua vez, apontavam para um anúncio em linha, não possuíam urls de rastreamento.
   * Quando há várias marcas de impressão em um anúncio no VAST XML, somente o primeiro url de impressão foi salvo e o restante foi ignorado. Agora, todos os urls de impressão serão salvos e colados posteriormente.
* **Zendesk nº 17224**
O agente do usuário PS4 move informações do tempo de vida para o fim da UAString
* **Zendesk nº 17226**
CSAI 2.x: Nem todos os anúncios compilados.
\
   Correção para indicar que a linha do tempo foi alterada devido às operações insertBy ou apagarBy e fazer a mudança de período de acordo.

* **Zendesk nº 17284**
   [Todas as plataformas] As legendas ocultas não são exibidas.\
   HLS - suporte para o `EXT-X-MEDIA-TIME` para arquivos de legenda VTT.

* **Zendesk nº 17889**
Reprodução &quot;leitosa&quot; no PS4
\
   yoffset correto aplicado (para conversão de cores)

* **Zendesk nº 17954**
Lógica de fallback de anúncio + manuseio de conteúdo vazio
\
   Correção do problema se um dos invólucros Vast estava vazio, o analisador Vast usado para continuar processando o invólucro.

* **Zendesk nº 17807**
Não é possível ultrapassar o vasto vazio do mesmo que o Zendesk nº 3103

* **Zendesk nº 17865**
Lógica de fallback no PS4 e XBox One
\
   Igual ao Zendesk nº 3103

**Versão 2.1.0.591**

* **Zendesk nº 3767**
Snippet do código do anúncio PS4, a resolução do anúncio falha ao processar redirecionamentos do VMAP.
* **Zendesk nº 4096**
PS4 CSAI: Falha de segmentação Correção de falha quando o TVSDK gera falha de segmentação quando a biblioteca de anúncios está processando uma resposta VMAP.

* **Zendesk nº 4161**
O Trickplay 16x no final do filme congela o deadlock fixo que ocorria quando a reprodução de trickplay retorna à reprodução normal

* **Zendesk nº 4208**
Travamento aleatório quando as legendas ocultas são ativadas em Vazamento de memória fixa quando as legendas ocultas são ativadas

* **Zendesk nº 4213**
PS4 CSAI: Alterar a sequência padrão do agente do usuário para todas as chamadas relacionadas a anúncios A sequência de agente do usuário é criada usando a mesma sequência de caracteres UA que o navegador está usando + adicionar cadeia de caracteres do Primetime

* **PTPLAY-7675** (interno) Os anúncios transcodificados não estão reproduzindo o Reempacotamento Criativo estava falhando quando foi chamado em uma resposta VMAP ou VAST. A correção é apenas ler o arquivo de mídia do anúncio em vez de ler do ativo no caso de anúncios grandes.

* **PTPLAY-7895** (interno) Quando `allowMultipleAds=false`, nenhum anúncio reproduzir o erro fixo em que `allowMultipleAds` não estava sendo seguido corretamente.

* **PTPLAY-7896** (interno) Os anúncios estão sendo reproduzidos da ordem de sequência no problema PS4 Fixo, em que os anúncios não estavam na ordem em que apareciam nas respostas XML.

* PS4 TVSDK retestado em um mini aplicativo em vez de jogo.

**Versão 2.1.0.563**

* **Zendesk nº 3868**
O TVSDK é compatível com o SDK do Playstation 2.5 O TVSDK agora é criado com o SDK do Playstation 2.5.

* **Zendesk nº 4093**
pares de valores-chave targetingInfo na solicitação de anúncios de página.
\
   Um caractere de nova linha que separa os pares chave/valor foi adicionado.

## Recursos compatíveis {#supported-features}

Os seguintes recursos são compatíveis com o TVSDK 2.1 para PlayStation 4:

**Versão 2.1.0.621**

* Fallback de anúncio, encadeamento de margarida na lógica de seleção de anúncio (Zendesk #3103) Para anúncios VAST (criações) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo MIME inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar.Você pode configurar alguns aspectos do comportamento de fallback

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

* Consulte a documentação completa de ajuda em [Aprendizagem e suporte do Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
