---
title: Importância da política
description: Importância da política
copied-description: true
exl-id: 6c6971fe-0c0a-4998-917c-aebbf1c4a9df
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Importância da política{#policy-criticality}

Se as novas regras de uso forem usadas nas políticas e essas políticas forem usadas em pacotes de conteúdo para servidores de licença mais antigos (que não entendem as novas regras de uso), você poderá especificar como os servidores de licença mais antigos devem se comportar. Por padrão, a criticidade da política é &quot;true&quot;, o que significa que o servidor de licenças deve entender todas as partes da política para gerar uma licença usando a política. Se a criticalidade de política for definida como &quot;false&quot;, um servidor de licença mais antigo poderá ignorar partes da política que não compreenda, e as licenças geradas pelo servidor não conterão as novas regras de uso.

Os servidores de Acesso ao Adobe que usam a versão 2.0.2 do SDK e superior respeitarão a configuração de criticidade de política.
