---
seo-title: Atualização do Adobe Primetime DRM Server para transmissão protegida
title: Atualização do Adobe Primetime DRM Server para transmissão protegida
uuid: 5c507ae3-d1d9-40ad-ba97-501ec92b45dc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Atualização do Adobe Primetime DRM Server para transmissão protegida{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Se quiser atualizar um servidor que execute o Primetime DRM Server for Protected Streaming, é necessário substituir o `flashaccessserver.war` arquivo que foi implantado no servidor de aplicativos pelo arquivo que foi incluído no DRM Primetime mais recente.

Se quiser usar as novas opções de configuração, é necessário atualizar o servidor `flashaccess-tenant.xml`. Você também precisa atualizar [!DNL jsafe.dll] ou [!DNL libjsafe.so] com a versão que foi incluída no DRM Primetime mais recente.
