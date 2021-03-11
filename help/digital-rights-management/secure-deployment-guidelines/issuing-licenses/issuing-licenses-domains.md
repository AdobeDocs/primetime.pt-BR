---
description: Para impedir que os usuários façam backup e restaurem arquivos para ignorar o cancelamento do registro do domínio, você deve implementar algumas abordagens de gerenciamento de domínio.
title: Gerenciamento de domínios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Gerenciamento de domínios {#managing-domains}

Para impedir que os usuários façam backup e restaurem arquivos para ignorar o cancelamento do registro do domínio, você deve implementar algumas abordagens de gerenciamento de domínio.

Estas são algumas abordagens de gerenciamento de domínio:

* Limite o tempo em que as credenciais de domínio são válidas.

   Os clientes precisam entrar em contato com o servidor de domínio para readquirir credenciais de domínio quando as credenciais expirarem. Nesse momento, o Servidor de Domínio pode verificar se o computador ainda está autorizado a ser membro do domínio.
* Passe o mouse sobre as chaves de domínio sempre que um usuário cancelar o registro.

   O License Server só deve emitir licenças para clientes que tenham a chave de domínio mais recente. Essa abordagem pressupõe que o License Server possa coordenar com o Domain Server para saber qual chave é a mais recente. Passar o mouse sobre as chaves de domínio envolve gerar um novo par de chaves para o domínio. Ao passar o mouse sobre as chaves de um domínio, incremente a versão da chave em `generateDomainCredential`.
* Se o servidor de domínio for o mesmo que o servidor de licença, o servidor poderá usar o contador de reversão para detectar um backup e uma restauração.

   Para obter mais informações, consulte [Processando solicitações Adobe Primetime DRM](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).

