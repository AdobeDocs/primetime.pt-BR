---
title: Atualização do servidor DRM da Adobe Primetime para transmissão protegida
description: Atualização do servidor DRM da Adobe Primetime para transmissão protegida
copied-description: true
exl-id: 6edfba1b-46a2-4cbd-bc14-feeef1a36ed6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Atualização do servidor DRM da Adobe Primetime para transmissão protegida{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Se quiser atualizar um servidor que execute o servidor DRM do Primetime para transmissão protegida, será necessário substituir o `flashaccessserver.war` arquivo que foi implantado no servidor de aplicativos com o arquivo que foi incluído com o DRM do Primetime mais recente.

Se quiser usar as novas opções de configuração, será necessário atualizar o `flashaccess-tenant.xml`. Também é necessário atualizar [!DNL jsafe.dll] ou [!DNL libjsafe.so] com a versão que foi incluída com o DRM do Primetime mais recente.
