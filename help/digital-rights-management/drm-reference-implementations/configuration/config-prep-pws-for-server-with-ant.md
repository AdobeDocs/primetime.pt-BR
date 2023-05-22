---
title: Preparar senhas usando Ant
description: Preparar senhas usando Ant
copied-description: true
exl-id: 78f00fd7-ca9c-49a9-9e4b-6d1e2daf9241
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# Preparar senhas usando Ant{#prepare-passwords-using-ant}

Usar Ant para criptografar sua senha:

1. Navegue até `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. Defina o `sdkdir` propriedade no [!DNL build-refimpl.xml] para apontar para o diretório que inclui o SDK Java DRM do Primetime.
1. Execute o seguinte comando:

   ```
   ant -f build-refimpl.xml
   ```
