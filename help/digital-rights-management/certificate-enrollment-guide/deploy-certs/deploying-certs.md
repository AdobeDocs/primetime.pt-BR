---
title: Implantar certificados
description: Implantar certificados
copied-description: true
exl-id: 649c4f24-f74e-4529-84a2-65bcd6d7677c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# Implantar certificados{#deploy-certificates}

Para evitar que a senha do PFX esteja disponível em texto não criptografado no Servidor de Licenças, a Implementação de Referência e o Servidor DRM da Adobe Primetime para Transmissão Protegida exigem que a senha seja criptografada quando especificada no arquivo de configuração. Consulte *Uso das implementações de referência de DRM do Primetime* ou *Usando o servidor DRM do Primetime* para Protected Streaming para obter instruções sobre como executar os utilitários de embaralhamento. Cada uma dessas opções inclui seu próprio utilitário de codificação, e as senhas criptografadas não são intercambiáveis entre essas duas implementações do License Server.

Para implantar os certificados e a senha embaralhada no servidor de licenças, consulte *Uso das implementações de referência de DRM do Primetime* ou *Uso do servidor DRM Primetime para transmissão protegida*.
