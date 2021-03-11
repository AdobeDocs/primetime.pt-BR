---
title: Arquivos de configuração do servidor de licenças
description: Arquivos de configuração do servidor de licenças
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Arquivos de configuração do servidor de licenças{#license-server-configuration-files}

O Adobe Primetime DRM Server for Protected Streaming requer os seguintes tipos de arquivos de configuração:

* Arquivo de configuração global ( [!DNL flashaccess-global.xml])
* Arquivo de configuração de locatário para cada locatário ( [!DNL flashaccess-tenant.xml])

Após concluir a edição dos arquivos de configuração, o Adobe recomenda usar os utilitários fornecidos com o Primetime DRM Server for Protected Streaming para verificar se os arquivos estão bem formados.

Consulte *Validador de configuração*.

Se você não quiser disponibilizar senhas em texto claro nos arquivos de configuração, será necessário criptografar todas as senhas especificadas nos arquivos de configuração global e do locatário usando a ferramenta Scrambler fornecida pelo Adobe.

Consulte *Scrambler de senha* para obter mais informações sobre como criptografar senhas.
