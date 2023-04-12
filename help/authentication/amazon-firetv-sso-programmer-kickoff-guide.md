---
title: Amazon fireTV SSO - Guia de lançamento do programador
description: Amazon fireTV SSO - Guia de lançamento do programador
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# Amazon fireTV SSO - Guia de lançamento do programador {#amazon-firetv-sso---programmer-kick-off-guide}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>

## Introdução {#intro}

Este documento descreve as informações necessárias para integrar o novo **SDK fireTV da autenticação da Adobe Primetime** no aplicativo fireTV. Esse novo SDK aproveita a integração no nível do sistema operacional na plataforma Amazon FireTV, oferecendo assim **Logon único** suporte. Para se beneficiar do Logon único, é necessário um pequeno esforço de seu lado para migrar seu aplicativo da API sem cliente para o novo SDK do FireTV. Há algumas alterações nos fluxos de autenticação que serão detalhadas abaixo.

## Arquitetura de alto nível e integração no nível do SO {#high}

Para obter o Logon único entre os aplicativos da TV em qualquer lugar na plataforma Amazon FireTV e para melhorar a experiência geral nessa plataforma, decidimos integrar nosso SDK principal no nível do sistema operacional FireTV. Os programadores serão solicitados a compilar em relação a uma biblioteca stub fornecida pelo Adobe. A funcionalidade real será fornecida pela biblioteca Adobe presente no Amazon FireTV OS.

Até que o Amazon forneça um simulador FireTV que incorpore nossa biblioteca no nível do SO, o desenvolvimento só seria possível usando dispositivos FireTV reais.

## Benefícios {#bene}

* Logon único entre todos os aplicativos TV em qualquer lugar alimentados por Adobe na plataforma Amazon FireTV com todos os MVPDs integrados.
* Capacidade de beneficiar do HBA (com MVPDs compatíveis).
* Capacidade de usar o SDK do FireTV mais recente sem precisar atualizar seus aplicativos sempre que uma nova versão do SDK for lançada.
* Todos os aplicativos TVE se beneficiam do uso da biblioteca de sistema compartilhada, removendo a necessidade de ter uma cópia local da biblioteca AccessEnabler. Isso também garante que todos os aplicativos estejam usando a mesma versão do SDK.
* Autenticação de tela única - sem necessidade de código de registro e fluxos de trabalho de segunda tela.

## Migração do aplicativo baseado na API sem cliente para o aplicativo baseado no SDK do FireTV {#migra1}

Para migrar da API sem cliente para o SDK do FireTV, é necessário remover a base de código relacionada à API sem cliente e integrar o novo SDK do FireTV.

Comparado com o aplicativo baseado na API sem cliente, com o novo SDK do FireTV, a autenticação é movida para a primeira tela, não há mais necessidade de uma segunda autenticação de tela.

Isso requer que os programadores adicionem um seletor de MVPD em seus aplicativos para que os usuários possam escolher seu provedor de TV diretamente no dispositivo FireTV. Após a seleção de MVPD, o usuário exibirá a página de logon do MVPD no dispositivo fireTV.

Wireframes dos fluxos de usuário que descrevem os cenários regular, HBA e SSO no FireTV podem ser encontrados em [Amazon Fire TV - Fluxo de Usuário de Logon do MVPD](https://xd.adobe.com/view/9058288e-4b67-43a1-9d5b-5f76ede6c51e/).

## Migração do aplicativo baseado no SDK do Android para o aplicativo baseado no SDK do FireTV {#migra2}

Esse novo SDK do FireTV é muito semelhante ao nosso Android SDK existente e à documentação atual que temos para **integração de nosso SDK do Android** <!--http://tve.helpdocsonline.com/android-technical-overview-->pode ser usado até que os documentos SDK do FireTV estejam prontos. Se você já tiver aplicativos Android que usam nosso Android SDK, a integração do FireTV SDK no aplicativo FireTV deve ser direta.

Comparado ao Android SDK existente, o SDK do FireTV simplificará o processo de autenticação, pois as tarefas de gerenciamento / apresentação da página de logon do MVPD e recuperação do token AuthN serão executadas internamente pela biblioteca AccessEnabler .

## Perguntas frequentes {#faq}

1. Como a **SSO** trabalho?

   * O SSO funcionará em todos os aplicativos programadores alimentados pela autenticação da Adobe Primetime que estejam usando o novo SDK do FireTV no mesmo dispositivo Amazon fireTV
   * SSO entre aplicativos do Programador implementados na API REST sem cliente e aplicativos implementados no SDK do FireTV **NÃO será suportado**

1. Qual é a cobertura do MVPD do fireTV SSO?

   * **Todos os MVPDs** integrado pela autenticação da Adobe Primetime será suportado tecnicamente pelo SSO no SDK do FireTV.

1. Além de usar o novo SDK, que outro **alterações no fluxo de trabalho** os programadores devem estar cientes disso?

   * Os programadores precisam implementar um seletor MVPD para a plataforma fireTV.

1. Haverá qualquer alteração na autenticação **TTLs**?

   * Não há alteração no comportamento em relação aos TTLs de autenticação.
   * O primeiro token de autenticação válido será usado para executar o SSO e, nesse caso, todos os outros aplicativos que serão autenticados por meio do SSO usarão o mesmo TTL até expirar. Portanto, ao navegar de um aplicativo para outro, o segundo aplicativo compartilhará o TTL do primeiro aplicativo que é autenticado.

1. Como a função **API de degradação** trabalho?

   * Não há alterações necessárias para a API de degradação, a experiência do usuário será a mesma de dispositivos Android.

1. How **TempPass** os fluxos são afetados?

   * Os fluxos de TempPass são uma única tela e se comportam como em qualquer outro dispositivo nativo.

1. Outras funcionalidades do Adobe funcionarão como antes?

   * Toda a funcionalidade de autenticação do Primetime funcionará no FireTV como em dispositivos Android.
