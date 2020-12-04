---
seo-title: Atualização do Adobe Primetime DRM Server para transmissão protegida
title: Atualização do Adobe Primetime DRM Server para transmissão protegida
uuid: 5c507ae3-d1d9-40ad-ba97-501ec92b45dc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Atualização do Adobe Primetime DRM Server para Protected Streaming{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Se desejar atualizar um servidor que executa o Primetime DRM Server for Protected Streaming, é necessário substituir o arquivo `flashaccessserver.war` que foi implantado no servidor de aplicativos pelo arquivo que foi incluído no DRM Primetime mais recente.

Se quiser usar as novas opções de configuração, você precisará atualizar o `flashaccess-tenant.xml` do servidor. Você também precisa atualizar [!DNL jsafe.dll] ou [!DNL libjsafe.so] com a versão que foi incluída no DRM Primetime mais recente.
