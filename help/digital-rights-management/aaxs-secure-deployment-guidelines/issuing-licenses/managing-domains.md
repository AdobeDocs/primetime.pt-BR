---
title: Gerenciamento de domínios
description: Gerenciamento de domínios
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Gerenciamento de domínios{#managing-domains}

Para impedir que os usuários possam fazer backup e restaurar seus arquivos em uma tentativa de ignorar o cancelamento de registro do domínio, recomenda-se que uma das seguintes abordagens seja implementada para o gerenciamento de domínio:

* Limite o tempo em que as credenciais de domínio são válidas. Os clientes precisarão entrar em contato com o servidor de domínio para adquirir novamente as credenciais de domínio quando expirarem. Nesse momento, o Servidor de Domínio pode garantir que o computador ainda esteja autorizado a ser membro do domínio.
* Substitua as chaves de domínio sempre que um usuário se desregistrar. O License Server só deve emitir licenças para clientes que tenham a chave de domínio mais recente. Isso pressupõe que o License Server possa coordenar com o Domain Server para saber qual chave é a mais recente. Passar o mouse sobre as chaves de domínio envolve gerar um novo par de chaves para o domínio. Ao passar as chaves de um domínio específico, incremente a versão da chave em `generateDomainCredential`. Para obter mais informações sobre como implementar uma sobreposição de chave, consulte *RefImplDomainReqHandler* na Implementação de referência.
* Se o servidor de domínio for o mesmo que o servidor de licença, o servidor poderá usar o contador de reversão para detectar backup e restauração. Consulte *Processando solicitações de acesso ao Adobe *em *Usando o SDK de acesso ao Adobe para proteger conteúdo.*

