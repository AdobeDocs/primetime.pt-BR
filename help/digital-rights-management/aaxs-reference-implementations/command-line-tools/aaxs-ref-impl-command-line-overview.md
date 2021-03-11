---
title: 'Ferramentas de linha de comando para empacotar conteúdo e criar listas de revogações '
description: 'Ferramentas de linha de comando para empacotar conteúdo e criar listas de revogações '
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Ferramentas de linha de comando para empacotar conteúdo e criar listas de revogações {#command-line-tools-for-packaging-content-revocation-lists}

A implementação de referência inclui as seguintes ferramentas de linha de comando:

* Gerenciador de políticas: Uma ferramenta para criar e gerenciar políticas
* Gerenciador de lista de atualização de política: Uma ferramenta para criar e exibir listas de atualização de política
* Gerenciador de lista de revogação: Uma ferramenta para criar e exibir listas de revogação
* Media Packager: Uma ferramenta para criar arquivos FLV e F4V criptografados
* ID do editor do AIR
* UtilitárioGerador de Licenças
* Embeder de licença

## Requisitos {#requirements}

Os requisitos para usar as ferramentas de linha de comando disponíveis nas implementações de referência são os seguintes:

* Todas as ferramentas de linha de comando exigem o Java 1.5 ou superior.
* Credenciais do Packager e do License Server (certificado e senha) emitidas pelo Adobe. Você precisa de credenciais para criptografar e assinar arquivos de vídeo, assinar listas de Atualização e Revogação de Política e pré-gerar licenças.

>[!NOTE]
>
>Devido a um bug do Java, os argumentos usados na linha de comando (como nomes de arquivos, nomes de políticas ou descrições) devem usar somente caracteres do conjunto de caracteres padrão do sistema operacional.

## Arquivo de configuração {#configuration-file}

Várias ferramentas de linha de comando exigem um arquivo de configuração que contenha informações para as ferramentas a serem usadas para aplicar políticas e criptografar arquivos.

O arquivo de configuração padrão é [!DNL flashaccesstools.properties]. Está localizado no diretório de trabalho; ou seja, o diretório no qual você executa as ferramentas (consulte Instalação das ferramentas de linha de comando). Cada ferramenta também contém uma opção ( `-c`) que permite apontar para o arquivo de configuração que deseja usar se preferir não usar o padrão.

O arquivo de configuração usa o formato de arquivo da propriedade Java. Se os valores de qualquer uma das propriedades contiverem caracteres especiais, lembre-se das seguintes restrições:

* Evite barras invertidas com uma barra invertida adicional. Por exemplo, para especificar o arquivo [!DNL C:\credentials.pfx], especifique-o como [!DNL C:\\credentials.pfx] ou `C:/credentials.pfx`. Para especificar um arquivo em um servidor de rede, especifique `\\\\server\\folder\\filename.pfx`.
* O arquivo de configuração pode conter somente caracteres Latin-1. Se você precisar usar caracteres não latino-1, use a sequência de escape Unicode apropriada (usando, opcionalmente, a ferramenta [!DNL native2ascii] que vem com o Java).

Defina os valores das propriedades no arquivo de configuração antes de executar as ferramentas. Para algumas ferramentas de linha de comando, é possível definir os valores de algumas opções por meio da linha de comando ou do arquivo de configuração. Nesses casos, os valores definidos pela linha de comando têm prioridade sobre qualquer valor no arquivo de configuração.

## Instalar as ferramentas da linha de comando {#installing-the-command-line-tools}

Você pode copiar os arquivos necessários do diretório [!DNL \Reference Implementation\Command Line Tools] no DVD, que contém o arquivo de configuração padrão [!DNL flashaccesstools.properties], e um diretório [!DNL libs], que contém os arquivos JAR das ferramentas.

O diretório [!DNL samples] contém vários arquivos de origem Java de exemplo que demonstram o uso das APIs do SDK do Adobe Access. Para criar e executar as amostras, use o script Ant [!DNL build-samples.xml].