---
title: Atualização do arquivo de configuração global
description: Atualização do arquivo de configuração global
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# Atualização do arquivo de configuração global{#updating-the-global-configuration-file}

A senha do HSM em [!DNL flashaccess-global.xml] pode ser modificada a qualquer momento e as alterações entrarão em vigor na próxima vez que o servidor recarregar o arquivo de configuração. No entanto, as alterações nos elementos &quot;Registro&quot; e &quot;Armazenamento em cache&quot; não são recarregadas; qualquer alteração nesses elementos requer uma reinicialização do servidor.
