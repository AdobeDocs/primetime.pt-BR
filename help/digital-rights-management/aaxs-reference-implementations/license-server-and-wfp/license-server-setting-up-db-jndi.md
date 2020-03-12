---
seo-title: Configuração do banco de dados e configuração da fonte de dados JNDI
title: Configuração do banco de dados e configuração da fonte de dados JNDI
uuid: 1326523f-c053-4169-a934-1b2d3907b1f4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configuração do banco de dados e configuração da fonte de dados JNDI {#setting-up-the-database-and-configuring-the-jndi-datasource}

O servidor de licenças de implementação de referência requer um banco de dados para suportar os seguintes recursos:

* Autenticação do usuário
* Regras de negócios de demonstração de modelo de uso
* Conversão de metadados
* Suporte a domínio

A aquisição de licença anônima não exige que um banco de dados esteja em execução.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>As instruções desta seção são para a plataforma Microsoft Windows. Para outros sistemas operacionais, consulte a documentação do seu sistema operacional ou consulte a documentação do MySQL.

Para executar o servidor de licenças, será necessário instalar e configurar o MySQL 5.1.34:

1. Execute o instalador MySQL (localizado na terceira pasta Party\MySQL\Installer\5.1 no DVD).
1. No final do procedimento de instalação, verifique **[!UICONTROL Configure MySQL Server Now]** para iniciar o assistente de configuração. Use as configurações padrão ou selecione configurações específicas para seus fins de teste, com a exceção de que na 5ª tela você deve selecionar **[!UICONTROL Online Transaction Processing (OLTP)]** ou **[!UICONTROL Manual Setting]** inserir o número máximo de conexões permitidas.

1. Anote a senha raiz.
1. Se precisar reinstalar o MySQL, siga estas etapas para evitar problemas ao iniciar o servidor depois:

   * Exclua a unidade de pasta *do sistema:* [!DNL \Documents and Settings\All Users\Application Data\MySQL].

   * Exclua a pasta de instalação antiga do MySQL: por exemplo, unidade *do sistema:* [!DNL \Program Files\MySQL\MySQL Server 5.1].

Em seguida, você precisará instalar o Driver MySQL JDBC 5.1.7. Para fazer isso, copie [!DNL mysql-connector-java-5.1.7-bin.jar] (localizado na [!DNL Third Party\MySQL\Installer\5.1] pasta do DVD) para o diretório lib do Tomcat Server: [!DNL ...\Tomcat6.0\lib].

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>O MySQL JDBC Driver 5.1.7 funciona com o Tomcat 6.0. Versões anteriores do Tomcat não são compatíveis.

Configure o banco de dados de amostra configurando o esquema do banco de dados e preenchendo o banco de dados com dados de amostra. Para fazer isso, execute as seguintes etapas:

1. Vá até **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]** .
1. Depois de digitar a senha, execute o script SQL a seguir para adicionar a conta de usuário `dbuser` para estabelecer uma conexão por meio de um aplicativo da Web e criar um esquema de banco de dados (verifique se não há &quot;;&quot; no final. Basta pressionar enter.):

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. Edite o script que preenche dados de amostra nas tabelas para incluir dados para suas finalidades de teste: [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql].
1. Execute esse script para preencher os dados como fez na Etapa 2.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>Na primeira vez que você executar o [!DNL CreateSampleDB.sql] script receberá o seguinte erro:

*ERRO 1396 (HY000): Falha na operação DROP USER para &#39;dbuser&#39;@&#39;localhost&#39; Consulta OK, 0 linhas afetadas (0,00 s).*

Esse erro pode ser ignorado com segurança. Isso só acontece na primeira vez que você executa esse script.

Nesse ponto, será necessário configurar o Pooling de Conexões de Banco de Dados (DBCP). O DBCP usa o Pool de Conexões de Banco de Dados Jakarta-Commons. Um JNDI Datasource TestDB está configurado para aproveitar esse pooling de conexão do servidor de aplicativos. Para alterar a conexão do banco de dados para apontar para um servidor MySQL que não esteja em um host local, modifique o [!DNL META-INF\context.xml] arquivo (que especifica o local, o nome de usuário e a senha do banco de dados do servidor de licenças) localizado em, ou modifique [!DNL flashaccess.war][!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] e recrie o arquivo WAR usando os arquivos atualizados. Para alterar qualquer um desses parâmetros, edite o [!DNL context.xml] localizado no diretório WebContent e use o script Ant para recriar o arquivo WAR. Para ajustar o banco de dados, altere as configurações da fonte de dados JNDI neste arquivo.

Se você depurar o projeto de Implementação de referência no Eclipse, precisará adicionar `$CATALINA_HOME\lib\tomcat-dbcp.jar` à sua configuração de execução/depuração. Esta etapa não é necessária se você executar o [!DNL flashaccess.war] arquivo em um servidor Tomcat 6.0 independente.
