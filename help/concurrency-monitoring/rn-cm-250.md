---
title: Notas de versão do Adobe Primetime Concurrency Monitoring 2.5.0
description: Notas de versão do Adobe Primetime Concurrency Monitoring 2.5.0
source-git-commit: ac0c15b951f305e29bb8fa0bd45aa2c53de6ad15
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Notas de versão do Adobe Primetime Concurrency Monitoring 2.5.0 {#cm-250}

Esta página descreve novos recursos, alterações e problemas conhecidos com esta versão:

Data de lançamento: 21/04/2016

## Novos recursos {#new-features}

A API de monitoramento de simultaneidade v2.0 agora está disponível em produção.

A versão V2 unifica as chamadas de heartbeat e de consulta e simplifica bastante a implementação quando essas duas APIs são usadas simultaneamente.



### Ciclo de vida da sessão {#session-lifecycle}

* APIs somente gravação para criação, manutenção de atividade e encerramento de uma sessão — ou seja, sem mais consultas, a decisão é retornada nas chamadas de inicialização e heartbeat da sessão
* O intervalo de heartbeat agora é controlado pelo servidor por meio de cabeçalhos Expires definidos nas chamadas de inicialização da sessão e keep-alive. Isso permite a configuração do lado do servidor de intervalos de heartbeat e um valor codificado a menos nos aplicativos.
* O caminho feliz (comportamento compatível do usuário e do aplicativo) é &quot;pavimentado&quot; com códigos de status 2XX

### Tratamento de erros {#error-handling}

* As decisões de negação, os metadados ausentes ou o comportamento incorreto do aplicativo são sinalizados como respostas 4XX (Conflito, Solicitação inválida, Não autorizado, Sumido etc.)

* Sempre que fizer sentido, a resposta inclui:

   * conselho associado — explicação detalhada da falha, a ser solicitada ao usuário.

   * obrigações — ações obrigatórias que o aplicativo deve realizar (por exemplo: atualizar metadados, fazer logout do Adobe Pass).

### Metadados {#metadata}

* Padrão em vez de metadados personalizados - permite que a API identifique se os metadados errados estão sendo enviados ou se os metadados exigidos pelas regras estão ausentes.
* Os atributos necessários para cada aplicativo agora são fornecidos por uma chamada de API e devem ser armazenados em cache pelos clientes.
Notas

>[!NOTE]
>
>A versão V1 continua disponível. Se os clientes precisarem usar queries fora da chamada de heartbeat, a versão V1 poderá ser usada.




### Correções de erros {#bug-fixes}

N/D

### Problemas conhecidos {#known-issues}

N/D
