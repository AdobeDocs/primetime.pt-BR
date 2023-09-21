---
title: Regras de firewall
description: Regras de firewall
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# Regras de firewall{#firewall-rules}

Para proteger o acesso ao servidor de individualização, somente determinados caminhos de aplicativos precisam ser expostos. O servidor de individualização deve aceitar solicitações de clientes para estes caminhos:

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

Caminhos de serviço, como [!DNL /flashaccess/admin/*] (ou seja, as páginas de status e de administrador) só devem estar acessíveis no firewall. Nenhuma parte do Servidor de Geração de Chaves deve ser acessada de fora do firewall.
