---
title: Opções de política básica
description: Opções de política básica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Opções básicas de política {#basic-policy-options}

A tabela a seguir descreve as preferências básicas de Política :

| Preferência | Descrição |
|---|---|
| Duração da política | Especifica o período de validade do conteúdo protegido com esta política. |
|  | Comece em | As licenças não podem ser utilizadas até essa data/hora. |
|  | Finalizar em | As licenças não podem ser usadas após essa data/hora. |
|  | Terminar após | Especifica o tempo de validade de uma licença (em minutos), a partir do momento em que é empacotada. |
| Armazenamento em cache de licenças | Especifica se as licenças podem ser armazenadas em cache pelo cliente. |
|  |  | As licenças não podem ser usadas após essa data/hora. |
|  | Excluir após | Especifica o período de validade de uma licença (em minutos), a partir do momento em que a licença é emitida pelo servidor de licenças. |
|  | Cache indefinidamente | A licença pode ser armazenada em cache no cliente indefinidamente. |
|  | Sem Cache de Licenças | A licença não pode ser armazenada em cache pelo cliente. Uma nova licença deve ser obtida do servidor sempre que o usuário reproduzir o conteúdo. |
| Autenticação |  |
|  | Anônimo | Nenhuma autenticação é necessária para visualizar o conteúdo. |
|  | Autenticado | Autenticação de nome de usuário/senha é necessária. |
| Ativar Encadeamento de Licenças | Permite que uma licença seja atualizada usando uma licença raiz pai para atualização em lote de licenças. Depois que a licença de folha expirar, o servidor poderá emitir ao cliente uma licença raiz, que renovará todo o conteúdo protegido por esta política. |

