---
title: Regras de firewall
description: Regras de firewall
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Regras de Firewall{#firewall-rules}

Para proteger o acesso ao servidor de individualização, somente determinados caminhos de aplicativo precisam ser expostos. O servidor de individualização deve aceitar solicitações dos clientes para estes caminhos:

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

Caminhos de serviço, como [!DNL /flashaccess/admin/*] (ou seja, páginas de status e de administrador) devem ser acessíveis somente no firewall. Nenhuma parte do Servidor de Geração de Chave deve ser acessada de fora do firewall.
