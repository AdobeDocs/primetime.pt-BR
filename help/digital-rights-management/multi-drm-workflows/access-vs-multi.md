---
description: Para aqueles que estão familiarizados com a solução DRM de acesso Primetime Adobe, há algumas diferenças de arquitetura fundamentais entre o Access e o DRM da Primetime Cloud, fornecido pela solução ExpressPlay.
title: Migração do acesso para multi-DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# Migração do Acesso para Multi-DRM {#migrating-from-access-to-multi-drm}

Para aqueles que estão familiarizados com a solução DRM de acesso Primetime Adobe, há algumas diferenças de arquitetura fundamentais entre o Access e o DRM da Primetime Cloud, fornecido pela solução ExpressPlay.

## Diferenças de arquitetura entre acesso e vários DRM

|  | Acesso | Multi-DRM |
|---|---|---|
| **Embalagem** | O Packager está vinculado a um servidor de licenças. O Packager deve saber a chave pública do servidor de licenças quando o conteúdo é empacotado. | O Packager não está vinculado a um servidor de licenças. |
|  | Depois que o conteúdo é empacotado, ele é vinculado a um determinado servidor de licenças. | O conteúdo não está vinculado a um servidor de licenças específico. Um efeito disso é que você pode empacotar todo o conteúdo antes de obter a licença de produção. |
|  | O Packager não precisa se comunicar com nenhuma forma de armazenamento de chave, pois as chaves são incorporadas com segurança ao próprio conteúdo (em metadados) após serem criptografadas. Somente o servidor de licenças correspondente pode lê-las. | As chaves devem ser enviadas *para* Packagers de um sistema de armazenamento de chaves ou enviadas *de* um Packager para um sistema de armazenamento de chaves. Um sistema de armazenamento principal pode ser o próprio sistema do cliente ou pode ser o Armazenamento principal do ExpressPlay. |
| **Direito** | O cliente faz uma solicitação de conteúdo para o serviço do Access Cloud. O serviço da nuvem Access faz uma solicitação para o sistema de direito do cliente. O sistema de direito do cliente responde com direitos para o cliente. (O cliente provavelmente recebeu um cookie para fazer logon dos servidores do cliente antes de fazer a solicitação de licença.) | O cliente faz uma solicitação de token da loja do cliente (provavelmente é o mesmo fluxo de trabalho no qual o cliente estava recebendo um cookie de autenticação). No momento, o cliente realiza uma verificação de direitos. Se a verificação de direitos for aprovada, o cliente enviará uma solicitação aos servidores do ExpressPlay para gerar um token para o cliente. Esse token está sempre vinculado a um conteúdo específico e *may* pode ser vinculado a um dispositivo específico. A loja do cliente envia o token de volta para o cliente. Quando o cliente faz uma solicitação de reprodução de DRM, o token é incluído na solicitação (o método para isso é específico do dispositivo) e o servidor DRM da ExpressPlay valida o token sem chamar o servidor do cliente. |