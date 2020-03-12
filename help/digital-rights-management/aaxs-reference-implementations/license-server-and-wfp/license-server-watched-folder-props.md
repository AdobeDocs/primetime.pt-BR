---
seo-title: Propriedades da pasta assistida
title: Propriedades da pasta assistida
uuid: fc204bb4-033a-46fe-8642-737f6a4cd1f1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Propriedades da pasta assistida {#watched-folder-properties}

Cada pasta assistida contém um arquivo chamado [!DNL properties/watchfolder.properties]. Este arquivo contém as opções de empacotamento para o conteúdo inserido nesta pasta, incluindo o que criptografar e quais políticas aplicar. Todas as alterações feitas nos valores no arquivo de propriedade entrarão em vigor na próxima vez que o empacotador de pastas assistido for executado (você não precisa reiniciar o servidor).

Se houver um erro de configuração no arquivo de propriedades do Packager, o thread do Packager será interrompido. Para retomar o empacotador de pastas monitoradas, reinicie o servidor. Se houver um erro de configuração em um arquivo de propriedades de pasta monitorada, a pasta assistida será removida temporariamente da lista de pastas processadas pelo empacotador. Para adicionar a pasta assistida de volta à lista, reinicie o servidor ou modifique o arquivo de propriedades do empacotador. Se ocorrer um erro durante o empacotamento de um arquivo específico (por exemplo, porque o arquivo está corrompido), o arquivo será ignorado e os arquivos restantes na pasta serão processados.
