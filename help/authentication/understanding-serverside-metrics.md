---
title: Como entender as métricas do lado do servidor
description: Como entender as métricas do lado do servidor
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---

# Como entender as métricas do lado do servidor {#understanding-server-side-metrics}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.


## Introdução {#intro}

Este documento descreve as métricas do lado do servidor de autenticação da Adobe Primetime geradas pelo serviço ESM (Entitlement Service Monitoring). Ela não descreve os mesmos eventos vistos na perspectiva do cliente (quais programadores veriam se implementassem um serviço de medição, como o Adobe Analytics, em sua página/aplicativo).  

## Resumo de eventos {#events_summary}

Do ponto de vista do servidor de autenticação da Adobe Primetime, os seguintes eventos são gerados:

* **Eventos gerados no fluxo de autenticação**(Um login real com o MVPD)

   * Notificação de tentativa de AuthN - Isso é gerado quando o usuário é enviado ao site de logon do MVPD.
   * Notificação de AuthN pendente - Se o usuário conseguir fazer logon com seu MVPD, isso será gerado quando o usuário for redirecionado para a autenticação do Primetime.
   * Notificação de AuthN concedida - É gerada quando o usuário retorna ao site do Programador e recuperou com êxito o token de autenticação da autenticação do Primetime. 
* **Fluxo de autorização** (Apenas um cheque de autorização com um MVPD)\
   *Pré-requisito:* Um token AuthN válido
   * Notificação da Tentativa de AuthZ
   * Notificação da AuthZ concedida
* **Solicitação de reprodução bem-sucedida**\
   *Pré-requisito:* Tokens AuthN e AuthZ válidos
   * Notificação de uma verificação com autenticação da Adobe Primetime 
   * Uma solicitação de reprodução requer uma autenticação concedida e uma autorização concedida


