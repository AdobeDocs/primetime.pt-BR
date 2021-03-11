---
title: Atualização do servidor DRM Adobe Primetime para transmissão protegida
description: Atualização do servidor DRM Adobe Primetime para transmissão protegida
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Atualizar o servidor DRM Adobe Primetime para transmissão protegida{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Se quiser atualizar um servidor que executa o Primetime DRM Server for Protected Streaming, é necessário substituir o arquivo `flashaccessserver.war` que foi implantado em seu servidor de aplicativos pelo arquivo que foi incluído com o DRM Primetime mais recente.

Se quiser usar as novas opções de configuração, será necessário atualizar o `flashaccess-tenant.xml` do servidor. Você também precisa atualizar [!DNL jsafe.dll] ou [!DNL libjsafe.so] com a versão que foi incluída no DRM Primetime mais recente.
