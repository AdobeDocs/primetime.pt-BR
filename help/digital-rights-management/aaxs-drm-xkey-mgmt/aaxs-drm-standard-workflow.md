---
title: Fluxo de trabalho padrão do AXS DRM
description: Fluxo de trabalho padrão do AXS DRM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
