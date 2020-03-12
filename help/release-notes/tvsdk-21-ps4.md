---
title: Notas de versão do TVSDK 2.1 PlayStation 4
seo-title: Notas de versão do TVSDK 2.1 PlayStation 4
description: As notas de versão do TVSDK 2.1 para PlayStation 4 descrevem os recursos compatíveis e os problemas conhecidos no TVSDK 2.1 PlayStation 4.
seo-description: As notas de versão do TVSDK 2.1 para PlayStation 4 descrevem os recursos compatíveis e os problemas conhecidos no TVSDK 2.1 PlayStation 4.
uuid: 494569cf-07e2-476a-b88e-e46c9cca4cdc
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: ebfc8819-f5a9-47a2-b454-0e4e6f9e4640
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Notas de versão do TVSDK 2.1 PlayStation 4 {#tvsdk-playstation-release-notes}

As notas de versão do TVSDK 2.1 para PlayStation 4 descrevem os recursos compatíveis e os problemas conhecidos no TVSDK 2.1 PlayStation 4.

## Problemas resolvidos {#resolved-issues}

Estes são os problemas resolvidos para TVSDK 2.1 para PlayStation 4:

**Versão 2.1.0.638**

* **PTPLAY-10439:**
Quando o link do anúncio do invólucro VMAP estava quebrado, o player estava ficando preso no estado Preparando (não estava sendo enviado `onComplete` ao chamador).

* **PTPLAY-10179:**
   `creativeRepackaging` e `fallbackOnInvalidCreative` os valores agora estão desativados por padrão. Além disso, quando o `creativeRepackaging` sinalizador foi definido, mas nenhum `creativeRepackaging` formato foi fornecido, o `onRepackagingComplete` estava sendo chamado quantas vezes mais que havia anúncios no intervalo do anúncio, fazendo com que os intervalos fossem criados várias vezes.

* **Zendesk #10304**:
A variável de ativação/desativação do anúncio não foi inicializada. Agora inicializamos a variável do `DataSetEntry's` operador.

* **PTPLAY-10318:**
O suporte para o modo em segundo plano foi introduzido.
* **Zendesk # 17409:**
Ao entrar no modo de reprodução de truque, em seguida, voltar ao modo de reprodução normal e, em seguida, entrar novamente no modo de reprodução de truque, a posição de reprodução estava pulando.
* **PTPLAY-9552:**
Depois de analisar os arquivos XML de resposta, o código de erro 1108 agora é pingado sempre que não há anúncios presentes.
* **PTPLAY-9551:**
Quando não há quebra de anúncio após o processamento do Auditude, o CRS chama **onPrefetchComplete** , o que diminui o groupCount. Como não há quebra de anúncio, **groupCount** é 0 e decrementado em 1. Anteriormente, **groupCount** era **uint32_t** por causa do qual costumava ser alterado para valor máximo. Agora é **int32_t**.

**Versão 2.1.0.621**

* **Zendesk #4555** Instant on Memory emite erros de carregamento principais - `MediaItemLoader` Correção de falha ao liberar `mediaitemloader`

* **Zendesk #17223** 2.x CSAI: Nem todos os URLs de rastreamento de anúncio são disparados
   * Alguns anúncios VAST que, por sua vez, apontavam para um anúncio embutido estavam sem URL de rastreamento.
   * Quando há várias marcas de impressão em um anúncio no XML VAST, somente o primeiro url de impressão foi salvo e o restante foi ignorado. Agora todos os urls de impressão serão salvos e colados posteriormente.
* **O agente do usuário do Zendesk #17224** PS4 move as informações do horário de funcionamento para o fim do UAString
* **Zendesk #17226** 2.x CSAI: Nem todos os anúncios costurados.\
   A correção indica que a linha do tempo foi alterada devido às operações insertBy ou eraseBy e que o período muda de acordo.

* **Zendesk #17284**
   [Nem todas as plataformas] As legendas ocultas são exibidas.\
   HLS - suporte para a `EXT-X-MEDIA-TIME` tag para arquivos de legenda VTT.

* **Zendesk #17889** Reprodução &quot;Látea&quot; no PS4\
   yoffset correto aplicado (para conversão de cores)

* **Zendesk #17954** Ad fallback logic + manuseio vazio e vasto\
   Corrigido o problema se um dos invólucros Vast estava vazio, o analisador Vast usado para continuar processando o invólucro.

* **Zendesk #17807** Não consegue ultrapassar o vasto vazioIgual ao Zendesk #3103

* **Zendesk #17865** Fallback Logic em PS4 e XBox One\
   Igual ao Zendesk #3103

**Versão 2.1.0.591**

* **Trecho de código de anúncio do Zendesk #3767** PS4, a resolução de anúncio falha ao processar redirecionamentos do VMAP.
* **Zendesk #4096** PS4 CSAI: Falha de segmentaçãoCorrigida falha quando o TVSDK gerava falha de segmentação quando a biblioteca de publicidade processava uma resposta VMAP.

* **Zendesk #4161** Trickplay 16x no final do filme congelaBloqueio corrigido que ocorria quando o trickplay retornava à reprodução normal

* **Zendesk #4208Falha** aleatória quando as legendas ocultas estão ativadasLiberação de memória fixa quando as legendas ocultas estão ativadas

* **Zendesk #4213** PS4 CSAI: Alterar a string padrão user-agent para todas as chamadas relacionadas a anúnciosA string user-agent é criada usando a mesma string UA que o navegador está usando + adicionar a string Primetime

* **PTPLAY-7675** (interno)Anúncios transcodificados não estão sendo reproduzidosA reembalagem da Creative falhou quando chamada em uma resposta VMAP ou VAST. A correção é apenas ler o arquivo mediático do anúncio em vez de ler do ativo no caso de grandes anúncios.

* **PTPLAY-7895** (interno)Quando `allowMultipleAds=false`, nenhum anúncio é reproduzidoCorrigido o erro no qual o `allowMultipleAds` parâmetro não estava sendo seguido corretamente.

* **PTPLAY-7896** (interno) Os anúncios estão sendo reproduzidos fora da ordem de sequência em um problema PS4Fixed no qual os anúncios não estavam na ordem em que apareciam nas respostas XML.

* PS4 TVSDK testado novamente em um mini aplicativo em vez de um jogo.

**Versão 2.1.0.563**

* **Zendesk #3868** A TVSDK oferece suporte ao Playstation SDK 2.5O TVSDK agora é criado com o SDK 2.5 Playstation.

* **Zendesk #4093** targetingInformações pares de valor chave na solicitação de anúncios publicitários.\
   Um caractere de nova linha que separa os pares de chave/valor foi adicionado.

## Recursos suportados {#supported-features}

Os seguintes recursos são suportados no TVSDK 2.1 para PlayStation 4:

**Versão 2.1.0.621**

* Ad Fallback, Encadeamento gradual na lógica de seleção de anúncio (Zendesk #3103)Para anúncios VAST (criativos) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo MIME inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar.Você pode configurar alguns aspectos do comportamento de fallback

**Versão 2.1.0.538**

* Reprodução VOD HLS, incluindo reprodução, pausa, busca
* Streaming adaptável de taxa de bits
* Reprodução de conteúdo criptografado com conteúdo protegido por AES Primetime DRM e baunilha
* Inserção de anúncio do cliente com comportamentos de anúncio padrão e perdão de anúncios
* Reembalagem criativa
* Legendas de WebVTT fechadas
* Instantâneo com posição inicial personalizada
* Brincar com avanço rápido e retrocesso rápido
* Redirecionamento 302

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página Aprendizagem e suporte [do](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.