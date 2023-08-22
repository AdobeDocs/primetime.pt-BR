---
title: Implementação de API sem clientes-códigos/mensagens do Erro com motivo/causa provável
description: Implementação de API sem clientes-códigos/mensagens do Erro com motivo/causa provável
exl-id: 616e35fc-9b72-422b-9a05-e6248bd52490
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Implementação de API sem clientes-códigos/mensagens do Erro com motivo/causa provável {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>A conteúdo neste página é fornecida somente para fins de informação. O uso desta API exige uma licença atual da Adobe Systems. Não é permitida nenhuma utilização não autorizada.

</br>


## Erro: não autorizado

### Causas:

1. Cabeçalho de autorização ausente no POST
1. Problema com cabeçalho de autorização-Verifique se solicitação tempo está em milissegundos.

## Erro: SC 400 durante a autenticação

### Causas:

1. O servidor não encontrou o código de registro, que foi criado para um solicitante e ambiente específicos.
1. Você pode estar em execução em problemas de script entre domínios
1. O spoofing apropriado deve ser adicionado ao arquivo/etc/hosts

## Erro: 400 solicitação incorreta

### Causas:

1. URL malformada para POST/GET
1. SAMLAssertionParserException – a SAML Assertion criptografada não pode ser descriptografada no final do Adobe Systems

## Erro: 403 Proibido

### Causas:

1. Muitas solicitações rápidas-um recurso do gerenciamento de API para evitar ataques de DoS.
2. Se estiver usando o prequal ambiente então adicione o spoofing, caso contrário, certifique-se de que o spoofing foi removido do arquivo/etc/hosts

## Erro: não é possível fazer logon no MVPD página

### Causas:

1. Nome de usuário e senha não correspondem
2. O logon pode ter sido desativado
3. Verificar se o logon é para produção ou preparo


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->
