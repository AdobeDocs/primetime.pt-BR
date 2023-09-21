---
description: Para impedir que os usuários façam backup e restaurem arquivos para ignorar o cancelamento de registro do domínio, você deve implementar algumas abordagens de gerenciamento de domínio.
title: Gerenciar domínios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Gerenciar domínios {#managing-domains}

Para impedir que os usuários façam backup e restaurem arquivos para ignorar o cancelamento de registro do domínio, você deve implementar algumas abordagens de gerenciamento de domínio.

Estas são algumas abordagens de gerenciamento de domínio:

* Limitar o tempo de validade das credenciais de domínio.

  Os clientes precisam entrar em contato com o servidor de domínio para readquirir credenciais de domínio quando as credenciais expirarem. Nesse momento, o Domain Server pode verificar se a máquina ainda está autorizada a ser membro do domínio.
* Passe o mouse sobre as chaves de domínio sempre que um usuário cancelar o registro.

  O License Server só deve emitir licenças para clientes que tenham a chave de domínio mais recente. Essa abordagem pressupõe que o License Server possa coordenar com o Domain Server para saber qual chave é a mais recente. A substituição das chaves de domínio envolve a geração de um novo par de chaves para o domínio. Ao substituir as chaves de um domínio, incremente a versão da chave em `generateDomainCredential`.
* Se o servidor de domínio for o mesmo que o servidor de licença, o servidor poderá usar o contador de reversão para detectar um backup e uma restauração.

  Para obter mais informações, consulte [Processamento de solicitações DRM do Adobe Primetime](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).
