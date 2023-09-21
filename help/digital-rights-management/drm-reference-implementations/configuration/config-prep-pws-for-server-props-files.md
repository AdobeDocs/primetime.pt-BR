---
title: Preparar senhas para os arquivos de propriedades do Servidor
description: Preparar senhas para os arquivos de propriedades do Servidor
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Preparar senhas para os arquivos de propriedades do Servidor{#prepare-passwords-for-the-server-properties-files}

A implementação de referência fornece `ScrambleUtil.class`, uma classe que garante a segurança da senha da sua credencial.

Use esta ferramenta para criptografar a senha antes de incluí-la na [!DNL flashaccess-refimpl.properties] arquivo.

Para executar a ferramenta, você pode usar um script Ant ou Java.

O utilitário gera a senha criptografada, que você deve copiar para o [!DNL flashaccess-refimpl.properties] arquivo.

>[!NOTE]
>
>Senhas que foram codificadas com o `ScrambleUtil.class` que foram fornecidas com a implementação de referência não funcionam com o servidor DRM do Primetime para transmissão protegida.
