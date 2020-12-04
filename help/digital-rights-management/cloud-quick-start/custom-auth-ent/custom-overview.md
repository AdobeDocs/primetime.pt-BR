---
seo-title: Visão geral de autenticação/autorização personalizada (opcional)
title: Visão geral de autenticação/autorização personalizada (opcional)
uuid: 8b5e38a5-562c-4781-ac40-4b3d6cdd97fe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Visão geral de autenticação/autorização personalizada (opcional){#custom-authentication-entitlement-overview-optional}

O Primetime Cloud DRM pode ser configurado para acessar seu próprio serviço de autenticação/autorização de back-end para determinar:

* Este usuário tem permissão para adquirir uma licença?
* Que direitos/restrições devem ser incluídos na licença?

O DRM da Primetime Cloud inclui uma implementação de referência de um serviço de autenticação/direito back-end. Para fins de demonstração, este servidor está emitindo respostas &quot;permitir&quot; para solicitações BEES. Consulte [!DNL BEESServlet.java] para modificar o comportamento do servidor.

>[!NOTE]
>
>Anteriormente, este era um produto separado chamado *Back End Entitlement Server* (BEES), portanto, as referências ao BEES em todo este documento e nos arquivos de origem.

