---
title: Sobre os arquivos de configuração das ferramentas de linha de comando
description: Sobre os arquivos de configuração das ferramentas de linha de comando
copied-description: true
exl-id: 0ec4917e-7c70-4b84-86ac-c34c8a522018
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Sobre os arquivos de configuração das ferramentas de linha de comando{#about-command-line-tools-configuration-files}

As ferramentas de linha de comando procuram [!DNL flashaccesstools.properties] no diretório em que você executa as ferramentas. No entanto, você pode usar a variável `-c` opção ao executar uma ferramenta de linha de comando para especificar um local diferente para o padrão [!DNL flashaccesstools.properties]. Também é possível usar `-c` para especificar um arquivo de configuração diferente.

Os arquivos de configuração das ferramentas de linha de comando usam o *Arquivo de propriedade Java* formato, ao qual se aplicam as seguintes regras:

* Evite as barras invertidas com uma barra invertida adicional.

   Por exemplo, em uma máquina com Windows, para especificar o [!DNL C:\credentials.pfx] arquivo, é necessário inseri-lo como [!DNL C:\\credentials.pfx] ou `C:/credentials.pfx`. Para especificar um arquivo em um servidor de rede Windows, você precisa digitar `\\\\server\\folder\\filename.pfx`
* Incluir somente *Latino-1* caracteres.

   Para usar não-*Latino-1* caracteres, é necessário usar a sequência de escape Unicode apropriada. Opcionalmente, é possível aplicar o [!DNL native2ascii] (incluído com o Java) nas entradas do arquivo de configuração.
