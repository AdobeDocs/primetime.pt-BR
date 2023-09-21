---
title: Preparar senhas usando Ant
description: Preparar senhas usando Ant
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
