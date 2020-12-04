---
description: nulo
seo-description: nulo
seo-title: Preparar senhas para os arquivos de propriedades do Servidor
title: Preparar senhas para os arquivos de propriedades do Servidor
uuid: 3e00ba9b-b692-4713-8306-5ab896461f2a
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Preparar senhas para os arquivos de propriedades do Servidor{#prepare-passwords-for-the-server-properties-files}

A implementação de referência fornece `ScrambleUtil.class`, uma classe que garante a segurança da senha da sua credencial.

Use essa ferramenta para criptografar a senha antes de incluí-la no arquivo [!DNL flashaccess-refimpl.properties].

Para executar a ferramenta, você pode usar um script Ant ou Java.

O utilitário gera a senha criptografada, que você deve copiar para o arquivo [!DNL flashaccess-refimpl.properties].

>[!NOTE]
>
>As senhas que foram codificadas com `ScrambleUtil.class` que foram fornecidas com a implementação de referência não funcionam com o Primetime DRM Server for Protected Streaming.
