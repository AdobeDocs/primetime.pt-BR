---
title: Configurar o banco de dados do servidor de licenças
description: Configurar o banco de dados do servidor de licenças
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Configurar o banco de dados do servidor de licenças{#set-up-the-license-server-database}

O servidor de licença de implementação de referência requer um banco de dados para oferecer suporte ao seguinte:

* Autenticação do usuário
* Regras de negócios da demonstração do modelo de uso
* Conversão de metadados
* Suporte de domínio

A aquisição de licença anônima não requer que o banco de dados esteja em execução.

>[!NOTE]
>
>Esse procedimento se aplica somente ao Microsoft Windows. Para outros sistemas operacionais, consulte a documentação do seu sistema operacional ou a documentação do MySQL.

Para executar o servidor de licenças, é necessário instalar e configurar o MySQL:

1. No DVD, acesse o [!DNL Third Party\MySQL\Installer\5.1] e inicie o programa de instalação.
1. Conclua a instalação do MySQL.
1. Selecionar **[!UICONTROL Configure MySQL Server Now]** para iniciar o assistente de configuração.
1. Até a quinta tela, use as configurações padrão ou selecione configurações específicas para o teste.
1. Na quinta tela, selecione **[!UICONTROL Online Transaction Processing (OLTP)]** ou **[!UICONTROL Manual Setting]** e insira o número máximo de conexões permitidas.
1. Anote a senha raiz.
1. Para reinstalar o MySQL, se precisar iniciar o servidor mais tarde, conclua as seguintes etapas:
   1. Exclua o *unidade do sistema:* pasta.

      Esta pasta está localizada em [!DNL \Documents and Settings\All Users\Application Data\MySQL].
   1. Exclua a pasta de instalação antiga do MySQL.

      Por exemplo, *unidade do sistema:*, que está localizado em [!DNL \Program Files\MySQL\MySQL Server 5.1].
1. Para instalar o driver MySQL JDBC 5.1.7, copie o [!DNL mysql-connector-java-5.1.7-bin.jar] arquivo no [!DNL Third Party\MySQL\Installer\5.1] no DVD para o [!DNL ...\Tomcat6.0\lib] no servidor Tomcat.

   >[!NOTE]
   >
   >O driver JDBC MySQL 5.1.7 funciona com Tomcat 6.0. As versões anteriores do Tomcat não são mais suportadas.
