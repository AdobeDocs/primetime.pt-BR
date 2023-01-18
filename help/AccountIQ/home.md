---
title: Visão geral do Account IQ
description: O Account IQ ajuda os MVPDs e programadores a compreenderem os riscos de suas operações de receita e negócios e a determinarem as ações mais eficazes a serem tomadas para mitigar os impactos da fraude de credenciais.
exl-id: c0d85fc8-b5ab-4284-802e-82f52eff401f
source-git-commit: 4475faca828510153a7ec3e505704ee8d8b044d0
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Visão geral do Account IQ {#account-iq-overview}

O compartilhamento de credenciais por assinantes de serviços de transmissão é um grande e crescente problema do setor. Para adicioná-lo, entender, identificar e atuar no compartilhamento de credenciais é um processo complexo. Há complexidade envolvida na compreensão do comportamento de uso do assinante e no desenvolvimento de uma visão holística de sua atividade, por exemplo, distinguindo o compartilhamento entre membros dentro e fora da mesma família. Devido a esse desafio, os provedores de serviços de transmissão podem ter inibições em agir contra o compartilhamento de credenciais.


<div class "preview">
Geralmente, os provedores de serviços de streaming de vídeo entendem o risco e o custo do compartilhamento em seus negócios, mas têm soluções limitadas, como bloquear os compartilhadores ou fazer ofertas. No entanto, é recomendada uma abordagem informada e direcionada, que permita que os serviços entendam o compartilhamento com precisão e adotem estratégias que recompensem o bom comportamento de visualização e, simultaneamente, direcionem o crescimento dos negócios. </span>

![Diagrama de fluxo do Account IQ](assets/aiq-intro.png)

*Figura: Fluxo de informações do Account IQ*

O Adobe Primetime Account IQ permite que os serviços de streaming de vídeo compreendam os padrões de uso do assinante e identifiquem o compartilhamento de credenciais. Analisando profundamente a longa trilha de dados deixada por cada assinante usando o modelo de aprendizagem de máquina de várias camadas do Adobe, os serviços de transmissão podem entender o comportamento de uso e identificar o compartilhamento de credenciais com maior grau de certeza. Além disso, ele permite que ações sejam tomadas por meio de integrações com outros sistemas, como limitar fluxos simultâneos ou personalizar ofertas, e valida o impacto dessas ações, seja incentivando o comportamento de visualização legítimo ou os assinantes e a receita crescentes.

O Account IQ fornece as ferramentas e os recursos para medir, gerenciar e monetizar o compartilhamento de credenciais. Relatórios, análises e painéis permitem a exploração dos dados para identificar padrões. A ação direta é suportada por exportações e integrações com sistemas Adobe e de terceiros, como gerenciamento de campanha, limitação de moeda ou registro de assinante. E as ferramentas de rastreamento dedicadas medem o sucesso dessas ações para que possam ser atualizadas ou expandidas.

As ferramentas e os recursos do aplicativo Account IQ são explicados nas seguintes seções:

* [Painel](/help/AccountIQ/dashboard.md)
* [Relatórios de uso geral](/help/AccountIQ/general-usage-reports.md)
* [Relatórios de contas compartilhadas](/help/AccountIQ/shared-acc-reports.md)
* [Padrões de uso](/help/AccountIQ/usage-patterns.md)
* [Operações](/help/AccountIQ/operations.md)

Vamos mergulhar nos gráficos e relatórios em cada uma dessas seções.

>[!MORELIKETHIS]
>
>* [Como começar a usar o Account IQ](/help/AccountIQ/get-started.md)
>* [Painel](/help/AccountIQ/dashboard.md)
>* [Relatórios de uso gerais](/help/AccountIQ/general-usage-reports.md)
>* [Relatórios de contas compartilhadas](/help/AccountIQ/shared-acc-reports.md)
>* [Padrões de uso](/help/AccountIQ/usage-patterns.md)
>* [Glossário de termos do produto](/help/AccountIQ/product-concepts.md)
>* [White paper sobre o Account IQ](https://www.adobe.com/content/dam/dx/us/en/products/primetime/resources/primetime-account-iq-whitepaper.pdf)


<!-- Credential sharing is rampant and prevalent among subscribers in the video streaming industry. To add to it, understanding, identifying, and acting on password sharing is a complex process. There is complexity involved in understanding the subscriber usage behavior and developing a holistic view of viewer activity—for example, distinguishing sharing among members within the same household and outside. Due to this challenge, streaming service providers have inhibitions in acting against password sharing.

Generally, video streaming service providers consider password sharing as fatal for business and act strongly against it, by blocking the sharers. However, it is advised to follow a holistic approach that enables them to understand sharing accurately and adopt strategies to reward good viewing behavior and target business growth simultaneously.

![Account IQ flow diagram](assets/aiq-intro.png)

*Figure: Account IQ information flow*

Adobe Primetime Account IQ enables video streaming services understand the subscriber usage patterns and identify password sharing by analyzing usage behavior. Moreover, it validates the impact of applying actions to encourage legitimate viewing behavior while maximizing business ROI, eventually growing subscribers and revenue.

By deeply analyzing the long, winding trail of data left behind by each subscriber using Adobe's proprietary multi-layer machine learning model, customers can understand usage behavior and identify password sharing with a greater degree of certainty, use the insights to validate the impact of applying actions to encourage legitimate viewing behavior while maximizing business growth, eventually act on password sharing using validated tactics to improve viewer experience, growing subscribers and revenue (for e.g. converting sharers to paid subscribers, managing ad loads based on sharing behavior, rewarding good behavior with better viewer experience).

Account IQ is helps you understand usage patterns and identify password sharing by leveraging the Primetime Authentication  solution that processes a huge volume of TV Everywhere transactions. A proprietary multi-layer machine learning model trained by this real-world TVE data accurately characterizes usage patterns and helps video streaming services understand usage patterns and identify password sharing at an individual account level. Based on Adobe's customer experience management solutions, Account IQ enables video streaming services to effectively use their audience data to create actionable sharing profiles as well powers integrations with other Adobe Digital Experience and 3rd party solutions—for example, Adobe Primetime Concurrency Monitoring or Adobe Analytics—to enable understanding usage patterns, identify and act upon password sharing.


<!-- The widespread availability of video content and streaming services bring with it problem of account sharing; eventually leading to the loss of revenue by content providers. Account IQ helps TV Everywhere and VOD (video on demand) providers understand the risks to their revenue and business operations, and determine the most effective actions to take to mitigate the impacts of credential fraud. It helps these media companies (MVPDs, Programmers, and VOD providers) manage and uncover the instances of password sharing with a high level of confidence, enabling them deliver better business outcomes and provide better viewing experiences for subscribers.

To help media companies better understand the password sharing within their businesses, Primetime Account IQ determines **Password Sharing Risk Index** that rates every subscriber on their likelihood of sharing account credentials for subscription passwords, from very low to very high. Based on these calculations and the resulting indices, analytics are performed and visuals are generated for better understanding and interpretation of the account sharing behavior. Account IQ is a hosted web application, which you can access using your browser.

Account IQ assigns sharing scores to different subscriber accounts, so that the content providers (media companies, programmers, MVPDs, and VOD providers) can take informed decisions about subscriber accounts and check the illicit sharing.

Passwords are the main methods for viewers to authenticate, and there is a misconception that credential sharing is allowed. This idea makes illicit password sharing a common practice; necessitating the need for media companies to educate their viewers about permissible sharing and prevent illicit sharing.-->
