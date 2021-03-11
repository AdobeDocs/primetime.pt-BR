---
title: Fluxo de trabalho padrão DRM AAXS
description: Fluxo de trabalho padrão DRM AAXS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Fluxo de trabalho padrão de DRM AAXS{#standard-aaxs-drm-workflow}

1. (Pacote) O AAXS Java SDK gera um CEK aleatório.
1. (Pacote) O CEK é usado para criptografar conteúdo.
1. (Pacote) O CEK é criptografado usando a chave pública do AAXS License Server.
1. (Pacote) O CEK criptografado é inserido nos metadados DRM do conteúdo.
1. O dispositivo tenta reproduzir o conteúdo solicitando uma licença do servidor AXS.
1. (Licenciamento) O servidor AXS usa sua chave privada para descriptografar o CEK dos metadados.
1. (Licenciamento) O servidor AXS emite ao dispositivo uma licença que contém o CEK.
