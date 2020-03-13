---
seo-title: Gerenciamento de domínios
title: Gerenciamento de domínios
uuid: aee02196-8704-46ee-add9-82b371722f0f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Gerenciamento de domínios{#managing-domains}

Para impedir que os usuários possam fazer backup e restaurar seus arquivos em uma tentativa de ignorar o cancelamento do registro do domínio, recomenda-se que uma das seguintes abordagens seja implementada para o gerenciamento do domínio:

* Limite o tempo de validade das credenciais de domínio. Os clientes precisarão entrar em contato com o servidor de domínio para adquirir novamente as credenciais de domínio quando expirarem. Nesse momento, o Servidor de Domínio pode garantir que a máquina ainda esteja autorizada a ser membro do domínio.
* Substitua as chaves de domínio sempre que um usuário cancelar o registro. O License Server só deve emitir licenças para clientes que tenham a chave de domínio mais recente. Isso pressupõe que o License Server possa coordenar com o Servidor de Domínio para saber qual chave é a mais recente. A rolagem das chaves de domínio envolve a geração de um novo par de chaves para o domínio. Ao passar o mouse sobre as chaves de um domínio específico, certifique-se de incrementar a versão principal em `generateDomainCredential`. Para obter mais informações sobre a implementação de uma sobreposição principal, consulte *RefImplDomainReqHandler* na Implementação de referência.
* Se o servidor de domínio for o mesmo que o servidor de licença, o servidor poderá usar o contador de reversão para detectar backup e restauração. Consulte *Processando solicitações do Adobe Access *em *Uso do SDK do Adobe Access para Proteção de Conteúdo.*

