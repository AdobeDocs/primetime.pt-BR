---
title: Gerenciar domínios
description: Gerenciar domínios
copied-description: true
exl-id: c9030373-fd54-4745-9f03-0218532b9d6d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Gerenciar domínios{#managing-domains}

Para evitar que os usuários possam fazer backup e restaurar seus arquivos em um esforço para ignorar o cancelamento de registro do domínio, recomenda-se que uma das seguintes abordagens seja implementada para o gerenciamento de domínio:

* Limitar o tempo de validade das credenciais de domínio. Os clientes precisarão entrar em contato com o servidor de domínio para readquirir credenciais de domínio quando expirarem. Nesse momento, o Domain Server pode garantir que a máquina ainda esteja autorizada a ser membro do domínio.
* Role as chaves de domínio sempre que um usuário cancelar o registro. O License Server só deve emitir licenças para clientes que tenham a chave de domínio mais recente. Isso pressupõe que o License Server possa coordenar com o Domain Server para saber qual chave é a mais recente. A substituição das chaves de domínio envolve a geração de um novo par de chaves para o domínio. Ao rolar sobre as chaves de um domínio específico, certifique-se de incrementar a versão da chave em `generateDomainCredential`. Para obter mais informações sobre como implementar uma sobreposição de chave, consulte *RefImplDomainReqHandler* na implementação de referência.
* Se o servidor de domínio for o mesmo que o servidor de licença, o servidor poderá usar o contador de reversão para detectar backup e restauração. Consulte *Processamento de solicitações de acesso ao Adobe *em *Utilização do SDK do Adobe Access para proteção de conteúdo.*
