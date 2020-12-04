---
seo-title: Opções de política básica
title: Opções de política básica
uuid: b09543b6-26a7-4e4d-8e8f-866b4bf9cc50
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Opções básicas de política {#basic-policy-options}

A tabela a seguir descreve as preferências de Política básica:

| Preferência | Descrição |
|---|---|
| Duração da política | Especifica o período de validade do conteúdo protegido com esta política. |
|  | Start em | As licenças não podem ser usadas até essa data/hora. |
|  | Terminar em | As licenças não podem ser usadas após essa data/hora. |
|  | Terminar após | Especifica a quantidade de tempo que uma licença é válida (em minutos), a partir do momento em que é empacotada. |
| Cache de licença | Especifica se as licenças podem ser armazenadas em cache pelo cliente. |
|  |  | As licenças não podem ser usadas após essa data/hora. |
|  | Excluir após | Especifica o tempo de validade de uma licença (em minutos), a partir do momento em que a licença é emitida pelo servidor de licenças. |
|  | Cache indefinidamente | A licença pode ser armazenada em cache no cliente indefinidamente. |
|  | Sem Cache de Licenças | A licença não pode ser armazenada em cache pelo cliente. Uma nova licença deve ser obtida do servidor sempre que o usuário reproduzir o conteúdo. |
| Autenticação |  |
|  | Anônimo | Nenhuma autenticação é necessária para visualização do conteúdo. |
|  | Autenticado | Autenticação de nome de usuário/senha obrigatória. |
| Ativar Encadeamento de Licenças | Permite que uma licença seja atualizada usando uma licença raiz pai para atualização em lote de licenças. Quando a licença de folha expirar, o servidor poderá emitir uma licença raiz para o cliente, que renovará todo o conteúdo protegido por esta política. |

