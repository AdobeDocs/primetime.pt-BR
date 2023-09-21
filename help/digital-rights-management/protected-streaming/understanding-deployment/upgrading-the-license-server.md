---
title: Atualização do servidor DRM da Adobe Primetime para transmissão protegida
description: Atualização do servidor DRM da Adobe Primetime para transmissão protegida
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Atualização do servidor DRM da Adobe Primetime para transmissão protegida{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Se quiser atualizar um servidor que execute o servidor DRM do Primetime para transmissão protegida, será necessário substituir o `flashaccessserver.war` arquivo que foi implantado no servidor de aplicativos com o arquivo que foi incluído com o DRM do Primetime mais recente.

Se quiser usar as novas opções de configuração, será necessário atualizar o `flashaccess-tenant.xml`. Também é necessário atualizar [!DNL jsafe.dll] ou [!DNL libjsafe.so] com a versão que foi incluída com o DRM do Primetime mais recente.
