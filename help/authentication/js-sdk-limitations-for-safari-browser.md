---
title: Limitações do SDK JS para o navegador Safari
description: Limitações do SDK JS para o navegador Safari
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---

# Limitações do SDK JS para o navegador Safari {#js-sdk-limitations-for-safari-browser}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

<!--
>[!IMPORTANT] 
>
>We are strongly recommending [migration to AccessEnabler JavaScript SDK versions 4.x](http://tve.helpdocsonline.com/accessenabler-js-v4-migration-guide) in order to have a stable and predictable behavior on Safari browser.-->


## Safari 10 {#safari10}

**Detalhes**

* A partir do Safari 10, as configurações padrão de privacidade do navegador farão com que os recursos de Logon único (SSO), Logout Único (SLO) e autenticação passiva parem de funcionar. O Logon único (SSO) e a autenticação passiva não funcionarão mesmo na mesma sessão entre várias guias ou janelas do navegador.

* Essas alterações afetam e estão afetando os processos de autenticação da Adobe Primetime para as seguintes versões do SDK JavaScript do AccessEnabler: v2 (versões 2.x), v3 (versões 3.x), v4 (versões 4.x).

### Atenuação {#mitigation-safari10}

* Para mitigar essas limitações, você pode instruir o usuário a alterar as configurações de privacidade do navegador Safari 10 e usar o &quot;**Permitir sempre**&quot; para a opção &quot;**Cookies e dados do site**&quot; na guia Privacidade do navegador, em Preferências, como mostrado na imagem abaixo.

   ![](assets/always-allow-safari10.png)


## Safari 11 {#safari11}

**Detalhes**

>[!IMPORTANT]
>
>Todos os detalhes acima da seção Safari 10 ainda se aplicam no caso do Safari 11.

* A partir do Safari 11, o navegador introduz [Prevenção de rastreamento inteligente](https://webkit.org/blog/7675/intelligent-tracking-prevention/)(ITP), uma tecnologia que usa heurística para impedir o rastreamento entre sites. Essas heurísticas afetam a maneira como os cookies de terceiros são armazenados e repetidos em chamadas de rede, o que significa que, dependendo da ativação do mecanismo ITP, o navegador Safari bloqueará os cookies de terceiros na comunicação cliente-servidor.

* O serviço de Autenticação Adobe Primetime usa e depende de cookies como parte do processo de autenticação **para funcionar**. Nas situações em que o processo ocorre automaticamente (por exemplo, Temp Pass) ou em implementações que usam iFrames ou a funcionalidade &quot;sem atualização&quot;, os cookies de autenticação do Adobe são considerados cookies de terceiros e bloqueados por padrão. Para quaisquer outros casos, o Safari usa um algoritmo de aprendizado de máquina que pode sinalizar todos os cookies de Autenticação do Adobe Primetime como cookies de rastreamento, estando, portanto, sujeito ao bloqueio do ITP.  

* Em conclusão, um usuário do navegador Safari 11 pode ser incapaz de autenticar em um site habilitado para autenticação da Adobe Primetime após a ativação do mecanismo de Prevenção de Rastreamento Inteligente (ITP), especialmente quando os usuários estão usando vários sites habilitados para Autenticação de Primetime do Adobe. Portanto, a experiência de autenticação do usuário pode ser inesperada e indefinida, desde a incapacidade de fazer logon até a duração de autenticação menor do que o esperado.

* Essas alterações afetam e estão afetando os processos de autenticação da Adobe Primetime das seguintes versões do SDK JavaScript do AccessEnabler: v2 (versões 2.x), v3 (versões 3.x).

### Atenuação {#mitigation-safari11}

* Tanto para o AccessEnabler JavaScript SDK v3 (versões 3.x) quanto para o AccessEnabler JavaScript SDK v4 (versões 4.x), a biblioteca contém um mecanismo capaz de identificar as situações em que a autenticação do usuário foi bloqueada devido à falta de cookies necessários. Nessas situações, a biblioteca aciona um retorno de chamada de erro específico [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference), que é retornado ao site habilitado para Autenticação do Adobe Primetime para ser usado como um sinal para instruir o usuário a tomar ações que possam atenuar o problema. Para beneficiar deste mecanismo, o sítio web deve implementar a variável [Relatório de erros](/help/authentication/error-reporting.md) especificação.

* Para o AccessEnabler JavaScript SDK v2 (versões 2.x), a biblioteca não oferece o mecanismo descrito acima, portanto, o site habilitado para Autenticação do Adobe Primetime não pode ser sinalizado quando instruir o usuário a tomar ações para atenuar o problema.

* A lista de ações que podem atenuar as questões acima mencionadas **se aplica a todas as três versões** do SDK do JavaScript do AccessEnabler.

* When [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference) O retorno de chamada de erro é recebido pelo site do implementador, o usuário deve ser instruído a desativar a Intelligent Tracking Prevention (ITP) e ativar cookies de terceiros:

* No caso do Mac OS X High Sierra e posterior: Desmarcando o &quot;**Impedir rastreamento entre sites**&quot; para &quot;**Rastreamento do site**&quot; na guia Privacidade do navegador, em Preferências, como mostrado na imagem abaixo.

   ![](assets/uncheck-prvnt-cr-st-tr-safari11.png)

* No caso do Mac OS X Sierra e anterior: Verificando o &quot;**Permitir sempre**&quot; para a opção &quot;**Cookies e dados do site**&quot; na guia Privacidade do navegador, em Preferências, como mostrado na imagem abaixo.

   ![](assets/always-allow-safari11.png)

## Safari 12 {#safari12}

**Detalhes**

>[!IMPORTANT]
>
>Todos os detalhes acima da seção Safari 10 e da seção Safari 11 ainda se aplicam no caso do Safari 12.

Esta seção detalha os problemas de compatibilidade do **AccessEnabler JavaScript SDK versões 4.x** no Safari 12.

>[!NOTE]
>
>Lembre-se de que, no caso das versões 2.x e 3.x do SDK JavaScript do AccessEnabler JavaScript, ambos usam cookies de terceiros para os processos de autenticação e, devido às políticas de ITP e cookies de terceiros que começam com o Safari 11, a experiência de autenticação do usuário pode ser inesperada e indefinida, desde a incapacidade de fazer logon até a duração de autenticação menor do que o esperado.


### Funcionalidade certificada do AccessEnabler JavaScript SDK v4 (versões 4.x) no Safari 12 {#certified-functionality-of-accessenabler-javacscript=sdk-v4}

* **Autenticação** os fluxos que usam a interação do usuário sempre funcionarão, mesmo se o navegador do usuário tiver cookies de terceiros desativados, pois a partir da versão 4.0, o SDK JavaScript do AccessEnabler não usa mais cookies de terceiros para os processos de autenticação.

>[!NOTE]
>
>O usuário DEVE interagir com o site para abrir pop-ups de login e/ou interagir com a página de login do MVPD.

* **Autorização/Comprovação/Metadados do Usuário** As operações estão totalmente funcionais, desde que o usuário já esteja autenticado.

### Problemas conhecidos do AccessEnabler JavaScript SDK v4 (versões 4.x) no Safari 12 {#known-issues-of-accessenabler-javascript-sdk-4}

* SSO e SLO

   * Devido a como o localStorage é implementado no Safari, a partir do Safari 10, o SDK do JS não pode mais compartilhar o estado de logon por meio de um iFrame de domínio comum. Isso significa que o usuário precisa fazer logon em cada site que usa o SDK JavaScript do AccessEnabler. Fazer logoff também não exclui tokens de autenticação entre sites, portanto, o usuário precisa fazer logoff de cada site habilitado para Autenticação da Adobe Primetime.

* Aprovação temporária

   * Para passagens temporárias, o SDK JavaScript do AccessEnabler usa um mecanismo de individualização, para bloquear um token de autenticação em um dispositivo específico (instância do navegador). Devido aos novos mecanismos no Safari 12 projetados para evitar o rastreamento, a impressão digital que estamos calculando e usando no mecanismo de individualização **será o mesmo para todos os usuários que têm o mesmo endereço IP**. Consideramos o IP do cliente para fins de individualização, mas mesmo assim o impacto é sobre os usuários que compartilham o mesmo endereço IP público. Para esses usuários, calcularemos a mesma id de individualização e a passagem temporária será vinculada a ela. Isso significa que, uma vez que esse usuário use um passe temporário, ninguém mais terá acesso a ele \! Isso afeta especialmente os usuários corporativos, instituições de ensino ou qualquer outra organização que tenha vários usuários usando o NAT ou um proxy comum para acessar a Internet.

>[!NOTE]
>
>Esse problema está afetando os usuários somente se o implementador usar a Passagem temporária como resultado da interação do usuário; caso contrário, a autenticação da Passagem temporária está sujeita a **Fluxos automáticos** abaixo.

* Fluxos automáticos

   * Os fluxos de autenticação tentados em um modo automatizado, sem qualquer interação do usuário, não terão êxito no Safari 12 ao usar o JS SDK 4.0. Observe que o próximo JS SDK 4.1 corrige todos os problemas com fluxos automatizados.

Casos de uso afetados por esse problema:

* Autenticação automática do TempPass (Visualização livre) - para esses fluxos, o SDK emitirá um erro N130.

* Autenticação Passiva (falha silenciosa) - o usuário é solicitado a selecionar este MVPD e inserir credenciais

### Atenuação {#mitigation-safari12}

**SSO e SLO**

Não existe qualquer mitigação conhecida disponível ou possível no momento da redação. A Apple introduziu uma &quot;API de acesso de armazenamento&quot; no Safari 12 (`https://webkit.org/blog/8124/introducing-storage-access-api`), mas a implementação atual não se aplica a localStorage, mas somente a cookies. Além disso, a API exige interação do usuário para ser usada e, depois de usá-la, o usuário também é solicitado a ter uma caixa de diálogo de permissão semelhante à abaixo.

![](assets/permission-dialog-apple.png)


Nesse ponto, esses requisitos/prompts do Safari não estão alinhados aos nossos requisitos de UX e não temos um comportamento consistente como em outros navegadores, onde o SSO &quot;só funciona&quot; depois que um token é salvo em um domínio comum localStorage.

**Aprovação temporária**

Para atenuar os problemas de individualização e ter uma interação com o usuário, recomendamos que você use **[Aprovação temporária promocional ](/help/authentication/promotional-temp-pass.md)** De maneira interativa e forneça pelo menos uma informação adicional sobre o usuário (por exemplo, endereço de email).

## Safari 13 {#safari13}

**Detalhes**

>[!IMPORTANT]
>
>Todos os detalhes acima da seção Safari 10 até a seção Safari 12 ainda se aplicam no caso do Safari 13.


A partir do Safari 13, o navegador introduz novas alterações no [Prevenção de rastreamento inteligente](https://webkit.org/blog/7675/intelligent-tracking-prevention/) (ITP), tornando a heurística por trás do mecanismo mais estrita no processo de marcar cookies de terceiros como cookies de rastreamento, a fim de impedir o rastreamento entre sites.

Conforme descrito em seções anteriores, o serviço de Autenticação da Adobe Primetime usa e depende de cookies de terceiros como parte dos processos de autenticação quando os implementadores estão usando o SDK v2 do JavaScript do AccessEnabler (versões 2.x) e o SDK v3 do JavaScript do AccessEnabler (versões 3.x). Comparado às versões anteriores do navegador Safari, em que o ITP entrou em vigor após um tempo para &quot;aprender&quot; sobre a interação entre o usuário e as partes envolvidas (sites do programador e Adobe), o navegador Safari 13 está bloqueando os cookies de terceiros iniciais, que são considerados cookies de rastreamento na comunicação cliente-modelo de servidor.

Em conclusão, um usuário do navegador Safari 13 provavelmente não poderá iniciar novas autenticações em um site habilitado para autenticação da Adobe Primetime que esteja usando uma versão mais antiga do SDK JavaScript do AccessEnabler, v2 (versões 2.x) ou v3 (versões 3.x). Isso está acontecendo devido ao fato de que todos os cookies de Autenticação Primetime do serviço Adobe necessários estão bloqueados pelo ITP, tornando o serviço incapaz de atender à solicitação de autenticação.

A biblioteca do AccessEnabler JavaScript SDK v4 (versões 4.x) não usa cookies de terceiros para o processo de autenticação, portanto, suas operações não são afetadas de forma alguma pelas alterações do Safari 13.

### Atenuação {#mitigation-safari13}

Em primeiro lugar, recomendamos vivamente **migração para o SDK do JavaScript do AccessEnabler versões 4.x** para ter um comportamento estável e previsível no navegador Safari.

Em segundo lugar, para o AccessEnabler JavaScript SDK v3 (versões 3.x), a biblioteca contém um mecanismo capaz de identificar as situações em que a autenticação de usuários foi bloqueada devido à falta de cookies necessários. Nessas situações, a biblioteca dispara um retorno de chamada de erro específico ([N130](/help/authentication/error-reporting.md#advanced-error-codes-reference)) que é retornado ao site habilitado para Autenticação do Adobe Primetime para ser usado como um sinal para instruir o usuário a tomar ações que possam atenuar o problema. Para beneficiar deste mecanismo, o sítio web deve implementar a variável [Relatório de erros](/help/authentication/error-reporting.md) especificação.

Para o AccessEnabler JavaScript SDK v2 (versões 2.x), a biblioteca não oferece o mecanismo descrito acima, portanto, o site habilitado para Autenticação do Adobe Primetime não pode ser sinalizado quando instruir o usuário a tomar ações para atenuar o problema.

When [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference) O retorno de chamada de erro é recebido pelo site do implementador, o usuário deve ser instruído a desativar a Intelligent Tracking Prevention (ITP) e ativar cookies de terceiros:

* No caso do Mac OS X High Sierra e posterior: Desmarcando o &quot;**Impedir rastreamento entre sites**&quot; para &quot;**Rastreamento do site**&quot; na guia Privacidade do navegador, em Preferências, como mostrado na imagem abaixo.

   ![](assets/prvnt-cross-site-tr-safari13.png)

* No caso do Mac OS X Sierra e anterior: Verificando</span>he &quot;**Permitir sempre**&quot; para a opção &quot;**Cookies e dados do site**&quot; na guia Privacidade do navegador, em Preferências, como mostrado na imagem abaixo.

   ![](assets/always-allow-safari13.png)

