---
title: Arquivo de propriedades do pacote
description: Arquivo de propriedades do pacote
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Arquivo de propriedades do pacote {#packager-properties-file}

Use o arquivo [!DNL flashaccess-refimpl-packager.properties] para configurar o componente Empacotador de pastas assistido da implementação de referência. No mínimo, certifique-se de definir o URL do servidor de licenças, o certificado do servidor de licenças, a credencial do empacotador e as opções de proteção de chave. Este arquivo também contém o local de cada pasta assistida (packager.watchfolder.source. `n`). Todas as alterações feitas nos valores neste arquivo de propriedade terão efeito na próxima vez que o pacote de pastas assistido for executado (a reinicialização do servidor não é necessária). No entanto, se houver um erro de configuração no empacotador, o encadeamento do empacotador de pastas observado será encerrado e o servidor precisará ser reiniciado para reiniciar o encadeamento do empacotador.
