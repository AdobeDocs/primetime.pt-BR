---
title: Guia de início rápido do programador
description: Guia de início rápido do programador
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# Guia de início rápido do programador {#programmer-kickstart-guide}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#prog-kickstart-guide-intro}

Bem-vindo à autenticação da Adobe Primetime para TV em qualquer lugar. Aguardamos com expectativa a oportunidade de trabalhar convosco.

>[!NOTE]
>
>Este é o Kickstart Guide for Programmers (provedores de conteúdo). Se você estiver com um Distribuidor de Programação de Vídeo Multicanal (MVPD), certifique-se de visualizar o [Guia de início rápido do MVPD](/help/authentication/mvpd-kickstart-guide.md).


Contatos de autenticação da Adobe Primetime:

* Suporte - para todas as perguntas, incidentes ou solicitações de recursos, `tve-support@adobe.com`
* Um contato de Ativação será atribuído ao seu projeto até o momento do lançamento do projeto.

As informações a seguir descrevem alguns primeiros passos importantes para nos levar a um começo sólido e eficiente. O objetivo é fornecer uma explicação e expectativas sobre como trabalharemos com parceiros para alcançar integrações. Observe as seções &quot;você fornecerá&quot; / &quot;o Adobe fornecerá&quot; abaixo para cada item. Eles são listados por meio de uma lista de verificação ou guia enquanto trabalhamos no projeto.

Este documento supõe que os programadores estejam inscritos para trabalhar com um parceiro MVPD escolhido.

## Programação de lançamento {#release-schedule}

O ciclo de desenvolvimento do Adobe é planejado para que você possa ver quando nossas versões são agendadas e como cada versão é promovida em nosso sistema de desenvolvimento.

Após a conclusão de cada etapa, ela fica disponível para QE ou para ver novas implementações em nosso servidor UAT.

Aproximadamente a cada 6 semanas será feita uma versão para o servidor de pré-qualificação do Adobe. (Este é o servidor onde realizamos a próxima versão proposta durante a execução do QE final.) Essas builds incluirão todo o trabalho concluído nas gravações desde a última queda. Uma janela de QE de duas semanas está disponível neste momento para os parceiros testarem esta versão.

Supondo que não tenha surgido nenhum problema crítico durante a janela de teste de duas semanas anterior, a versão será promovida para produção em tempo real. Isso significa que a integração estará disponível no ambiente de lançamento do Adobe, mas os parceiros escolhem quando tornam o lançamento público.

<!--For the latest release schedule information, see the Release Calendar.-->

## Documentação de suporte {#supp-doc}

O Adobe fornecerá:

* Guia de implantação: **`https://tve.zendesk.com/entries/498741-tve-deployment-guide`**
* Acesso ao nosso sistema de suporte ao cliente do Zendesk. Também é aqui que você pode encontrar amostras, informações e tutoriais em vídeo sobre alguns processos. Para acessar este documento no Zendesk, juntamente com outros documentos publicados no Zendesk, será necessário registrar-se e criar uma conta no `https://tve.zendesk.com/home`. Não há limite para a quantidade de usuários que você pode registrar.  Você pode ver e compartilhar comentários em qualquer ticket arquivado. Todas as questões de apoio devem ser endereçadas a `tve-support@adobe.com`.
* [Guia de integração do programador](/help/authentication/programmer-integration-guide-overview.md)
* Biblioteca do verificador de token de mídia: `https://tve.zendesk.com/entries/471323-media-token-validator-library`.

## Configuração do ambiente de teste {#test-env-setup}

O Adobe primeiro o configurará com o site de teste do Adobe, onde o Adobe atua como um MVPD para fins de teste. Sua equipe pode configurar um site de teste que chama a API do Adobe. Use o seletor MVPD padrão e selecione &quot;Adobe&quot; como idP.

Você fornecerá:

1. ID do solicitante. Esta é uma string que identificará exclusivamente a marca do site ou do aplicativo que está fazendo solicitações para a autenticação da Adobe Primetime. A cadeia de caracteres em si é arbitrária, mas precisa ser acordada entre o Adobe e o Programador
1. Informações do canal. Este é um conjunto de strings que identifica os canais de conteúdo que estão sendo solicitados pela ID do solicitante. Em muitos casos, o canal e a ID do solicitante são os mesmos. No entanto, você pode ter vários canais de conteúdo que podem ser solicitados pela mesma ID. As cadeias de caracteres de nome de canal devem corresponder aos canais de TV a cabo. Alguns MVPDs validarão esse valor através do protocolo AuthN e/ou AuthZ.
1. Nomes de domínio (a ser permitido para essa ID do solicitante). Esta será uma lista de nomes de domínio reais que serão listados pelo Adobe para aceitar a ID do solicitante. Isso garante que somente os domínios aprovados tenham acesso à autenticação da Adobe Primetime com seus metadados. OBSERVAÇÃO: Os nomes de domínio válidos para produção podem ser diferentes para teste/armazenamento temporário e ambos devem ser fornecidos e identificados.

O Adobe irá configurar a conta e o Adobe fornecerá:

* Logon e senha para acessar o site de teste

## Configuração com MVPD {#setup-mvpd}

Esta seção descreve o que é necessário ao migrar do site de teste de Adobe para trabalhar com um MVPD.

Você fornecerá (via MVPD):

* **Dois conjuntos de credenciais**:
   * AuthN + AuthZ : login/senha para um usuário autenticado e autorizado
   * AuthN + Non-AuthZ : login/senha para um usuário autenticado, mas não autorizado
* **ID do recurso**. Este é um identificador de conteúdo específico que será validado com um MVPD sobre o protocolo AuthZ. Pode estar no nível de canal, programa, episódio ou ativo; deve ser acordado com o seu MVPD.

A autenticação do Adobe Primetime suporta um esquema de metadados baseado em MRSS, o que significa que os IDs de Recurso podem ser tão específicos quanto necessário e podem incluir identificadores que podem ser exclusivos a um MVPD específico.

**NOVA integração MVPD**: É importante lembrar que o MVPD escolhido desempenha uma parte integral na conclusão de qualquer integração. O Adobe precisa gravar o código para cada MVPD de acordo com suas especificações. Até que essas etapas sejam concluídas, você não poderá selecionar esse MVPD na caixa de diálogo ou concluir o teste do produto. O Adobe precisa agendar esse trabalho antecipadamente para se adaptar à próxima edição disponível. (Para obter informações de programação atual, consulte o Calendário de Liberação.)

**Integrações existentes do MVPD**: Se o MVPD escolhido já estiver configurado com o Adobe, as etapas de conectividade devem ser muito mais simples (mais rápidas) e, frequentemente, a conectividade pode ser alcançada por meio de alterações de configuração.

>[!NOTE]
>
>O MVPD AINDA terá de habilitar o Programador e assinar quaisquer negócios relevantes.

**QE com MVPDs**: Todas as integrações envolverão QE conjunto e, como o usuário final é, em última análise, um cliente do MVPD, muitos definiram ciclos de teste antes de enviar &quot;ao vivo&quot;. Como isso envolve a programação de recursos do MVPD, essa é uma área potencial para atraso.

<!--
>[RELATEDINFORMATION]
>[MVPD Kickstart Guide](help\authentication\mvpd-kickstart-guide.md)
-->

