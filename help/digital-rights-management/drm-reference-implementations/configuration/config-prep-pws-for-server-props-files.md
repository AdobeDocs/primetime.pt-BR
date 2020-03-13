---
description: nulo
seo-description: nulo
seo-title: Preparar senhas para os arquivos de propriedades do Servidor
title: Preparar senhas para os arquivos de propriedades do Servidor
uuid: 3e00ba9b-b692-4713-8306-5ab896461f2a
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Preparar senhas para os arquivos de propriedades do Servidor{#prepare-passwords-for-the-server-properties-files}

A implementação de referência fornece `ScrambleUtil.class`, uma classe que garante a segurança da senha da sua credencial.

Use essa ferramenta para criptografar a senha antes de incluí-la no [!DNL flashaccess-refimpl.properties] arquivo.

Para executar a ferramenta, você pode usar um script Ant ou Java.

O utilitário gera a senha criptografada, que você deve copiar para o [!DNL flashaccess-refimpl.properties] arquivo.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>As senhas que foram codificadas com o `ScrambleUtil.class` que foi fornecido com a implementação de referência não funcionam com o Primetime DRM Server for Protected Streaming.
