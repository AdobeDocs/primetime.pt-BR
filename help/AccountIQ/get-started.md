---
title: O Account IQ é iniciado com o Account IQ, pré-requisitos e integração
description: 'Como integrar, pré-requisitos e começar a usar o Account IQ. '
source-git-commit: 258ce10297aa15086a3ed1c1a825af2a30d34d24
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# Como começar a usar o Account IQ {#onboarding}

Leia para saber sobre os pré-requisitos para usar o Account IQ e como sua empresa pode se integrar a fim de começar a ver as pontuações de compartilhamento de conta dos assinantes.

## Pré-requisitos {#prerequisites}

* A organização deve estar registrada em [!DNL Adobe Marketing Cloud] organizações.

* Os usuários nessa organização devem ser atribuídos ao Painel TVE de leitura ou ao Painel TVE de somente leitura.

### Pré-requisitos do navegador {#browser-prerequisites}

O Account IQ é um serviço da Web hospedado. Ele é compatível com a versão mais recente dos seguintes navegadores:

* Google Chrome
* Mozilla Firefox
* Versão do Safari

### Como integrar organizações no Account IQ? {#steps-to-onboard}


É o que temos neste momento. O plano é se livrar da verificação dma_primetime e ter um perfil dedicado para o AIQ. Os usuários que precisam ter acesso ao console precisam ter esse perfil de usuário. No entanto, não é esse o caso neste momento.

1. Ter a organização deles integrada no Adobe Marketing Cloud @Eric ou @Peter, pode levar isso.  Eu acho que agora se chama &quot;Experience Cloud&quot;, mas isso é menor.  Há mais detalhes nisso? Isso é gerenciado por outro grupo? Em caso afirmativo, fornecemos um link, contato etc.? Isso também deve conter um aviso sobre como verificar se sua organização já faz parte do Experience Cloud.

2. Ter perfis &quot;TVE Dashboard Read-Write&quot; ou &quot;TVE Dashboard Read Only&quot; atribuídos aos usuários em http://adminconsole.adobe.com/.
@Eric, você sabe como fazer isso?  Existem subetapas?  Podemos explicar aos clientes por que eles escolheram Leitura e Somente Leitura?
@Cristina, você pode dar uma breve explicação de que esta é uma abordagem temporária e talvez como ela funcionará na próxima versão?

3. Tendo a id organizacional deles na lista de permissões do lado do AIQ @Cristina, existe um processo que podemos colocar em prática para gerenciar isso?  Por exemplo, envie um email para &quot;DL-AdobePass-Eng AdobePass-Eng@adobe.com&quot; com a ID da organização etc.

<!-- these user groups set dma_primetime product context for the user accounts. In AIQ code we’re checking for this product context when providing access. Internally, in the code we have an additional condition: the org id should be whitelisted in order for the users to get access to their data. -->

Ao acessar o Adobe Enterprise Dashboard, você verá os dois grupos de usuários recém-criados em sua organização da Adobe Marketing Cloud:

Leitura e gravação do painel TVE - os membros deste grupo têm direitos totais em todas as seções editáveis do painel TVE somente leitura - os membros deste grupo têm direitos de visualização somente em todo o painel. Adicione sua conta ao grupo de usuários Leitura e gravação do painel TVE, no Adobe Enterprise Dashboard e faça logon no Adobe Primetime TVE Dashboard.  Posteriormente, você poderá gerenciar as permissões do usuário no Adobe Enterprise Dashboard, adicionando e removendo usuários dos dois grupos de usuários listados acima.

............

Na documentação fornecida, há essa parte chamada &quot;Introdução ao provisionamento do usuário do Primetime TVE Dashboard&quot; que se aplica ao console do Adobe Pass, mas também deve ser semelhante para o AIQ.
http://tve.helpdocsonline.com/primetime-tve-dashboard-user-guide A organização que está interessada no AIQ deve ser uma organização registrada no Adobe Marketing Cloud Orgs. Os usuários nessa organização devem ser atribuídos ao Painel TVE de leitura ou ao Painel TVE de somente leitura.
Somente para seu conhecimento, esses grupos de usuários definem o contexto de produto dma_primetime para as contas de usuário. No código AIQ, estamos verificando esse contexto de produto ao fornecer acesso. Internamente, no código, temos uma condição adicional: a id da organização deve ser incluída na lista de permissões para que os usuários tenham acesso aos seus dados.
É o que temos neste momento. O plano é se livrar da verificação dma_primetime e ter um perfil dedicado para o AIQ. Os usuários que precisam ter acesso ao console precisam ter esse perfil de usuário. No entanto, não é esse o caso neste momento.

...........................

1. Ter sua organização integrada no Adobe Marketing Cloud
2. Ter perfis &quot;TVE Dashboard Read-Write&quot; ou &quot;TVE Dashboard Read Only&quot; atribuídos aos usuários em http://adminconsole.adobe.com/.
3. Ter sua ID de organização na lista de permissões no lado do AIQ
