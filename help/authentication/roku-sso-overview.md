---
title: Visão geral do Roku SSO
description: Sobre o Roku SSO
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# Visão geral do Roku SSO {#overview}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#roku-sso-intro}

Este documento descreve as informações necessárias para aproveitar o recurso de Logon único em dispositivos Roku. A autenticação da Adobe Primetime colabora com o Roku para melhorar a experiência do usuário de logon e facilitar o logon único nos aplicativos de TV em qualquer lugar para assinantes de TV.

A solução é baseada na API REST sem cliente da autenticação da Adobe Primetime, de modo que a maioria dos programadores não precisará atualizar seus aplicativos para se beneficiar do Logon único.

## Ativação do Roku SSO {#enable-roku-sso}

O Roku SSO é ativado por padrão, a menos que o Programador ou o MVPD solicite o SSO ser desativado.

Cada programador pode ativar/desativar o SSO na plataforma Roku para integrações específicas.

### O que um Programador deve fazer para que o Roku SSO funcione {#make-roku-sso-work}

Para aplicativos de Programadores que implementam a REST API em dispositivos cliente, o Roku SSO funcionará sem qualquer alteração. O Roku OS adicionará dois cabeçalhos HTTP em qualquer solicitação aos pontos finais de Autenticação da Adobe Primetime.

Para aplicativos de Programadores implementando uma solução Servidor para Servidor para api REST , o Programador deve entrar em contato com a equipe do Roku e solicitar uma configuração onde esses dois cabeçalhos serão enviados para o seu domínio em todos os fluxos de api.

A ID de assinante fornecida pelo Roku a ser usada em vez de qualquer ID de dispositivo transmitida pelo aplicativo para garantir o SSO entre aplicativos (e entre dispositivos).

Para obter detalhes específicos sobre o formato dos cabeçalhos necessários, entre em contato com o representante do Adobe.

### Possíveis problemas {#possible-issues}

Os programadores devem verificar se as implementações atuais baseadas na API REST sem cliente do Adobe não impedem o SSO da plataforma Roku. Veja abaixo uma lista de possíveis problemas e como eles devem ser resolvidos.

| Problema | Causa possível | Possíveis soluções | |-|-|-| |Nenhum cabeçalho Roku SSO enviado ao Adobe|Uso de HTTP em vez de HTTPS para chamadas a domínios de autenticação da Adobe Primetime|Usar HTTPS| |Logotipo MVPD não mostrado / não atualizado para tokens SSO|A interface do usuário depende do armazenamento local|Os aplicativos devem atualizar a interface do usuário (e o armazenamento local, se necessário) após verificar a autenticação| |Logout acionado em AuthZ|Design do aplicativo|O aplicativo deve ser atualizado para nunca realizar logout nos bastidores|

## Perguntas frequentes {#faq}

* **Como funcionará o SSO?**

   O SSO funcionará em todos os aplicativos do Programador fornecidos pela autenticação da Adobe Primetime em todos os dispositivos Roku associados ao mesmo usuário Roku.
Nem todos os MVPDs permitirão o Roku SSO.

* **Haverá alguma alteração nos TTLs de autenticação?**

   O primeiro token de autenticação válido será usado para executar SSO e, nesse caso, todos os outros aplicativos que serão autenticados por meio do SSO usarão o mesmo TTL até expirar. Portanto, ao navegar de um aplicativo para outro, o segundo aplicativo compartilhará o TTL do primeiro aplicativo que é autenticado.

* **Outras funcionalidades do Adobe funcionarão como antes?**

   Toda a funcionalidade de autenticação do Primetime funcionará como antes.

* **Existe um processo de aceitação/recusa do programador que se beneficia do SSO na plataforma Roku?**

   Essa será uma alteração de configuração no painel TVE do Adobe. Cada programador pode ativar/desativar o SSO na plataforma Roku para integrações específicas.
