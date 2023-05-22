---
title: Glossário do Account IQ
description: Um glossário de terminologias de produtos.
exl-id: 2ee54442-9538-4c30-b999-265310b3935f
source-git-commit: 4eb5ba53fb3e0a0c314695fcd30cf15c7242b53c
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 0%

---

# Conceitos e glossário do produto {#glossary}

Consulte as terminologias de produto a seguir e suas definições.

## Probabilidade de Compartilhamento de Contas {#account-sharing-probability-def}

Um painel de painel com gráficos que dividem os segmentos atuais que compartilham pontuações em categorias de intervalo de compartilhamento Muito baixo, Baixo, Moderado, Alto e Muito alto.

## Ação {#action-def}

Um evento direto ou indireto associado a um [Operação](#operation-def) que afeta as características (por exemplo, pontuação de compartilhamento ou número de dispositivos em uso) de um segmento de operação relacionado (ou coorte).

## Pontuação de compartilhamento agregada {#sharing-probability-level-def}

Um painel de painel com gráficos que dividem os segmentos atuais que compartilham pontuações em categorias de intervalo de compartilhamento Muito baixo, Baixo, Moderado, Alto e Muito alto, juntamente com cada porcentagem de categorias da quantidade total de streaming do segmento.

## AuthN {#authn-def}

Autenticação ou o número de tentativas de autenticação. Uma tentativa de autenticação é o processo pelo qual um usuário sem um estado de autenticação válido no momento é redirecionado para o MVPD escolhido, onde se identifica para o MVPD - normalmente com um nome de usuário e senha.

## AuthN OK {#authn-ok-def}

O número de autenticações bem-sucedidas. Uma autenticação bem-sucedida ocorre quando uma identificação de usuários é confirmada por um MVPD e resulta no redirecionamento do usuário para o aplicativo ou site do programador.

## AuthZ {#authz-def}

Autorização ou o número da solicitação de autorização. Uma solicitação de autorização é o processo pelo qual um programador solicita permissão de um MVPD por meio do Adobe para começar a transmitir o conteúdo solicitado por um usuário. O MVPD normalmente concede a solicitação com base nos direitos de conteúdo associados à assinatura do MVPD do usuário (por exemplo, se o canal associado ao conteúdo está na assinatura do usuário). Algumas respostas de solicitação de autorização são armazenadas em cache pelo Adobe, o que permite que o Adobe responda imediatamente sem transmitir a solicitação para o MVPD.

## AuthZ OK {#authz-ok-def}

O número de autorizações bem-sucedidas.

## Canal {#channel-def}

O canal, também conhecido como Propriedade, é uma fonte de conteúdo de vídeo relacionada a temas. Tradicionalmente, representa um feed de vídeo contínuo distinto, endereçável numericamente, de um MVPD. O canal mapeia diretamente para um canal acessível de conteúdo disponível para os assinantes por meio do Set Top Box (STB).

## Cluster {#cluster-def}

Um cluster é uma coleção de locais e dispositivos. Os clusters são criados encontrando locais comuns entre dispositivos. Os dispositivos que foram vistos em um local comum serão considerados como pertencentes ao mesmo cluster. Dois dispositivos podem estar no mesmo cluster, mesmo que não tenham locais comuns, mas podem ser conectados por meio dos locais de outros dispositivos.

### Cluster móvel {#mobile-cluster-def}

Um cluster que não tem dispositivos estáticos.

### Cluster estático {#static-cluster-def}

Um cluster que tenha pelo menos um dispositivo estático.

## Simultaneidade {#consurrency-def}

O simultâneo é definido por dois (ou mais) fluxos reproduzidos ao mesmo tempo ou muito próximo no tempo, de modo que o intervalo entre eles não pode ser justificado por viajar a uma velocidade normal.
O uso simultâneo é calculado usando a velocidade máxima (milhas/hora) entre 2 clusters diferentes. Considera-se que um utilizador tem utilização simultânea se tiver uma velocidade superior a 124 m/h a uma distância inferior a 124 milhas ou se tiver uma velocidade superior a 400 m/h a uma distância superior a 124 milhas. A distância é calculada entre locais de clusters diferentes. O uso simultâneo é permitido no mesmo cluster.

## Dispositivo {#device-def}

Um produto de hardware de vídeo digital com capacidade para reproduzir conteúdo da TV em todos os locais e com suporte do Adobe Pass. Por exemplo, smartphones, notebooks e desktops, consoles de jogos e televisões inteligentes.

## Extensão geográfica {#geographical-span-def}

A distância entre os pontos mais distantes em um conjunto de locais.

## Granularidade {#granularity-def}

Em referência ao período, o tamanho do período; como uma semana ou um mês.

## Índice médio da indústria {#industry-avg-index-def}

Um valor calculado para cada um dos Índices de Risco (Contas, Uso, Geral) entre todos os Programadores e MVPDs durante o período selecionado.

## IP {#ip-def}

O endereço de protocolo IP atribuído a um dispositivo por um provedor de serviços de Internet. Por exemplo, provedor de serviços de cabo e provedor de serviços de célula.

## Modo de isolamento {#isolation-mode-def}

Um tipo de análise de compartilhamento em que a avaliação de uma conta é limitada a eventos que ocorreram diretamente nos programadores no segmento selecionado.  Normalmente, todos os eventos de conta são avaliados, o que fornece uma estimativa muito mais precisa de compartilhamento.  Alguns dados do MVPD são estruturados de uma maneira que permite apenas a análise do Modo de isolamento.

## Localização {#location-def}

Um ponto único na Terra. Também é chamada de geolocalização para uma solicitação de reprodução específica, detectada com os dados Pass, com uma precisão de 1000 mx1000 m (um km quadrado).

<!-- ### Home location {#home-location-def}

the precision is 0.01 ~ 2000mx2000m (4 square km) - at this moment the home location is detected using an ML algo, based on data provided by two mvpds. The probability is ~ 80%. We are not using the zip code for the majority of the users. Currently, this information is not used in assessing the sharing probability. -->

## Empresa de mídia {#media-company-def}

Media Company é uma empresa proprietária de um grupo de redes de mídia.

## Métrica {#metric}

Métrica é um atributo da conta do assinante (por exemplo, o MVPD, os programadores e canais do conteúdo transmitido, o número de dispositivos usados).

## Dispositivo móvel {#mobile-device-def}

Um dispositivo com alta mobilidade. Por exemplo, celular e tablet.

## MVPD {#mvpd-def}

O MVPD, também conhecido como Distribuidor, é agregador, revendedor e distribuidor de conteúdo de vídeo da Media Company.

## Operação {#operation-def}

A operação é um registro criado para rastrear o efeito de um determinado [ação](#action-def) em um segmento associado. Um exemplo de ação pode ser um limite colocado no número de fluxos simultâneos permitidos para contas identificadas pelo segmento.

## Pontuação geral de compartilhamento {#overall-sharing-score}

Um valor que ajuda os usuários a entender a magnitude do compartilhamento de senhas em propriedades do Programador ou por assinantes do MVPD e fornece a eles um senso de urgência para agir em relação a ele.

<!--**Aggregated Risk Index**
Also known as Risk Index and Sharing Risk Index, it is a value that helps users understand the magnitude of password sharing on Programmer properties or by MVPD subscribers and provides them a sense of urgency to act upon it.-->

<!--**Risk Index - Overall**
A value computed as an average of "Risk Index - Accounts" and the "Risk Index - Usage". Overall Sharing Risk Index-->

## Solicitação de reprodução {#play-requests-def}

Uma solicitação feita por um aplicativo cliente ou site para o Adobe para solicitar um token de mídia para gravar e proteger um início de fluxo.

## Programador {#programmer-def}

Programmer, também conhecida como Network, é uma empresa que é subsidiária de uma empresa maior (corporação) que possui e gerencia um ou mais canais.

## requestorID {#requestorid-def}

A ID que uma Empresa de mídia usa para identificar a si mesma ou a uma subsidiária de um MVPD.  Dependendo da implementação do Programador, isso pode mapear para uma Empresa de mídia, Programador ou Canal.  A mais comum. A ID que uma Empresa de mídia usa para se identificar ou uma subsidiária de um MVPD.  Dependendo da implementação do Programador, isso pode mapear para uma Empresa de mídia, Programador ou Canal.  Tradicionalmente, isso é mapeado para um Canal.  Com a criação de pseudo-canais como MML (March Madness Live) e movimentações tecnicamente orientadas para lidar com limitações de dados orientadas por MVPD, requestorID está começando a se tornar mais associado com a Media Company.

## resourceID {#resource-id-def}

O conteúdo solicitado pelo usuário final.  Tradicionalmente, isso identificou o Canal associado ao conteúdo que o usuário solicitou.  As melhorias no sistema permitem que a ID represente programas específicos (por exemplo, com classificações específicas), a ID continua identificando o Canal associado.

## Índice de risco - Utilização {#risk-index-usage}

Também conhecido como Uso de contas compartilhadas, é um valor calculado com base no número de solicitações de reprodução feitas por cada conta ponderadas pela probabilidade de compartilhamento de cada conta. Também é conhecido como Uso pelo Índice de Risco de Contas Compartilhadas.

## Segmento {#segmet-def}

Segmento é um conjunto de contas que atendem às condições definidas pelo usuário especificadas pelas métricas selecionadas (por exemplo, &quot;usuários de MVPD A, B, C, D ou E que assistiram aos canais X, Y ou Z&quot;).

## Nível de compartilhamento {#sharing-level-def}

Também conhecido como Índice de Risco - Contas ou Índice de Risco de Contas Compartilhadas, é um valor calculado com base em uma média da probabilidade de compartilhamento calculada para cada conta no conjunto de MVPDs selecionados que transmitiu de um dos Canais do programador selecionados durante o intervalo de tempo selecionado.

## Dispositivo estático {#static-device-def}

Um dispositivo com baixa mobilidade. Por exemplo, console de jogos, decodificador de sinais e televisor.

## Período de tempo {#time-frame-def}

Também conhecida como Período ou Fenda de Tempo, é a janela de tempo que contém a atividade de solicitação de reprodução representada na interface do usuário e nas tabelas do início ao fim.

## Principais MVPDs no segmento {#top-mvpds-def}

Os principais (no máximo 10) MVPDs no segmento selecionado são medidos pelo nível de compartilhamento, Uso de contas compartilhadas ou Pontuação geral de compartilhamento.

## Tendência {#trend-def}

A diferença de porcentagem na métrica associada (por exemplo, porcentagem do total de solicitações de reprodução) entre o período atual e o anterior.

## Assinantes únicos {#unique-subscriber-def}

O número de contas MVPD exclusivas por um determinado período que interagiram com aplicativos ou sites programadores da TV Everywhere envolvendo o Adobe Pass por um determinado período.  Essa interação inclui qualquer atividade no aplicativo ou site do programador que resulte em uma chamada para um serviço do Adobe Pass. Por exemplo, verificar o estado de authN ou authZ, autenticação e autorização. O número total de assinantes únicos também incluirá o número de dispositivos exclusivos se o uso de Adobe TempPass por programadores (ou seja, pré-visualização gratuita) fizer parte do segmento.

## Uso {#usage-defs}

### Usuário ávido {#avid-user-def}

Mais de 37 solicitações de reprodução por mês.

### Usuário pouco frequente {#infrequent-users-def}

Menos de 9 solicitações de reprodução por mês.

### Usuário normal {#regular-user-def}

De 9 a 37 solicitações de reprodução por mês.

## Padrão de uso {#usage-patern-def}

Um de um conjunto finito de rótulos de categoria aplicados a uma conta que melhor caracteriza os usuários da conta em termos de grupos sociais ou comportamentos (por exemplo, uma pequena família, um viajante ou viajante, compartilhamento social etc.).

## Código postal {#zip-code-def}

O CEP dos EUA associado a locais dentro dos EUA
