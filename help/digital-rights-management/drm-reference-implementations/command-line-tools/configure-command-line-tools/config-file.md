---
description: nulo
seo-description: nulo
seo-title: Sobre arquivos de configuração de ferramentas de linha de comando
title: Sobre arquivos de configuração de ferramentas de linha de comando
uuid: 8220921f-1fe9-439c-8134-dc16c2e3601b
translation-type: tm+mt
source-git-commit: 0143d98185b9a63ef978aba18e2f3c8728333155

---


# Sobre arquivos de configuração de ferramentas de linha de comando{#about-command-line-tools-configuration-files}

As ferramentas de linha de comando são procuradas [!DNL flashaccesstools.properties] no diretório em que você executa as ferramentas. No entanto, você pode usar a `-c` opção ao executar uma ferramenta de linha de comando para especificar um local diferente para o padrão [!DNL flashaccesstools.properties]. Você também pode usar `-c` para especificar um arquivo de configuração diferente.

Os arquivos de configuração das ferramentas de linha de comando usam o formato de arquivo *de propriedade* Java, ao qual se aplicam as seguintes regras:

* Evite barras invertidas com uma barra invertida adicional.

   Por exemplo, em uma máquina do Windows, para especificar o [!DNL C:\credentials.pfx] arquivo, é necessário inseri-lo como [!DNL C:\\credentials.pfx] ou `C:/credentials.pfx`. Para especificar um arquivo em um servidor de rede do Windows, é necessário inserir `\\\\server\\folder\\filename.pfx`
* Incluir somente caracteres *latino-1* .

   Para usar caracteres que não sejam *Latin-1* , é necessário usar a sequência de escape Unicode apropriada. Opcionalmente, você pode aplicar a [!DNL native2ascii] ferramenta (incluída com Java) às entradas do arquivo de configuração.
