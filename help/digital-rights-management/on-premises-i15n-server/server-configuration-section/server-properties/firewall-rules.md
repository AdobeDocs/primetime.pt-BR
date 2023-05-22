---
title: Regras de firewall
description: Regras de firewall
copied-description: true
exl-id: 1a40822a-893d-43ec-9c3e-8e0b4ebe6d01
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
