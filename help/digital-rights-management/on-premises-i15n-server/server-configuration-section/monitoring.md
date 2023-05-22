---
title: Monitoramento
description: Monitoramento
copied-description: true
exl-id: edf62298-4082-4ac1-b2b7-8d0e0959ed04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Monitoramento{#monitoring}

O servidor de individualização e o servidor de geração de chave têm uma página de status, que pode ser usada para determinar a integridade dos servidores.

* **Página de status de individualização:** [!DNL https://SERVER:PORT/flashaccess/status]

   * Relata &quot;Ativo&quot; se o servidor de aplicativos estiver em execução e o aplicativo puder fazer uma solicitação GET ao servidor de Geração de chaves
   * A página informa &quot;Ativo&quot; ou nada. Nenhuma informação sobre o aplicativo é revelada, portanto, esta página pode ser usada para monitoramento de fora do firewall.

* **Página de status Geração de chave:** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * Reporta &quot;Ativo&quot; se o servidor de aplicativos estiver em execução
   * Todos os URLs de Geração de Chave devem estar acessíveis apenas internamente

* **Página Estatísticas de Individualização:** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * Inclui estatísticas sobre o servidor de individualização, como o número de solicitações atendidas e o número de chaves disponíveis no cache
   * Esta página só pode ser acessada internamente

* **Página Estatísticas de Geração de Chave:** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * Inclui estatísticas sobre o servidor de Geração de Chaves, como o número de solicitações atendidas e o número de arquivos principais disponíveis no disco
   * Todos os URLs de Geração de Chave devem estar acessíveis apenas internamente
