---
seo-title: Monitoramento
title: Monitoramento
uuid: ee62c55f-0d44-40f4-a2c7-39456f4d3d99
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c

---


# Monitoramento{#monitoring}

O servidor de Individualização e o servidor de Geração de Chave têm uma página de status, que pode ser usada para determinar a integridade dos servidores.

* **Página de status de individualização:** [!DNL https://SERVER:PORT/flashaccess/status]

   * Relata &quot;Vivo&quot; se o servidor de aplicativos estiver em execução e o aplicativo puder fazer uma solicitação GET ao servidor de geração de chave
   * A página informa &quot;Vivo&quot; ou nada. Nenhuma informação sobre o aplicativo é revelada, portanto esta página pode ser usada para monitoramento fora do firewall.

* **Página de status Geração de chave:** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * Relata &quot;Vivo&quot; se o servidor de aplicativos estiver sendo executado
   * Todos os URLs de geração de chave devem estar acessíveis apenas internamente

* **Página Estatísticas de individualização:** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * Inclui estatísticas sobre o servidor de individualização, como o número de solicitações fornecidas e o número de chaves disponíveis no cache
   * Esta página só pode ser acessada internamente

* **Página Estatísticas de geração de chave:** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * Inclui estatísticas sobre o servidor de geração de chave, como o número de solicitações fornecidas e o número de arquivos de chave disponíveis no disco
   * Todos os URLs de geração de chave devem estar acessíveis apenas internamente

