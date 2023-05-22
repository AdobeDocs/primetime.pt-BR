---
title: Criptografar senhas
description: Criptografar senhas
copied-description: true
exl-id: 97b78e00-e5e3-4a9d-8eab-fcf96d3b1219
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 0%

---

# Criptografar senhas{#encrypt-passwords}

Os arquivos de propriedades incluem vários valores de senha que você não deve inserir como texto simples. Criptografe esses valores usando o seguinte comando:

`java -jar adobe-flashaccess-i15n-setup.jar password`

Esse comando gerará uma senha criptografada, que você usará nos arquivos de propriedades.

>[!NOTE]
>Este não é o utilitário usado para criptografar senhas do License Server.
