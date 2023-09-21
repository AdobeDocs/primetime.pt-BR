---
title: Atualizar o arquivo de configuração global
description: Atualizar o arquivo de configuração global
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Atualizar o arquivo de configuração global{#updating-the-global-configuration-file}

A senha do HSM no [!DNL flashaccess-global.xml] pode ser modificado a qualquer momento e as alterações entrarão em vigor na próxima vez que o servidor recarregar o arquivo de configuração. No entanto, as alterações nos elementos &quot;Log&quot; e &quot;Cache&quot; não são recarregadas; qualquer alteração nesses elementos requer uma reinicialização do servidor.
