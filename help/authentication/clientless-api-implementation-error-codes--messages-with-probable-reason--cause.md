---
title: Implementação de API sem cliente - Códigos de erro / mensagens com motivo provável / causa
description: Implementação de API sem cliente - Códigos de erro / mensagens com motivo provável / causa
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Implementação de API sem cliente - Códigos de erro / mensagens com motivo provável / causa {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>


## Erro: Não Autorizado

### Causas:

1. Cabeçalho de autorização ausente no POST
1. Problema com o cabeçalho de autorização - verifique se o tempo de solicitação está em milissegundos.

## Erro: SC 400 durante a autenticação

### Causas:

1. O servidor não encontrou o código de registro, que foi criado para um solicitante e um ambiente específicos.
1. Você pode estar enfrentando problemas de script entre domínios
1. A falsificação adequada deve ser adicionada ao arquivo /etc/hosts

## Erro: 400 Solicitação inválida

### Causas:

1. URL malformado para POST/GET
1. SAMLAsertionParserException - A asserção de SAML criptografada não pôde ser descriptografada no final do Adobe

## Erro: 403 Proibido

### Causas:

1. Demasiadas solicitações rápidas - um recurso do gerenciamento de API para evitar ataques de DoS.
2. Se estiver usando um ambiente igual, adicione falsificação, caso contrário, verifique se a falsificação foi removida do arquivo /etc/hosts

## Erro: Não é possível efetuar login na página MVPD

### Causas:

1. Nome de usuário e senha não correspondem 
2. O logon pode ter sido desabilitado
3. Verifique se o logon é para produção ou armazenamento temporário


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->