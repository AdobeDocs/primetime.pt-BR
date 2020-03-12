---
description: Para aqueles que estão familiarizados com a solução DRM do Primetime Access da Adobe, há algumas diferenças fundamentais entre o Access e o DRM da Primetime Cloud, desenvolvido pela solução ExpressPlay.
seo-description: Para aqueles que estão familiarizados com a solução DRM do Primetime Access da Adobe, há algumas diferenças fundamentais entre o Access e o DRM da Primetime Cloud, desenvolvido pela solução ExpressPlay.
seo-title: Migração do acesso a vários DRM
title: Migração do acesso a vários DRM
uuid: 3e33ca9a-867e-46b8-bf88-8dbfe14ff786
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Migração do acesso a vários DRM {#migrating-from-access-to-multi-drm}

Para aqueles que estão familiarizados com a solução DRM do Primetime Access da Adobe, há algumas diferenças fundamentais entre o Access e o DRM da Primetime Cloud, desenvolvido pela solução ExpressPlay.

## Diferenças arquitetônicas entre o acesso e o Multi-DRM

|  | Acesso | Multi-DRM |
|---|---|---|
| **Embalagem** | O Packager está vinculado a um servidor de licenças. O Packager deve saber a chave pública do servidor de licenças quando o conteúdo é empacotado. | O Packager não está vinculado a um servidor de licenças. |
|  | Depois que o conteúdo é empacotado, ele é vinculado a um determinado servidor de licenças. | O conteúdo não está vinculado a um servidor de licenças específico. Um efeito disso é que você pode disponibilizar todo o seu conteúdo antes de obter sua licença de produção. |
|  | O Packager não precisa se comunicar com nenhuma forma de armazenamento de chave, pois as chaves são incorporadas com segurança ao próprio conteúdo (nos metadados) após serem criptografadas. Somente o servidor de licenças correspondente pode lê-las. | As chaves devem ser enviadas *para* Packagers de um sistema de armazenamento de chave ou enviadas *de um Packager para* um sistema de armazenamento de chave. Um sistema de armazenamento principal pode ser um sistema próprio do cliente ou pode ser o Armazenamento principal do ExpressPlay. |
| **Direito** | O cliente faz uma solicitação de conteúdo para o serviço do Access Cloud. O serviço de nuvem do Access faz uma solicitação para o sistema de direito do cliente. O sistema de direito do cliente responde com direitos para o cliente. (Provavelmente, o cliente recebeu um cookie para o logon dos servidores do cliente antes de fazer a solicitação de licença.) | O cliente faz uma solicitação de token da vitrine do cliente (provavelmente é o mesmo fluxo de trabalho no qual o cliente estava recebendo um cookie de autenticação). No momento, o cliente realiza uma verificação de direitos. Se a verificação de direitos for bem-sucedida, o cliente enviará uma solicitação aos servidores ExpressPlay para gerar um token para o cliente. Esse token está sempre vinculado a um conteúdo específico e *pode* estar vinculado a um dispositivo específico. A vitrine do cliente envia o token de volta para o cliente. Quando o cliente faz uma solicitação de reprodução de DRM, o token é incluído na solicitação (o método para isso é específico do dispositivo) e o servidor DRM do ExpressPlay valida o token sem chamar o servidor do cliente. |