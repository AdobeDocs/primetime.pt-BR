---
title: Visão geral de autenticação/direito personalizado (opcional)
description: Visão geral de autenticação/direito personalizado (opcional)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Visão geral de autenticação/direito personalizado (opcional){#custom-authentication-entitlement-overview-optional}

O DRM da Primetime Cloud pode ser configurado para entrar em contato com seu próprio serviço de Autenticação/Direitos de Back-end para determinar:

* Este usuário tem permissão para adquirir uma licença?
* Que direitos/restrições devem ser incluídos na licença?

O DRM da Primetime Cloud inclui uma implementação de referência de um serviço de autenticação/direito de back-end. Para fins de demonstração, este servidor está emitindo respostas de &quot;permissão&quot; para solicitações BEES. Consulte [!DNL BEESServlet.java] para modificar o comportamento do servidor.

>[!NOTE]
>
>Anteriormente, esse era um produto separado chamado *Back End Entitlement Server* (BEES), portanto, as referências ao BEES em todo este documento e nos arquivos de origem.

