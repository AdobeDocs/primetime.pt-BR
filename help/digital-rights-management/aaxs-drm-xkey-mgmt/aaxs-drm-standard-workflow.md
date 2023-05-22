---
title: Fluxo de trabalho padrão do AXS DRM
description: Fluxo de trabalho padrão do AXS DRM
exl-id: 3bc6aa6a-cda6-4c83-af08-f27eb103a47a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Fluxo de trabalho padrão do AXS DRM{#standard-aaxs-drm-workflow}

1. (Pacote) O SDK Java AXS gera um CEK aleatório.
1. (Pacote) O CEK é usado para criptografar o conteúdo.
1. (Pacote) O CEK é criptografado usando a chave pública do AXS License Server.
1. (Pacote) O CEK criptografado é inserido nos metadados DRM do conteúdo.
1. O dispositivo tenta reproduzir o conteúdo solicitando uma licença ao servidor AXS.
1. (Licenciamento) O servidor AXS usa sua chave privada para descriptografar o CEK dos metadados.
1. (Licenciamento) O servidor AXS emite para o dispositivo uma licença que contém o CEK.
