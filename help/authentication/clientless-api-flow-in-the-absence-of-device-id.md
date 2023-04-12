---
title: Fluxo da API sem cliente na ausência de ID do dispositivo
description: Fluxo da API sem cliente na ausência de ID do dispositivo
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Fluxo da API sem cliente na ausência de ID do dispositivo {#clientless-api-flow-in-the-absence-of-device-id}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>


## Problema

Nem todos os aplicativos de dispositivos inteligentes poderão fornecer uma ID de dispositivo exclusiva.  Como deviceId é um parâmetro obrigatório, o serviço retorna um erro 400 se não for passado.


## Solução temporária/solução alternativa

Para clientes sem ID de dispositivo:

1. Chame o serviço de código de registro pela primeira vez com `deviceId=dummy`
1. Na resposta, extraia o UUID. A UUID está disponível no elemento &quot;id&quot; da resposta do código de registro (formatos de resposta XML e JSON).
1. Chame o serviço de registro uma segunda vez. Desta vez, passe `deviceId=<uuid obtained in step #2>`
1. Exiba o código de registro obtido na Etapa 3 na interface do usuário do console


Depois que essas etapas forem concluídas, a autenticação da Adobe Primetime usará a UUID como a ID do dispositivo. Armazene essa ID de dispositivo (UUID) no armazenamento local do dispositivo. Caso o usuário gere um novo código de registro, execute novamente as etapas de 1 a 4 e substitua a ID de dispositivo (UUID) armazenada anteriormente pela nova.



## Solução permanente

O Adobe alterará isso em uma versão futura, fazendo `deviceId` uma carga opcional ao criar o código reg e usar UUID como a chave de token em vez de `deviceId`, quando `deviceId` não está presente.

<!--
## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)
-->