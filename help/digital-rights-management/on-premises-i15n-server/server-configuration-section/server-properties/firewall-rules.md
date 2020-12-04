---
seo-title: Regras de firewall
title: Regras de firewall
uuid: f1629ceb-22de-4bb5-b73f-9b874d97ea8b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Regras de Firewall{#firewall-rules}

Para proteger o acesso ao servidor de individualização, somente determinados caminhos de aplicativo precisam ser expostos. O servidor de individualização deve aceitar solicitações dos clientes para estes caminhos:

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

Caminhos de serviço, como [!DNL /flashaccess/admin/*] (ou seja, páginas de status e de administração) devem ser acessíveis somente no firewall. Nenhuma parte do Servidor de geração de chave deve ser acessada fora do firewall.
