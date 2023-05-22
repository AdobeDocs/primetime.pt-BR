---
title: Arquivo de propriedades do empacotador
description: Arquivo de propriedades do empacotador
copied-description: true
exl-id: 7d78576b-fd77-460d-92d9-c2e69e37006e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Arquivo de propriedades do empacotador {#packager-properties-file}

Use o [!DNL flashaccess-refimpl-packager.properties] arquivo para configurar o componente Pacote de pastas monitoradas da implementação de referência. No mínimo, defina o URL do servidor de licenças, o certificado do servidor de licenças, a credencial do empacotador e as opções de proteção de chave. Esse arquivo também contém o local de cada pasta monitorada (packager.watchfolder.source). `n`). Quaisquer alterações feitas nos valores desse arquivo de propriedades terão efeito na próxima vez que o empacotador de pastas observado for executado (não é necessário reiniciar o servidor). No entanto, se houver um erro de configuração no empacotador, o thread do empacotador de pastas observado será encerrado e o servidor precisará ser reiniciado para reiniciar o thread do empacotador.
