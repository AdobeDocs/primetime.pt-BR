---
title: Propriedades da pasta monitorada
description: Propriedades da pasta monitorada
copied-description: true
exl-id: e86518d4-2a16-45c7-aa96-189f677c3ee6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Propriedades da pasta monitorada {#watched-folder-properties}

Cada pasta monitorada contém um arquivo chamado [!DNL properties/watchfolder.properties]. Esse arquivo contém as opções de empacotamento para o conteúdo colocado nessa pasta, incluindo o que criptografar e quais políticas aplicar. Quaisquer alterações feitas nos valores no arquivo de propriedade entrarão em vigor na próxima vez que o empacotador de pastas observado for executado (não é necessário reiniciar o servidor).

Se houver um erro de configuração no arquivo de propriedades do empacotador, o thread do empacotador será interrompido. Para retomar o empacotador de pastas observado, reinicie o servidor. Se houver um erro de configuração em um arquivo de propriedades de pasta monitorada, a pasta monitorada será removida temporariamente da lista de pastas que o empacotador processa. Para adicionar novamente a pasta monitorada à lista, reinicie o servidor ou modifique o arquivo de propriedades do empacotador. Se ocorrer um erro durante o empacotamento de um determinado arquivo (por exemplo, porque o arquivo está corrompido), o arquivo será ignorado e os arquivos restantes na pasta serão processados.