O número de usuários únicos é abordado detalhadamente na seção [Usuários únicos](#unique-users) abaixo. Como visão geral, como as respostas de autenticação e autorização concedidas geralmente são armazenadas em cache, as seguintes fórmulas geralmente se aplicam:

* Número de tentativas de AuthN \> Número de AuthN concedidas
* Número de tentativas de AuthZ \> Número de AuthZ concedidas
* Número de tentativas de AuthZ \> Número de AuthN concedidas (geralmente)
* Número de Solicitações de Reprodução Bem-sucedidas \> Número de AuthZ concedidas


### Exemplo {#example}

O exemplo a seguir mostra as métricas do lado do servidor para um mês em uma marca:

| Métrica | MVPD 1 | MVPD 2 | ... | MVPD n | Total | | — | — | — | - | — | — | | Autenticações bem-sucedidas | 1125 | 2892 | | 2203 | SUM(MVP1+...MVPD n) | | Autorizações bem-sucedidas | 2527 | 5603 | | 5904 | SUM(MVP1+...MVPD n) | | Solicitações de reprodução bem-sucedidas | 4201 | 10518 | | 10737 | SUM(MVP1+...MVPD n) | | Usuários únicos | 1375 | 2400 | | 2890 | SUM de todos os usuários para todos os MVPDs deduplicados\* | | Autenticações tentadas | 2147 | 3887 | | 3108 | SUM(MVP1+...MVPD n) | | Autorizações tentadas | 2889 | 6139 | | 6039 | SUM(MVP1+...MVPD n) |

</br>

A desduplicação, nesse caso, não deve ter efeito, pois usuários diferentes do MVPD não devem receber a mesma ID de usuário. Ao fazer uma soma para duas marcas diferentes, mas o mesmo MVPD, o efeito de desduplicação deve ser muito maior.

## Acionadores de evento {#event_triggers}

### Novo usuário - Fluxo completo {#new-user-full-flow}

O gráfico a seguir descreve os eventos e as etapas para um usuário sem token de autenticação (um novo usuário ou um token de autenticação de usuário que expirou):



![](assets/ae-flow-with-events.png)



O fluxo envolve viagens de ida e volta para MVPDs para Autenticação (#5 a \#7) e Autorização (\#11).



Após concluir o fluxo, os tokens de Autenticação e Autorização são armazenados em cache no dispositivo do usuário. Os valores de Time-to-Live (TTL) para tokens de autenticação estão entre 6 horas e 90 dias. Uma expiração de token AuthN força automaticamente uma expiração de token AuthZ. O valor TTL do token de autorização geralmente é de 24 horas.

| Eventos do lado do servidor acionados | <ul><li>Tentativa de autenticação, Autenticação pendente, Autenticação concedida</li><li>Tentativa de autorização, Autorização concedida</li><li>Solicitação de reprodução bem-sucedida</li></ul> |
|---|---|


### Usuário recorrente - Tokens AuthZ e AuthN em cache

Para usuários que têm tokens AuthZ e AuthN válidos em cache, as seguintes etapas ocorrem:


![](assets/ae-flow-tokens-cached-web.png)



Isso é acionado automaticamente ao chamar `getAuthorization()`e envolve apenas verificações com autenticação da Adobe Primetime. O MVPD não está envolvido neste fluxo.


| Eventos do lado do servidor acionados | * Solicitação de reprodução bem-sucedida |
|---|---|


### Usuário recorrente - Tokens AuthN em cache, Token AuthZ expirado

Para usuários que ainda têm tokens AuthN válidos, as seguintes etapas ocorrem:

![](assets/ae-flow-authn-token-cached.png)


Este fluxo envolve uma viagem de ida e volta ao MVPD.


| Eventos do lado do servidor acionados | <ul><li>Tentativa de autorização, Autorização OK</li><li>Solicitação de reprodução bem-sucedida</li> |
|---|---|

## Eventos de autenticação {#authn_events}

### Tentativa de autenticação {#authentication-attempt}

Como ilustrado no diagrama acima, os eventos de autenticação só são acionados quando o usuário faz uma ida e volta para o MVPD; os eventos de autenticação não incluem autenticações de token em cache.

O evento de tentativa de autenticação é acionado após o usuário clicar em um MVPD específico do seletor.

* O primeiro evento no lado do MVPD próximo a isso é o carregamento da página
* A autenticação Adobe Primetime não conta tentativas repetidas do usuário para fazer logon na página MVPD (senha incorreta, tente novamente)
* várias tentativas são contadas como uma tentativa
* Alguns MVPDs também executam a Autorização na etapa Autenticação e o usuário não é redirecionado se a autorização falhar.

### Autenticação pendente {#authentication-pending}

Esse evento ocorre quando o processo de redirecionamento para a autenticação da Adobe Primetime é iniciado.

### Autenticação concedida {#authentication-granted}

O usuário é um assinante conhecido do MVPD, normalmente com uma assinatura de TV paga, mas, às vezes, apenas com acesso à Internet. Uma autenticação bem-sucedida pode ocorrer porque o usuário inseriu explicitamente credenciais válidas com seu MVPD ou porque ele tinha inserido credenciais válidas anteriormente e marcado &quot;lembrar-me&quot; (e a sessão anterior não tinha expirado).

O MVPD, portanto, envia uma resposta positiva à autenticação da Adobe Primetime para a solicitação de autenticação e a autenticação da Adobe Primetime cria um *Token de AuthN*.

* Normalmente, a autenticação é armazenada em cache por um longo período de tempo (um mês ou mais). Devido a isso, os eventos de autenticação não estarão mais presentes até que o token expire e o fluxo seja iniciado novamente.
* Entrar de outro site/aplicativo por meio do Logon único não acionará eventos de autenticação.

 

### Autenticação de Comcast {#comcast-authentication}

O Comcast tem um fluxo AuthN diferente em comparação com o resto dos MVPDs.

Os seguintes recursos descrevem as diferenças:

* **Comportamento do cookie da sessão**: Isso causa uma remoção completa de todos os tokens de autenticação depois que o usuário fecha o navegador. Esse recurso está presente somente na Web. O principal objetivo é garantir que sua sessão Comcast não seja mantida em computadores inseguros/compartilhados. O impacto é que haverá mais tentativas de autenticação / fluxos concedidos do que para o resto dos MVPDs.

* **AuthN por requestorID**: A Comcast não permite que o estado AuthN seja armazenado em cache de uma ID do solicitante para outra. Devido a isso, cada site/aplicativo deve ir para o Comcast para obter um token de autenticação. Além das considerações sobre a experiência do usuário, o impacto, como acima, é que mais tentativas de autenticação/eventos concedidos serão gerados.

* **Autenticação Passiva**: Para melhorar a experiência do usuário, mas ainda manter a funcionalidade AuthN por requestorID, um fluxo de autenticação passivo ocorre em um iFrame oculto. O usuário não verá nada, mas os eventos ainda serão acionados como antes.

Se o usuário clicar em &quot;lembrar-se de mim&quot; na página de logon Comcast, as visitas subsequentes a essa página (em um período de 2 semanas) serão apenas um redirecionamento rápido. Caso contrário, os usuários realmente terão que se autenticar na página.

### Autenticação sem êxito {#unsuccessful-authentication}

Uma autenticação malsucedida não é um evento per-se na autenticação do Adobe Primetime, mas pode ser calculado como a diferença entre tentativas e sucessos.

Na versão de maio de 2013, a autenticação da Adobe Primetime adicionará códigos de erro para Autenticações malsucedidas devido a erros do sistema ou da rede, incluindo erros de DRM (falha no vínculo de token) e erros de LSO (sem espaço para gravar o token etc).

### Taxa de conversão de autenticação {#authenitication-conversion-rate}

Uma métrica interessante que os Programadores podem rastrear é a taxa de conversão de autenticação, calculada como (solicitações AuthN/AuthN concedidas)%.

Algumas observações sobre as métricas:

* Como é uma métrica baseada em eventos, ela não reflete a taxa de conversão de usuário exclusiva - se um usuário tentar oito vezes e tiver sucesso na nona vez - ela refletirá muito mal na taxa de conversão acima.
* Não há como (ainda) na autenticação da Adobe Primetime (no lado do servidor) calcular uma conversão de autenticação baseada exclusiva.
* Se tentativas automáticas de AuthN estiverem presentes no site/aplicativo, isso também distorcerá a métrica acima.

## Eventos de autorização {#authorization_events}

### Tentativa de autorização {#authorization_attempt}

Além de obter um token de autenticação, os usuários também devem obter um token de autorização antes de reproduzir o conteúdo. Isso geralmente acontece após a autenticação ou se o token de autorização expirar. Como essa verificação é feita no lado do servidor (dos servidores de autenticação da Adobe Primetime para os servidores MVPD), o usuário não é obrigado a fazer nada.

### Autorização concedida {#authorization-granted}

Uma &quot;autorização concedida&quot; indica que a assinatura do usuário autenticado inclui a programação solicitada.

Note que nem todos os MVPD suportam uma etapa de autorização separada; para algumas autenticações é equiparado a autorização. O MVPD envia uma resposta bem-sucedida à autenticação da Adobe Primetime para a solicitação AuthZ do backchannel e a autenticação da Adobe Primetime cria um token AuthZ.

* O token AuthZ é armazenado em cache por um período de tempo, normalmente 24 horas Durante esse período, nenhum evento AuthZ será acionado.
* Alguns MVPDs trabalham com Autorizações de Nível de Ativo, outros trabalham com Autorizações de Nível de Canal; - dependendo de qual é usado, mais ou menos eventos AuthZ são disparados. Mesmo para a autorização no nível do canal, o armazenamento em cache está em vigor, portanto, se o mesmo ativo for solicitado em menos de 24 horas, nenhum evento será acionado.

### Autorização negada {#authorization-denied}

Se uma autorização for negada, o usuário autenticado não terá uma assinatura confirmada para a programação solicitada. A causa mais provável é que o canal não faz parte do pacote de assinatura do usuário, mas isso também pode refletir um usuário que tem somente acesso à Internet do MVPD.

Para alguns MVPDs, os usuários são autenticados com êxito mesmo que tenham apenas uma assinatura de Internet do MVPD (sem assinatura de TV paga). Nesse caso, mesmo que o canal para o qual o usuário solicita autorização esteja no pacote base, a autorização será negada.

Alguns MVPDs oferecem mensagens de erro personalizadas para negações de AuthZ que podem incluir ofertas para atualizar seu pacote.


### Taxa de conversão de autorização {#authorization-conversion-rate}

A taxa de conversão de Autenticação pode ser calculada como (solicitações AuthZ / AuthZ concedidas)%.

### Solicitação de reprodução bem-sucedida {#successful-play-request}

Um usuário autenticado e autorizado pode exibir conteúdo protegido.

Após uma solicitação de reprodução bem-sucedida, a autenticação do Adobe Primetime gera um token de mídia de curta duração afirmando que o usuário tem direito a exibir o vídeo solicitado. O Programador usa esse Token de mídia para validar ainda mais o visualizador em potencial. Os tokens de mídia são rastreados como solicitações de reprodução bem-sucedidas.

* A autenticação da Adobe Primetime faz *not* rastreie se a reprodução de vídeo realmente começou após a geração do token de mídia. Por exemplo, se houver uma restrição geográfica no conteúdo, a transação ainda será contada como uma solicitação de reprodução bem-sucedida, mesmo que o fluxo nunca tenha realmente início.
* Como os tokens AuthN e AuthZ armazenam em cache a resposta MVPD por um período de tempo, o evento bem-sucedido da solicitação de reprodução é o evento mais frequente nas métricas.

## Usuários únicos {#unique-users}

### Definição {#definition}

Após uma autenticação bem-sucedida, a autenticação da Adobe Primetime rastreia a existência de um usuário exclusivo, com base no valor de ID de usuário MVPD retornado.  Esse valor é baseado nas informações de logon do usuário, mas não contém informações de identificação pessoal.

Esse valor também é passado para o site/aplicativo no retorno de chamada sendTrackingData.

Esse valor pode ser persistente em todos os dispositivos (o MVPD produz o mesmo valor para um determinado usuário, independentemente de onde o logon ocorre) ou transitório (para cada logon, um novo valor é gerado, que o MVPD mapeia em seu back-end. Normalmente, os valores fornecidos pelos MVPDs para a autenticação da Adobe Primetime são persistentes entre sessões e dispositivos, mas, como observado, a persistência não é garantida nem validada.

Esse valor é usado como uma maneira de calcular os usuários únicos. O valor reportado (por ID/intervalo/MVPD do solicitante) é desduplicado para o intervalo específico. Portanto, a soma dos usuários únicos por dia geralmente é diferente do valor mensal, com o valor mensal tendo o valor menor.

Esse número inclui todos os eventos da autenticação do Adobe Primetime, menos as tentativas de autenticação (que não têm ID de usuário), mas incluindo as autorizações tentadas (e possivelmente com falha).

### Exemplos {#examples}

#### Dia 1 {#day1}

O usuário XYZ vai ao site para assistir a um vídeo.

Eventos disparados:

* Tentativa de AuthN (ainda não há usuário exclusivo)
* AuthN concedido
   * neste ponto, identificamos exclusivamente o usuário com base no que o MVPD retorna, portanto, a contagem diária de usuários únicos é aumentada em 1
   * o token AuthN é armazenado em cache por 30 dias
* Tentativa de AuthZ / evento concedido
   * Token de AuthZ armazenado em cache por 1 dia
* Evento de solicitação de reprodução bem-sucedido

#### Dia 1 (Mais Tarde Em) {#day1-later-on}

O usuário XYZ assiste a outro vídeo.

Eventos disparados:

* Evento de solicitação de reprodução bem-sucedido (o restante é armazenado em cache)
* Sem aumento dos únicos diários ou mensais

#### Dia 3 {#day3}

O usuário XYZ assiste a outro vídeo.

Eventos disparados:

* Tentativa de AuthZ / evento concedido
   * Desde que 1 dia de armazenamento em cache a partir do dia 1 expirou
* Evento de solicitação de reprodução bem-sucedido (o restante é armazenado em cache)
* Usuários únicos diários aumentados em 1 - os únicos mensais ainda são 1

#### Dia 31 {#day31}

O usuário XYZ assiste a outro vídeo.

O mesmo que no dia 1 desde que o armazenamento em cache do AuthN expirou.

Se o mesmo usuário não autorizasse, a contagem mensal de usuários únicos ainda seria aumentada em 1 porque há dois eventos que contêm a ID do usuário - autenticação concedida e tentativa de autorização.

### Logon único (SSO) {#single-sign-on-sso}

Em alguns casos, o número de usuários únicos pode ser maior que o número de autenticações bem-sucedidas. Geralmente, esse é o caso quando muitos usuários chegam via SSO a partir de outros sites/aplicativos e precisam apenas obter autorização no site/aplicativo atual.

### Comparação de usuários únicos do lado do cliente e do lado do servidor {#comparing-client-side-and-server-side-unique-users}

Se o valor da ID de usuário for de `sendTrackingData()` é usado no lado do cliente para contar usuários únicos, então os números do lado do cliente e do lado do servidor devem corresponder.

Se as diferenças forem maiores, os seguintes motivos geralmente contabilizam a diferença:

* Uniques de reprodução de vídeo versus todos os únicos de eventos. Como mencionado, a autenticação da Adobe Primetime conta usuários exclusivos para todos os eventos, exceto as tentativas de AuthN. Isso significa que, se o usuário apenas se autenticar (na página), mas não visualizar um vídeo, um aumento exclusivo da contagem de usuários ainda será acionado.

* Contando usuários que falharam na autorização - A autenticação da Adobe Primetime conta esses usuários, bem como no número relatado.

<!--
## Related Information {#related-information}

- [Entitlement Service Monitoring API](/help/authentication/entitlement-service-monitoring-api.md)

-->