---
title: Sobre arquivos de configuração de ferramentas de linha de comando
description: Sobre arquivos de configuração de ferramentas de linha de comando
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Sobre arquivos de configuração de ferramentas de linha de comando{#about-command-line-tools-configuration-files}

As ferramentas de linha de comando procuram [!DNL flashaccesstools.properties] no diretório em que você executa as ferramentas. No entanto, você pode usar a opção `-c` ao executar uma ferramenta de linha de comando para especificar um local diferente para o [!DNL flashaccesstools.properties] padrão. Você também pode usar `-c` para especificar um arquivo de configuração diferente.

Os arquivos de configuração das ferramentas de linha de comando usam o formato *Java property file*, ao qual se aplicam as seguintes regras:

* Evite barras invertidas com uma barra invertida adicional.

   Por exemplo, em uma máquina Windows, para especificar o arquivo [!DNL C:\credentials.pfx], é necessário inseri-lo como [!DNL C:\\credentials.pfx] ou `C:/credentials.pfx`. Para especificar um arquivo em um servidor de rede do Windows, você precisa inserir `\\\\server\\folder\\filename.pfx`
* Inclua somente caracteres *Latin-1*.

   Para usar caracteres não *Latin-1*, é necessário usar a sequência de escape Unicode apropriada. Opcionalmente, você pode aplicar a ferramenta [!DNL native2ascii] (incluída com o Java) às entradas do arquivo de configuração.
