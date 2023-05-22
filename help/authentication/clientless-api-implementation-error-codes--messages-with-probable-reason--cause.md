---
title: Implementação da API sem cliente - códigos de erro/mensagens com motivo provável/causa
description: Implementação da API sem cliente - códigos de erro/mensagens com motivo provável/causa
exl-id: 616e35fc-9b72-422b-9a05-e6248bd52490
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Implementação da API sem cliente - códigos de erro/mensagens com motivo provável/causa {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

</br>


## Erro: não autorizado

### Causas:

1. Cabeçalho de autorização ausente no POST
1. Problema com o cabeçalho de autorização: verifique se o tempo de solicitação está em milissegundos.

## Erro: SC 400 durante a autenticação

### Causas:

1. O servidor não encontrou o código de registro, que foi criado para um solicitante e ambiente específicos.
1. Você pode estar tendo problemas de script entre domínios
1. A falsificação adequada deve ser adicionada ao arquivo /etc/hosts

## Erro: 400 Solicitação incorreta

### Causas:

1. URL malformado para POST/GET
1. SAMLAssertionParserException - Não foi possível descriptografar a declaração SAML criptografada no final do Adobe

## Erro: 403 Proibido

### Causas:

1. Muitas solicitações rápidas - um recurso do gerenciamento de API para impedir ataques de DoS.
2. Se estiver usando um ambiente pré-igual, adicione a falsificação; caso contrário, verifique se a falsificação foi removida do arquivo /etc/hosts

## Erro: não é possível fazer logon na página MVPD

### Causas:

1. O nome de usuário e a senha não correspondem 
2. O logon pode ter sido desativado
3. Verificar se o logon é para produção ou preparo


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->
