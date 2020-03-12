---
description: nulo
seo-description: nulo
seo-title: Configurar o banco de dados do servidor de licenças
title: Configurar o banco de dados do servidor de licenças
uuid: 6d34e849-1616-46bd-ad18-4f98e6c45af7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configurar o banco de dados do servidor de licenças{#configure-the-license-server-database}

Para configurar o banco de dados de amostra, configure o esquema do banco de dados e preencha o banco de dados com dados de amostra:

1. Abra a linha de comando MySQL.

   **No Windows -** , clique em **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **No Linux etc.** - Tipo `MySQL`.

1. Execute o seguinte script SQL:

   mysql> source &quot; `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   Esse script adiciona a conta de usuário `dbuser`, estabelece uma conexão por meio de um aplicativo da Web e cria um esquema de banco de dados.

   >[!NOTE]
   >
   >Verifique se não há ponto-e-vírgula ( `;`) no final do script.

1. Edite o `PopulateSampleDB.sql` script que preenche os dados de amostra nas tabelas para incluir dados para seus testes.

   Esse script está localizado na `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` pasta.
1. Execute o [!DNL PopulateSampleDB] script para preencher os dados como fez na etapa 2.

   >[!NOTE] {class=&quot;- tópico/observação &quot;}
   >
   >Na primeira vez que você executar o [!DNL CreateSampleDB.sql] script, ocorrerá o seguinte erro:

   Esse erro pode ser ignorado com segurança. Isso ocorre somente na primeira vez que você executa esse script.

É necessário configurar o Pooling de Conexões de Banco de Dados (DBCP), que usa o Pool de Conexões de Banco de Dados Jakarta-Commons. Um JNDI Datasource TestDB está configurado para aproveitar esse pooling de conexão do servidor de aplicativos. Para alterar a conexão do banco de dados para apontar para um servidor MySQL que não esteja em um host local, modifique um dos seguintes arquivos:

* O [!DNL META-INF\context.xml] arquivo, que especifica o local, o nome de usuário e a senha do banco de dados do servidor de licenças que está no [!DNL flashaccess.war] arquivo.

* O `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` arquivo.

e recrie o arquivo WAR usando os arquivos atualizados.

Para alterar qualquer um desses parâmetros, edite o [!DNL context.xml] arquivo no [!DNL WebContent] diretório e use o script Ant para recriar o arquivo WAR. Para ajustar o banco de dados, altere as configurações da fonte de dados JNDI neste arquivo.

Se você depurar o projeto de Implementação de referência no Eclipse, adicione `$CATALINA_HOME\lib\tomcat-dbcp.jar` à sua configuração de execução/depuração.

>[!NOTE]
>
>Se você executar o [!DNL flashaccess.war] arquivo em um servidor Tomcat 6.0 independente, essa etapa não será necessária.

