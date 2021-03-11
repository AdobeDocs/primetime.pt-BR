---
title: Preparar senhas para os arquivos de propriedades do servidor
description: Preparar senhas para os arquivos de propriedades do servidor
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---


# Preparar senhas para os arquivos de propriedades do servidor{#prepare-passwords-for-the-server-properties-files}

A implementação de referência fornece `ScrambleUtil.class`, uma classe que garante a segurança da senha da credencial.

Use essa ferramenta para criptografar a senha antes de incluí-la no arquivo [!DNL flashaccess-refimpl.properties].

Para executar a ferramenta, é possível usar um script Ant ou Java.

O utilitário gera a senha criptografada, que deve ser copiada para o arquivo [!DNL flashaccess-refimpl.properties].

>[!NOTE]
>
>As senhas que foram codificadas com o `ScrambleUtil.class` fornecido com a implementação de referência não funcionam com o servidor DRM Primetime para transmissão protegida.
