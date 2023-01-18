---
title: Glossário do Account IQ
description: Um glossário de terminologias de produtos.
exl-id: 2ee54442-9538-4c30-b999-265310b3935f
source-git-commit: 4eb5ba53fb3e0a0c314695fcd30cf15c7242b53c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Conceitos e glossário de produto {#glossary}

Consulte as terminologias de produto a seguir e suas definições.

## Probabilidade de compartilhamento de contas {#account-sharing-probability-def}

Um painel de painel com gráficos que divide as pontuações de compartilhamento dos segmentos atuais em categorias de intervalo de Muito baixa, Baixa, Moderada, Alta e Muito alta.

## Ação {#action-def}

Um evento direto ou indireto associado a um [Operação](#operation-def) que afeta as características (por exemplo, Pontuação de compartilhamento ou número de dispositivos em uso) de um segmento de operação relacionado (ou coorte).

## Pontuação de compartilhamento agregada {#sharing-probability-level-def}

Um painel de painel com gráficos que divide as pontuações de compartilhamento dos segmentos atuais em categorias de intervalo de Muito baixa, Baixa, Moderada, Alta e Muito alta, juntamente com cada porcentagem da quantidade total de streaming do segmento.

## AuthN {#authn-def}

Autenticação ou o número de tentativas de autenticação. Uma tentativa de autenticação é o processo pelo qual um usuário sem um estado de autenticação atualmente válido é redirecionado para o MVPD escolhido, onde ele se identifica com o MVPD - normalmente com um nome de usuário e senha.

## AuthN OK {#authn-ok-def}

O número de autenticações bem-sucedidas. Uma autenticação bem-sucedida ocorre quando um usuário identifica é confirmado por um MVPD e resulta no redirecionamento do usuário para o aplicativo programador ou site.

## AuthZ {#authz-def}

Autorização ou o número de pedidos de autorização. Uma solicitação de autorização é o processo pelo qual um programador solicita permissão de um MVPD por meio do Adobe para começar a transmitir o conteúdo solicitado de um usuário. O MVPD normalmente concede a solicitação com base nos direitos de conteúdo associados à assinatura MVPD do usuário (por exemplo, se o canal associado ao conteúdo está na assinatura do usuário). Algumas respostas de solicitação de autorização são armazenadas em cache pelo Adobe, o que permite que o Adobe responda imediatamente sem passar a solicitação para o MVPD.

## AuthZ OK {#authz-ok-def}

O número de autorizações bem-sucedidas.

## Canal {#channel-def}

O Canal, também conhecido como Propriedade, é uma fonte relacionada temática de conteúdo de vídeo. Tradicionalmente representando um feed de vídeo contínuo distinto e endereçável numericamente de um MVPD. O canal mapeia diretamente para um canal acessível de conteúdo disponível para os assinantes por meio de seu Set Top Box (STB).

## Cluster {#cluster-def}

Um cluster é uma coleção de locais e dispositivos. Os clusters são criados localizações comuns entre dispositivos. Os dispositivos que foram vistos em um local comum serão considerados como pertencendo ao mesmo cluster. Dois dispositivos podem estar no mesmo cluster, mesmo que não tenham locais comuns, mas possam ser conectados por meio dos locais de outros dispositivos.

### Cluster móvel {#mobile-cluster-def}

Um cluster que não tem dispositivos estáticos.

### Cluster estático {#static-cluster-def}

Um cluster que tem pelo menos um dispositivo estático.

## Simultaneidade {#consurrency-def}

O concorrente é definido por dois (ou mais) fluxos reproduzidos ao mesmo tempo ou muito próximos no tempo, de modo que o intervalo entre eles não possa ser justificado por viagens a uma velocidade normal.
A utilização simultânea é calculada utilizando a velocidade máxima (milhas/hora) entre dois clusters diferentes. Considera-se que um utilizador tem utilização simultânea se tiver uma velocidade superior a 124 m/h numa distância inferior a 124 milhas ou se tiver uma velocidade superior a 400 m/h numa distância superior a 124 milhas. A distância é calculada entre localizações de diferentes clusters. O uso simultâneo é permitido no mesmo cluster.

## Dispositivo {#device-def}

Um produto de hardware de vídeo digital capaz de reproduzir conteúdo de TV em qualquer lugar e compatível com o Adobe Pass. Por exemplo, smartphones, laptop e desktop, consoles de jogos e televisões inteligentes.

## Span Geográfico {#geographical-span-def}

A distância entre os pontos mais distantes em um conjunto de locais.

## Granularidade {#granularity-def}

Em referência ao período, a dimensão do período; como uma semana ou um mês.

## Índice médio da indústria {#industry-avg-index-def}

Um valor calculado para cada um dos Índices de Risco (Contas, Uso, Geral) em todos os Programadores e MVPDs durante o período de tempo selecionado.

## IP {#ip-def}

O endereço do Protocolo de Internet atribuído a um dispositivo por um Provedor de Serviços de Internet. Por exemplo, provedor de serviço por cabo e provedor de serviço de célula.

## Modo de isolamento {#isolation-mode-def}

Um tipo de análise de compartilhamento em que a avaliação de uma conta é limitada a eventos que ocorreram diretamente nos programadores no segmento selecionado.  Normalmente, todos os eventos de conta são avaliados, o que fornece uma estimativa de compartilhamento muito mais precisa.  Alguns dados MVPD são estruturados de uma maneira que permite apenas a análise do Modo de isolamento.

## Localização {#location-def}

Um ponto único na Terra. Também é chamada de geolocalização para uma solicitação de reprodução específica, detectada por meio dos dados Pass, com precisão de 1000mx1000m (um km quadrado).

<!-- ### Home location {#home-location-def}

the precision is 0.01 ~ 2000mx2000m (4 square km) - at this moment the home location is detected using an ML algo, based on data provided by two mvpds. The probability is ~ 80%. We are not using the zip code for the majority of the users. Currently, this information is not used in assessing the sharing probability. -->

## Empresa de mídia {#media-company-def}

Empresa de mídia é a empresa proprietária de um grupo de redes de mídia.

## Métrica {#metric}

Métrica é um atributo da conta do assinante (por exemplo, o MVPD, os programadores e canais do conteúdo que fazem stream, o número de dispositivos que usam).

## Dispositivo móvel {#mobile-device-def}

Um dispositivo com alta mobilidade. Por exemplo, celular e tablet.

## MVPD {#mvpd-def}

O MVPD, também conhecido como Distribuidor, é agregador, revendedor e distribuidor de conteúdo de vídeo da Empresa de mídia.

## Operação {#operation-def}

Operação é um registro criado para rastrear o efeito de um [ação](#action-def) em um segmento associado. Um exemplo de ação pode ser um limite colocado no número de fluxos simultâneos permitidos para contas identificadas pelo segmento.

## Pontuação de compartilhamento geral {#overall-sharing-score}

Um valor que ajuda os usuários a entender a magnitude do compartilhamento de senha nas propriedades do Programador ou pelos assinantes do MVPD e lhes fornece um senso de urgência para agir de acordo com ele.

<!--**Aggregated Risk Index**
Also known as Risk Index and Sharing Risk Index, it is a value that helps users understand the magnitude of password sharing on Programmer properties or by MVPD subscribers and provides them a sense of urgency to act upon it.-->

<!--**Risk Index - Overall**
A value computed as an average of "Risk Index - Accounts" and the "Risk Index - Usage". Overall Sharing Risk Index-->

## Reproduzir solicitação {#play-requests-def}

Uma solicitação feita por um aplicativo cliente ou site para o Adobe para solicitar um token de mídia para registrar e proteger um início de fluxo.

## Programador {#programmer-def}

Programmer, também conhecida como Network, é uma empresa subsidiária de uma empresa maior (corporação) que detém e gerencia um ou mais canais.

## requestorID {#requestorid-def}

A ID que uma empresa de mídia usa para se identificar ou para uma subsidiária de um MVPD.  Dependendo da implementação do Programador, isso pode mapear para uma Empresa de mídia, Programador ou Canal.  A ID mais comum que uma empresa de mídia usa para identificar a si mesma ou a uma subsidiária de um MVPD.  Dependendo da implementação do Programador, isso pode mapear para uma Empresa de mídia, Programador ou Canal.  Tradicionalmente, isso mapeava para um Canal.  Com a criação de pseudo-canais como MML (Março Madness Live) e as iniciativas técnicas para lidar com limitações de dados orientadas por MVPD, o requestorID está começando a se associar mais à Empresa de mídia.

## resourceID {#resource-id-def}

O conteúdo solicitado pelo usuário final.  Tradicionalmente, isso identificou o Canal associado ao conteúdo que o usuário solicitou.  Os aprimoramentos do sistema permitem que a ID represente programas específicos (por exemplo, com classificações específicas), e a ID continua a identificar o Canal associado.

## Índice de risco - Utilização {#risk-index-usage}

Também conhecido como Uso de contas compartilhadas, é um valor calculado com base no número de solicitações de reprodução feitas por cada conta, ponderado pela probabilidade de compartilhamento de cada conta. Também é conhecido como Uso por Índice de Risco de Contas Compartilhadas.

## Segmento {#segmet-def}

Segmento é um conjunto de contas que atende às condições definidas pelo usuário, especificadas pelas métricas selecionadas (por exemplo, &quot;usuários de MVPD A, B, C, D ou E que assistiram aos canais X, Y ou Z&quot;).

## Nível de compartilhamento {#sharing-level-def}

Também conhecido como Índice de Risco - Contas ou Índice de Risco de Contas Compartilhadas, é um valor calculado com base na média da probabilidade de compartilhamento calculada para cada conta no conjunto de MVPDs selecionados que foi transmitido de um dos Canais de Programador selecionados durante o período selecionado.

## Dispositivo estático {#static-device-def}

Um dispositivo com mobilidade muito baixa. Por exemplo, console de jogos, set top box e televisor.

## Intervalo de tempo {#time-frame-def}

Também conhecida como Período ou Slot de tempo, é a janela de tempo que contém a atividade de solicitação de reprodução representada na interface do usuário e as tabelas do início ao fim.

## Principais MVPDs no segmento {#top-mvpds-def}

Os principais (no máximo 10) MVPDs no segmento selecionado como medida pelo nível de Compartilhamento, Uso de contas compartilhadas ou Pontuação de compartilhamento geral.

## Tendência {#trend-def}

A diferença da porcentagem na métrica associada (por exemplo, a porcentagem do total de solicitações de reprodução) entre o período atual e o anterior.

## Assinantes únicos {#unique-subscriber-def}

O número de contas MVPD exclusivas para um determinado período que interagiram com aplicativos do programador TV em qualquer lugar ou sites que envolveram o Adobe Pass por um determinado período.  Essa interação inclui qualquer atividade no aplicativo programador ou no site que resulta em uma chamada para um serviço da Adobe Pass. Por exemplo, verificar o estado authN ou authZ, autenticar e autorizar. O número total de assinantes únicos também incluirá o número de dispositivos exclusivos se o uso de Adobe TempPass (ou seja, visualização gratuita) por um programador fizer parte do segmento.

## Uso {#usage-defs}

### Usuário do Avid {#avid-user-def}

Mais de 37 solicitações de reprodução por mês.

### Usuário pouco frequente {#infrequent-users-def}

Menos de 9 solicitações de reprodução por mês.

### Usuário regular {#regular-user-def}

De 9 a 37 solicitações de reprodução por mês.

## Padrão de uso {#usage-patern-def}

Um dos conjuntos finitos de rótulos de categoria aplicados a uma conta que melhor caracteriza os usuários da conta em termos de grupos sociais ou comportamentos (por exemplo, uma família pequena, um viajante ou um viajante, compartilhamento social etc.).

## Código Postal {#zip-code-def}

O código postal dos EUA associado a localizações nos EUA
