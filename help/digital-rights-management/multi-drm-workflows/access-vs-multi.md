---
description: Para aqueles familiarizados com a solução Adobe Primetime Access DRM, existem algumas diferenças arquitetônicas fundamentais entre o Access e o Primetime Cloud DRM, alimentado pela solução ExpressPlay.
title: Migração do Access para o Multi-DRM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# Migração do Access para o Multi-DRM {#migrating-from-access-to-multi-drm}

Para aqueles familiarizados com a solução Adobe Primetime Access DRM, existem algumas diferenças arquitetônicas fundamentais entre o Access e o Primetime Cloud DRM, alimentado pela solução ExpressPlay.

## Diferenças de arquitetura entre acesso e vários DRMs

|  | Access | Multi-DRM |
|---|---|---|
| **Empacotamento** | O empacotador está vinculado a um servidor de licenças. O empacotador deve conhecer a chave pública do servidor de licenças quando o conteúdo for empacotado. | O empacotador não está vinculado a um servidor de licenças. |
|  | Depois que o conteúdo é empacotado, ele é vinculado a um determinado servidor de licença. | O conteúdo não está vinculado a um servidor de licenças específico. Um efeito disso é que você pode empacotar todo o conteúdo antes de obter a licença de produção. |
|  | O Packager não precisa se comunicar com nenhuma forma de armazenamento de chaves, pois as chaves são incorporadas com segurança ao próprio conteúdo (em metadados) após serem criptografadas. Somente o servidor de licenças correspondente pode lê-las. | As chaves devem ser enviadas *para* Empacotadores de um sistema de armazenamento principal ou enviados *de* um empacotador para um sistema de armazenamento principal. Um sistema de armazenamento de chaves pode ser o próprio sistema do cliente ou o Armazenamento de chaves do ExpressPlay. |
| **Direito** | O cliente faz uma solicitação de conteúdo para o serviço Access Cloud. O serviço de nuvem do Access faz uma solicitação ao sistema de direitos do cliente. O sistema de direitos do cliente responde com direitos para o cliente. (O cliente provavelmente obteve um cookie para logon nos servidores do cliente antes de fazer a solicitação de licença.) | O cliente faz uma solicitação para um token da loja do cliente (provavelmente é o mesmo fluxo de trabalho no qual o cliente recebia um cookie de autenticação anteriormente). No momento, o cliente executa uma verificação de direitos. Se a verificação de direitos for aprovada, o cliente enviará uma solicitação aos servidores ExpressPlay para gerar um token para o cliente. Esse token é sempre vinculado a um conteúdo específico e *maio* estar vinculado a um dispositivo específico. A vitrine do cliente envia o token de volta para o cliente. Quando o cliente faz uma solicitação de reprodução DRM, o token é incluído na solicitação (o método para isso é específico do dispositivo) e o servidor DRM do ExpressPlay valida o token sem chamar o servidor do cliente. |
