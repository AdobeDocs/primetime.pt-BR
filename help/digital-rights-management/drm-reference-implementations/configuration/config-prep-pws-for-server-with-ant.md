---
title: Preparar senhas usando Ant
description: Preparar senhas usando Ant
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---


# Preparar senhas usando Ant{#prepare-passwords-using-ant}

Use Ant para criptografar sua senha:

1. Navegue até `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. Defina a propriedade `sdkdir` em [!DNL build-refimpl.xml] para apontar para o diretório que inclui o SDK Java de DRM do Primetime.
1. Execute o seguinte comando:

   ```
   ant -f build-refimpl.xml
   ```

