---
title: Plano de integração direta do MVPD
description: Plano de integração direta do MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---


# Guia de início rápido do MVPD: Plano de integração direta do MVPD {#mvpd-dir-int-plan}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#mvpd-kickstart-intro}

Bem-vindo à autenticação da Adobe Primetime para TV em qualquer lugar.  Aguardamos com expectativa a oportunidade de trabalhar convosco.

>[!NOTE]
>
>Este é o Guia de início rápido dos Distribuidores de Programação de Vídeo Multicanal (MVPDs). Se você for um Programador (provedor de conteúdo), consulte a [Guia de início rápido dos programadores](/help/authentication/programmer-kickstart-guide.md).

O suporte está disponível o tempo todo por meio do sistema de tíquete de autenticação do Primetime no Zendesk. Também é aqui que você pode encontrar amostras, documentação e tutoriais em vídeo para nossos processos. Para usar [Zendesk](https://adobeprimetime.zendesk.com/), será necessário registrar-se e criar uma conta em https://tve.zendesk.com/home. Não há limite para a quantidade de usuários que você pode registrar e que podem ver ou postar comentários em um ticket de campo. Todas as questões de apoio devem ser endereçadas: Suporte ao tve em adobe.com

**Contatos da equipe**:

**Suporte** - Para todas as perguntas, incidentes ou solicitações de recursos **tve-support@adobe.com**.

## 1. Reuniões iniciais {#kickoff-meetings}

O âmbito destas reuniões é o início de discussões técnicas entre o Adobe e o MVPD. Neste ponto do processo, a documentação precisa ser compartilhada de ambos os lados. Como acompanhamento, o Adobe precisa abrir um tíquete em nosso sistema de emissão de bilhetes (https://tve.zendesk.com/) para rastrear o status da integração.

## 2. Recursos {#features}

O Adobe configurará uma chamada de status semanal para discutir e rastrear o cronograma geral, as etapas, a linha do tempo e os detalhes de implementação da integração. Nesta fase, o Adobe faz uma revisão das especificações do MVPD. O resultado disso deve ser uma página de especificação que detalhe todos os recursos necessários para o MVPD. O MVPD enviará um documento de especificação do Adobe, detalhando a implementação de autenticação/autorização do MVPD.

Itens para esclarecer, consulte [Recursos de integração do MVPD](/help/authentication/mvpd-integr-features.md).

Há várias configurações que precisarão ser descritas detalhadamente neste ponto:

* **URL do logotipo do MVPD** - Este é um arquivo com as seguintes dimensões: 112 x 33 pixels. O logotipo é exibido pelos Programadores em seus sites quando o usuário clica no botão &quot;Fazer logon&quot; para selecionar seu provedor de TV paga.
* **Valores de TTL (tempo de vida útil)** - O TTL é normalmente definido pelo MVPD durante o processo de autenticação/autorização. No entanto, o Adobe pode substituir esses valores TTL e fornecer valores diferentes dependendo do que for acordado pelo Programador e pelo MVPD.
* **Nome de exibição** - Isso é exibido pelos programadores em seus sites quando o usuário clica no botão &quot;Fazer logon&quot; para selecionar seu provedor de TV paga.
* **Testar credenciais** - Ambos os perfis (armazenamento temporário e produção) devem ter uma lista de credenciais de teste.

>[!IMPORTANT]
>
>Cada vez que um usuário iniciar um fluxo de direito, ele será associado a uma única ID de usuário opaca e exclusiva.  A ID de usuário é usada para identificar o usuário de um aplicativo do Programador, mas é originada do MVPD.

>[!CAUTION]
>
>Um aviso importante para cada MVPD: a ID do usuário NÃO deve conter informações PII (Informações de identificação pessoal), informações que possam ser usadas isoladamente ou junto a outras informações para identificar, contactar ou localizar o usuário.

## 2. Intercâmbio de metadados {#metadata-ex}

Os dois lados precisam trocar os metadados para todos os ambientes envolvidos (produção, armazenamento temporário, etc.).

* **Adobe**
   * Para o ambiente de preparo, os metadados do Adobe SP podem ser recuperados de: [Metadados sp de preparação de autenticação](https://sp.auth-staging.adobe.com/sp/metadata)
   * Para o ambiente de produção, os metadados do Adobe SP podem ser recuperados: [Metadados sp de produção de autenticação](https://sp.auth.adobe.com/sp/metadata)

* **MVPD**
   * Para adicionar metadados (preparação/produção).

## 4. Permitir lista de IP {#allow-ip-list}

Os seguintes IPs devem ser colocados na lista de permissões no firewall do MVPD. Entre em contato com o Adobe para obter a lista de IPs.

* A autenticação do Primetime requer que firewalls sejam abertos nas portas 80 e 443, para permitir acesso a recursos restritos.

* O MVPD precisa adicionar uma lista de endereços IP para servidores de autenticação e autorização (se esse for o caso).

## 5. Desenvolvimento {#deve}

A duração da fase de desenvolvimento será determinada após revisão das especificações e tendo em conta os elementos que ambas as partes assinaram. O Adobe precisa gravar o código personalizado da parte de autorização.

>[!NOTE]
>
>Observe que a autorização é executada por recurso. Normalmente, a transação de autorização é executada com uma sequência de caracteres de ID, transmitida do site do Programador, representando o canal para o qual o usuário está solicitando autorização. Esse ID de recurso é estabelecido entre o programador e o MVPD e pode ser tão granular quanto necessário.

## 6. Ambientes Adobe {#adobe-env}

O Adobe fornece ambientes diferentes para diferentes estágios do processo de desenvolvimento:

* **Prequalificação** (PRÉ-QUAL): O ambiente PRE-QUAL contém o candidato da próxima versão. O Adobe integra inicialmente novos parceiros neste ambiente, antes de atualizar a integração para o ambiente de versão. Os parceiros têm duas semanas para testar o ambiente PRE-QUAL e devem solicitar explicitamente qualquer alteração na configuração PRE-QUAL (entre em contato com o representante do Adobe para obter detalhes sobre o processo de solicitação de alteração). Correções de erros acionam novas implantações neste ambiente.
* **Versão** (VERSÃO): A produção atual é implantada em um ambiente aqui.

Para obter mais informações sobre como usar ambientes Adobe, consulte [Compreensão dos ambientes do Adobe](/help/authentication/understanding-the-adobe-environments.md)

## 7. Implantação de armazenamento temporário {#stag-env}

Com base nos metadados recebidos do MVPD, o Adobe criará e configurará um novo MVPD no sistema de autenticação do Primetime. Isso será implantado no ambiente de preparo pré-igual do Adobe e será configurado com nosso Programador de teste (TestDistributors).

O MVPD precisa fazer a mesma implantação em seu ambiente de controle de qualidade/preparo/teste.

## 8. Testar e solucionar problemas {#tes-troubleshoot}

Nesta fase, o Adobe e o teste MVPD e a solução de problemas da integração. Para ajudar a testar a integração, a equipe de autenticação do Primetime pode usar o site de teste da API do Adobe. Para saber mais sobre o uso do site de teste da API do Adobe, consulte [Testar os fluxos de autenticação e autorização usando o site de teste da API Adobe](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

Quando o teste e a solução de problemas forem concluídos com êxito, a integração será habilitada no ambiente de preparo da versão Adobe. Nesse ponto, o Adobe pode integrar o MVPD com um programador real.

## 9. Implantação de produção {#prod-dep}

* O MVPD precisa ser implantado primeiro no perfil de produção, para testar a conectividade.

* O Adobe é implantado em produção pré-igual.

* Todas as partes podem agora testar no perfil de produção.

* Se tudo estiver certo nesse ponto, o Adobe pode mover a integração para o ambiente de produção de lançamento (&quot;live&quot;), que está disponível para todos os usuários.

## 10. Procedimentos de escalonamento {#esc-proc}

Quando a integração estiver em produção, é essencial fornecer a melhor experiência do cliente. Para garantir a melhor resposta no caso de um problema de servidor suspenso, os MVPDs devem fornecer a documentação do procedimento de escalonamento para problemas trazidos ao conhecimento do Adobe.

Por sua vez, o Adobe fornece MVPDs com o processo de escalonamento de autenticação do Primetime mais atual.


<!--- [!RELATEDINFORMATION]
>
>* [Programmer Kickstart Guide](/help/authentication/programmer-kickstart-guide.md)
>* [MVPD Integration Guide](/help/authentication/mvpd-integr-features.md)
-->
