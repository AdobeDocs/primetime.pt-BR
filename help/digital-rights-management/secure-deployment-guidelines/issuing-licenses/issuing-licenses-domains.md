---
description: Para impedir que os usuários façam backup e restaurem arquivos para ignorar o cancelamento do registro do domínio, é necessário implementar algumas abordagens de gerenciamento de domínio.
seo-description: Para impedir que os usuários façam backup e restaurem arquivos para ignorar o cancelamento do registro do domínio, é necessário implementar algumas abordagens de gerenciamento de domínio.
seo-title: Gerenciamento de domínios
title: Gerenciamento de domínios
uuid: 30b73e38-d6ed-43c6-89ba-ae8616383779
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Gerenciando domínios {#managing-domains}

Para impedir que os usuários façam backup e restaurem arquivos para ignorar o cancelamento do registro do domínio, é necessário implementar algumas abordagens de gerenciamento de domínio.

Estas são algumas abordagens de gerenciamento de domínio:

* Limite o tempo de validade das credenciais de domínio.

   Os clientes precisam entrar em contato com o servidor de domínio para readquirir credenciais de domínio quando as credenciais expirarem. Nesse momento, o Servidor de Domínio pode verificar se a máquina ainda está autorizada a ser membro do domínio.
* Passe o ponteiro do mouse sobre as chaves de domínio sempre que um usuário cancelar o registro.

   O License Server só deve emitir licenças para clientes que tenham a chave de domínio mais recente. Essa abordagem supõe que o License Server possa coordenar com o Domain Server para saber qual chave é a mais recente. A rolagem das chaves de domínio envolve a geração de um novo par de chaves para o domínio. Quando você passar o mouse sobre as chaves de um domínio, incremente a versão principal em `generateDomainCredential`.
* Se o servidor de domínio for o mesmo que o servidor de licenças, o servidor poderá usar o contador de reversão para detectar um backup e uma restauração.

   Para obter mais informações, consulte [Processando solicitações Adobe Primetime DRM](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).

