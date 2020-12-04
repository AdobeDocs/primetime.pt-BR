---
seo-title: Licenças pré-geradoras
title: Licenças pré-geradoras
uuid: 0207abdf-52bb-4bd0-a4f2-fe740b89fa83
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# Pré-gerando licenças{#pre-generating-licenses}

Se você estiver pré-gerando licenças que contêm regras de uso baseadas em tempo, é altamente recomendável que a licença inclua requisitos de sincronização (Consulte *Usando o guia SDK de acesso ao Adobe para proteção de conteúdo*), para que a expiração da licença possa ser imposta com segurança. A implementação de um mecanismo de &quot;pulsação cardíaca&quot; entre o cliente e o servidor é altamente recomendável se você tiver restrições baseadas em tempo na licença, já que o batimento cardíaco sincronizará o horário do cliente com o horário do servidor.
