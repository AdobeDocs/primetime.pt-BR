---
description: nulo
seo-description: nulo
seo-title: Configurar o banco de dados do servidor de licenças
title: Configurar o banco de dados do servidor de licenças
uuid: aa6185f2-8e9d-4b65-971a-b7534d910580
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Configurar a base de dados do servidor de licenças{#set-up-the-license-server-database}

O servidor de licenças de implementação de referência requer um banco de dados para suportar o seguinte:

* Autenticação do usuário
* Regras de negócios de demonstração de modelo de uso
* Conversão de metadados
* Suporte a domínio

A aquisição de licença anônima não exige que o banco de dados esteja em execução.

>[!NOTE]
>
>Este procedimento se aplica somente ao Microsoft Windows. Para outros sistemas operacionais, consulte a documentação do seu sistema operacional ou consulte a documentação do MySQL.

Para executar o servidor de licenças, é necessário instalar e configurar o MySQL:

1. No DVD, vá para a pasta [!DNL Third Party\MySQL\Installer\5.1] e start o programa de instalação.
1. Compete a instalação do MySQL.
1. Selecione **[!UICONTROL Configure MySQL Server Now]** para start do assistente de configuração.
1. Até a quinta tela, use as configurações padrão ou selecione configurações específicas para seu teste.
1. Na quinta tela, selecione **[!UICONTROL Online Transaction Processing (OLTP)]** ou **[!UICONTROL Manual Setting]** e insira o número máximo de conexões permitidas.
1. Anote a senha raiz.
1. Para reinstalar o MySQL, se precisar start o servidor mais tarde, conclua as seguintes etapas:
   1. Exclua a pasta *unidade do sistema:*.

      Esta pasta está localizada em [!DNL \Documents and Settings\All Users\Application Data\MySQL].
   1. Exclua a pasta de instalação antiga do MySQL.

      Por exemplo, *unidade do sistema:*, que está localizada em [!DNL \Program Files\MySQL\MySQL Server 5.1].
1. Para instalar o driver JDBC MySQL 5.1.7, copie o arquivo [!DNL mysql-connector-java-5.1.7-bin.jar] na pasta [!DNL Third Party\MySQL\Installer\5.1] no DVD para o diretório [!DNL ...\Tomcat6.0\lib] no servidor Tomcat.

   >[!NOTE]
   >
   >O MySQL JDBC Driver 5.1.7 funciona com o Tomcat 6.0. Versões anteriores do Tomcat não são mais suportadas.

