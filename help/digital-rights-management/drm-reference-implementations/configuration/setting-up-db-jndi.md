---
title: Configurar o banco de dados do servidor de licenças
description: Configurar o banco de dados do servidor de licenças
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Configurar o banco de dados do servidor de licenças{#set-up-the-license-server-database}

O servidor de licenças de implementação de referência requer um banco de dados para suportar o seguinte:

* Autenticação do usuário
* Regras de negócios de demonstração do modelo de uso
* Conversão de metadados
* Suporte ao domínio

A aquisição de licença anônima não exige que o banco de dados esteja em execução.

>[!NOTE]
>
>Este procedimento aplica-se apenas ao Microsoft Windows. Para outros sistemas operacionais, consulte a documentação do seu sistema operacional ou consulte a documentação do MySQL .

Para executar o servidor de licenças, é necessário instalar e configurar o MySQL:

1. No DVD, vá para a pasta [!DNL Third Party\MySQL\Installer\5.1] e inicie o programa de instalação.
1. Conclua a instalação do MySQL.
1. Selecione **[!UICONTROL Configure MySQL Server Now]** para iniciar o assistente de configuração.
1. Até a quinta tela, use as configurações padrão ou selecione configurações específicas para seu teste.
1. Na quinta tela, selecione **[!UICONTROL Online Transaction Processing (OLTP)]** ou **[!UICONTROL Manual Setting]** e insira o número máximo de conexões permitidas.
1. Anote a senha raiz.
1. Para reinstalar o MySQL, se precisar iniciar o servidor mais tarde, conclua as seguintes etapas:
   1. Exclua a pasta *unidade do sistema:*.

      Esta pasta está localizada em [!DNL \Documents and Settings\All Users\Application Data\MySQL].
   1. Exclua a pasta antiga de instalação do MySQL.

      Por exemplo, *unidade do sistema:*, que está localizada em [!DNL \Program Files\MySQL\MySQL Server 5.1].
1. Para instalar o driver JDBC do MySQL 5.1.7, copie o arquivo [!DNL mysql-connector-java-5.1.7-bin.jar] na pasta [!DNL Third Party\MySQL\Installer\5.1] no DVD para o diretório [!DNL ...\Tomcat6.0\lib] no servidor Tomcat.

   >[!NOTE]
   >
   >O MySQL JDBC Driver 5.1.7 funciona com o Tomcat 6.0. Versões mais antigas do Tomcat não são mais compatíveis.

