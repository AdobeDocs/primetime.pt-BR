---
title: Opções básicas de política
description: Opções básicas de política
copied-description: true
exl-id: d5ddd54d-9301-42da-b7fd-0b838eb6cf9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Opções básicas de política {#basic-policy-options}

A tabela a seguir descreve as preferências de Política Básica:

| Preferência | Descrição |
|---|---|
| Duração da política | Especifica o período de validade do conteúdo protegido com esta política. |
|  | Iniciar em | As licenças não podem ser usadas até esta data/hora. |
|  | Termina em | As licenças não podem ser usadas após essa data/hora. |
|  | Termina após | Especifica o tempo de validade (em minutos) de uma licença, a partir do momento em que é empacotada. |
| Licença de cache | Especifica se as licenças podem ser armazenadas em cache pelo cliente. |
|  |  | As licenças não podem ser usadas após essa data/hora. |
|  | Excluir após | Especifica o tempo de validade (em minutos) de uma licença, a partir do momento em que ela é emitida pelo servidor de licenças. |
|  | Armazenar em cache indefinidamente | A licença pode ser armazenada em cache no cliente indefinidamente. |
|  | Sem Licença de Cache | A licença não pode ser armazenada em cache pelo cliente. Uma nova licença deve ser obtida do servidor sempre que o usuário reproduzir o conteúdo. |
| Autenticação |  |
|  | Anônimo | Nenhuma autenticação é necessária para visualizar o conteúdo. |
|  | Autenticado | A autenticação de nome de usuário/senha é necessária. |
| Ativar encadeamento de licenças | Permite que uma licença seja atualizada usando uma licença raiz pai para atualização em lote de licenças. Quando a licença folha expirar, o servidor poderá emitir ao cliente uma licença raiz, que renovará todo o conteúdo protegido com essa política. |
