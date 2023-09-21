---
title: Ferramentas de linha de comando para empacotar conteúdo e criar listas de revogação
description: Ferramentas de linha de comando para empacotar conteúdo e criar listas de revogação
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Ferramentas de linha de comando para empacotar conteúdo e criar listas de revogação {#command-line-tools-for-packaging-content-revocation-lists}

A implementação de referência inclui as seguintes ferramentas de linha de comando:

* Policy Manager: uma ferramenta para criar e gerenciar políticas
* Gerenciador de Listas de Atualização de Políticas: Uma ferramenta para criar e exibir listas de atualização de políticas
* Gerenciador de Listas de Revogação: Uma ferramenta para criar e exibir listas de revogação
* Media Packager: uma ferramenta para criar arquivos FLV e F4V criptografados
* ID do editor do AIR
* UtilityLicense Generator
* Incorporador de Licença

## Requisitos {#requirements}

Os requisitos para usar as ferramentas de linha de comando disponíveis nas implementações de referência são os seguintes:

* Todas as ferramentas de linha de comando exigem o Java 1.5 ou superior.
* Credenciais do empacotador e do servidor de licenças (certificado e senha) emitidas pelo Adobe. Você precisa de credenciais para criptografar e assinar arquivos de vídeo, para assinar listas de Atualização e Revogação de Políticas e para pré-gerar licenças.

>[!NOTE]
>
>Devido a um bug do Java, os argumentos usados na linha de comando (como nomes de arquivos, nomes de políticas ou descrições) devem usar somente caracteres do conjunto de caracteres padrão do sistema operacional.

## Arquivo de configuração {#configuration-file}

Várias das ferramentas de linha de comando exigem um arquivo de configuração que contenha informações para as ferramentas usarem na aplicação de políticas e na criptografia de arquivos.

O arquivo de configuração padrão é [!DNL flashaccesstools.properties]. Ela está localizada no diretório de trabalho; ou seja, o diretório a partir do qual você executa as ferramentas (consulte Instalação das ferramentas de linha de comando). Cada ferramenta também contém uma opção ( `-c`) que permite apontar para o arquivo de configuração que você deseja usar se preferir não usar o padrão.

O arquivo de configuração usa o formato de arquivo de propriedade Java. Se os valores de qualquer uma das propriedades contiverem caracteres especiais, lembre-se das seguintes restrições:

* Evite as barras invertidas com uma barra invertida adicional. Por exemplo, para especificar a variável [!DNL C:\credentials.pfx] arquivo, especifique-o como [!DNL C:\\credentials.pfx] ou `C:/credentials.pfx`. Para especificar um arquivo em um servidor de rede, especifique `\\\\server\\folder\\filename.pfx`.
* O arquivo de configuração pode conter apenas caracteres latinos 1. Se você precisar usar caracteres não latinos-1, use a sequência de escape Unicode apropriada (usando, opcionalmente, a variável [!DNL native2ascii] que vem com Java).

Defina valores para propriedades no arquivo de configuração antes de executar as ferramentas. Para algumas das ferramentas de linha de comando, você pode definir os valores de algumas opções por meio da linha de comando ou do arquivo de configuração. Nesses casos, os valores definidos por meio da linha de comando têm prioridade sobre quaisquer valores no arquivo de configuração.

## Instalação das ferramentas de linha de comando  {#installing-the-command-line-tools}

Você pode copiar os arquivos necessários do [!DNL \Reference Implementation\Command Line Tools] no DVD, que contém o diretório padrão [!DNL flashaccesstools.properties] arquivo de configuração e um [!DNL libs] diretório, que contém os arquivos JAR das ferramentas.

A variável [!DNL samples] O diretório contém vários arquivos de código-fonte Java de amostra que demonstram o uso das APIs do SDK de acesso ao Adobe. Para criar e executar as amostras, use o [!DNL build-samples.xml] Script do Ant.
