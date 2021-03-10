---
title: Propriedades da pasta assistida
description: Propriedades da pasta assistida
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Propriedades da pasta assistida {#watched-folder-properties}

Cada pasta assistida contém um arquivo chamado [!DNL properties/watchfolder.properties]. Esse arquivo contém as opções de empacotamento para o conteúdo colocado nessa pasta, incluindo o que criptografar e quais políticas aplicar. Todas as alterações feitas nos valores no arquivo de propriedade entrarão em vigor na próxima vez que o pacote de pastas assistido for executado (você não precisa reiniciar o servidor).

Se houver um erro de configuração no arquivo de propriedades do empacotador, o encadeamento do empacotador será interrompido. Para retomar o empacotador de pastas observado, reinicie o servidor. Se houver um erro de configuração em um arquivo de propriedades da pasta monitorada, a pasta assistida será removida temporariamente da lista de pastas que o empacotador processa. Para adicionar a pasta assistida de volta à lista, reinicie o servidor ou modifique o arquivo de propriedades do empacotador. Se ocorrer um erro durante o empacotamento de um arquivo específico (por exemplo, porque o arquivo está corrompido), o arquivo será ignorado e os arquivos restantes na pasta serão processados.
