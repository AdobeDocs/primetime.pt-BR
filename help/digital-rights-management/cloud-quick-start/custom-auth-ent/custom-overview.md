---
title: Visão geral de autenticação/direito personalizado (opcional)
description: Visão geral de autenticação/direito personalizado (opcional)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Visão geral de autenticação/direito personalizado (opcional){#custom-authentication-entitlement-overview-optional}

O DRM do Primetime Cloud pode ser configurado para contatar seu próprio serviço de Autenticação/Direito de Back-End para determinar:

* Este usuário tem permissão para adquirir uma licença?
* Que direitos/restrições devem constar na licença?

O DRM da Primetime Cloud inclui uma implementação de referência de um serviço de autenticação/direito de back-end. Para fins de demonstração, esse servidor está emitindo respostas de &quot;permissão&quot; para solicitações do BEES. Consulte [!DNL BEESServlet.java] para modificar o comportamento de servidor.

>[!NOTE]
>
>Anteriormente, esse era um produto separado chamado *Servidor de Direito Back-End* (BEES), ou seja, as referências a BEES em todo este documento e nos arquivos de origem.
