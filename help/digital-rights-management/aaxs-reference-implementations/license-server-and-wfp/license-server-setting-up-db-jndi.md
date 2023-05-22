---
title: Configurando o banco de dados e a fonte de dados JNDI
description: Configurando o banco de dados e a fonte de dados JNDI
copied-description: true
exl-id: ed22f095-924b-4792-8a10-e7548fab2c3b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Configurando o banco de dados e a fonte de dados JNDI {#setting-up-the-database-and-configuring-the-jndi-datasource}

O servidor de licenças de implementação de referência requer um banco de dados para oferecer suporte aos seguintes recursos:

* Autenticação do usuário
* Regras de negócios da demonstração do modelo de uso
* Conversão de metadados
* Suporte de domínio

A aquisição de licença anônima não requer que um banco de dados esteja em execução.

>[!NOTE]
>
>As instruções nesta seção são para a plataforma Microsoft Windows. Para outros sistemas operacionais, consulte a documentação do seu sistema operacional ou a documentação do MySQL.

Para executar o servidor de licenças, será necessário instalar e configurar o MySQL 5.1.34:

1. Execute o instalador do MySQL (localizado na Terceira pasta Party\MySQL\Installer\5.1 no DVD).
1. No final do procedimento de instalação, verifique **[!UICONTROL Configure MySQL Server Now]** para iniciar o assistente de configuração. Use as configurações padrão ou selecione configurações específicas para fins de teste, com a exceção de que na 5ª tela você deve selecionar **[!UICONTROL Online Transaction Processing (OLTP)]** ou **[!UICONTROL Manual Setting]** e insira o número máximo de conexões permitidas.

1. Anote a senha raiz.
1. Se precisar reinstalar o MySQL, siga estas etapas para evitar problemas ao iniciar o servidor posteriormente:

   * Excluir a pasta *unidade do sistema:* [!DNL \Documents and Settings\All Users\Application Data\MySQL].

   * Exclua a pasta de instalação antiga do MySQL: por exemplo, *unidade do sistema:* [!DNL \Program Files\MySQL\MySQL Server 5.1].

Em seguida, será necessário instalar o driver MySQL JDBC 5.1.7. Para fazer isso, copie [!DNL mysql-connector-java-5.1.7-bin.jar] (encontrado no [!DNL Third Party\MySQL\Installer\5.1] no DVD) para o diretório lib do servidor Tomcat: [!DNL ...\Tomcat6.0\lib].

>[!NOTE]
>
>O driver JDBC MySQL 5.1.7 funciona com Tomcat 6.0. As versões anteriores do Tomcat não são compatíveis.

Configure o banco de dados de amostra configurando o esquema do banco de dados e preenchendo o banco de dados com dados de amostra. Para fazer isso, execute as seguintes etapas:

1. Ir para  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]** .
1. Depois de digitar a senha, execute o script SQL a seguir para adicionar a conta de usuário `dbuser` para estabelecer uma conexão por meio de uma aplicação web e criar um esquema de banco de dados (verifique se não há &quot;;&quot; no final. Basta pressionar Enter.):

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. Edite o script que preenche dados de amostra nas tabelas para incluir dados para fins de teste: [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql].
1. Execute este script para preencher os dados conforme você fez na Etapa 2.

>[!NOTE]
>
>Na primeira vez que você executar o [!DNL CreateSampleDB.sql] script você receberá o seguinte erro:

*ERRO 1396 (HY000): falha na operação DROP USER para a consulta &#39;dbuser&#39;@&#39;localhost&#39; OK, 0 linhas afetadas (0,00 s).*

Você pode ignorar esse erro com segurança. Isso só acontece na primeira vez que você executa esse script.

Nesse ponto, será necessário configurar o DBCP (Database Connection Pooling). O DBCP usa o Pool de Conexão de Banco de Dados Jakarta-Commons. Um TestDB de Origem de Dados JNDI é configurado para aproveitar este pool de conexões do servidor de aplicações. Para alterar a conexão do banco de dados para apontar para um servidor MySQL que não esteja no host local, modifique o [!DNL META-INF\context.xml] arquivo (que especifica a localização, o nome de usuário e a senha do banco de dados do servidor de licenças) localizado em [!DNL flashaccess.war], ou modificar [!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] e recriar o arquivo WAR usando os arquivos atualizados. Para alterar qualquer um desses parâmetros, edite o [!DNL context.xml] localizado no diretório WebContent e use o script Ant para recriar o arquivo WAR. Para ajustar o banco de dados, altere as configurações da fonte de dados JNDI neste arquivo.

Se você depurar o projeto de implementação de referência no Eclipse, será necessário adicionar `$CATALINA_HOME\lib\tomcat-dbcp.jar` à sua configuração executar/depurar. Esta etapa não é necessária se você executar o [!DNL flashaccess.war] em um servidor Tomcat 6.0 independente.
