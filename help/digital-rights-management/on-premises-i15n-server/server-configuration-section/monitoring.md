---
title: Monitoramento
description: Monitoramento
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Monitoramento{#monitoring}

Cada um dos servidores de Individualização e Geração de Chave tem uma página de status, que pode ser usada para determinar a integridade dos servidores.

* **Página de status da individualização:** [!DNL https://SERVER:PORT/flashaccess/status]

   * Relata &quot;Vivo&quot; se o servidor de aplicativos estiver em execução e o aplicativo puder fazer uma solicitação GET para o servidor de Geração de Chave
   * A página informa &quot;Vivo&quot; ou nada. Nenhuma informação sobre o aplicativo é revelada, portanto, esta página pode ser usada para monitoramento fora do firewall.

* **Página Status da Geração de Chave:** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * Relata &quot;Vivo&quot; se o servidor de aplicativos estiver em execução
   * Todos os URLs de Geração de Chave só devem ser acessíveis internamente

* **Página Estatísticas de individualização:** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * Inclui estatísticas sobre o servidor de individualização, como o número de solicitações fornecidas e o número de chaves disponíveis no cache
   * Esta página só deve ser acessível internamente

* **Página Estatísticas de Geração de Chave:** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * Inclui estatísticas sobre o servidor de Geração de Chave, como o número de solicitações fornecidas e o número de arquivos-chave disponíveis no disco
   * Todos os URLs de Geração de Chave só devem ser acessíveis internamente

