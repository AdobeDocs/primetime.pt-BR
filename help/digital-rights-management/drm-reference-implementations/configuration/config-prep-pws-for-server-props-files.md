---
title: Preparar senhas para os arquivos de propriedades do Servidor
description: Preparar senhas para os arquivos de propriedades do Servidor
copied-description: true
exl-id: b613d43d-17ec-44e9-bd14-81f9bb9a7f62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
