---
title: Arquivos de configuração do servidor de licenças
description: Arquivos de configuração do servidor de licenças
copied-description: true
exl-id: d48e88a4-caae-4f4e-b870-38da4f3a715e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Arquivos de configuração do servidor de licenças{#license-server-configuration-files}

O servidor DRM da Adobe Primetime para transmissão protegida requer os seguintes tipos de arquivos de configuração:

* Arquivo de configuração global ( [!DNL flashaccess-global.xml])
* Arquivo de configuração de locatário para cada locatário ( [!DNL flashaccess-tenant.xml])

Após concluir a edição dos arquivos de configuração, a Adobe recomenda que você use os utilitários fornecidos com o servidor DRM Primetime para transmissão protegida para verificar se os arquivos estão bem formados.

Consulte *Validador de configuração*.

Se você não quiser disponibilizar senhas em texto não criptografado nos arquivos de configuração, criptografe todas as senhas especificadas nos arquivos de configuração global e de locatário usando a ferramenta Scrambler fornecida pelo Adobe.

Consulte *Scrambler de senhas* para obter mais informações sobre como criptografar senhas.
