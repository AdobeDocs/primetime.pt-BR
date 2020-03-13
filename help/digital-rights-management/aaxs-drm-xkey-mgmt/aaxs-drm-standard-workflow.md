---
seo-title: Fluxo de trabalho DRM AXS padrão
title: Fluxo de trabalho DRM AXS padrão
description: Fluxo de trabalho DRM AXS padrão
seo-description: Fluxo de trabalho DRM AXS padrão
uuid: b996eb2c-8e37-4a29-a972-e09c69d2461d
translation-type: tm+mt
source-git-commit: 17a492d30c65b1b5e12419f04afa0116654b99fc

---


# Fluxo de trabalho DRM AXS padrão{#standard-aaxs-drm-workflow}

1. (Pacote) O AAXS Java SDK gera um CEK aleatório.
1. (Pacote) O CEK é usado para criptografar conteúdo.
1. (Pacote) O CEK é criptografado usando a chave pública do AAXS License Server.
1. (Pacote) O CEK criptografado é inserido nos metadados DRM do conteúdo.
1. O dispositivo tenta reproduzir conteúdo solicitando uma licença do servidor AAXS.
1. (Licenciamento) O servidor AAXS usa sua chave privada para descriptografar o CEK dos metadados.
1. (Licenciamento) O servidor AAXS emite ao dispositivo uma licença que contém o CEK.
