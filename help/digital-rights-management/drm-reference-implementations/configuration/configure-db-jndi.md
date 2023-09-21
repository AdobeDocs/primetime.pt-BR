---
title: Configurar o banco de dados do servidor de licenças
description: Configurar o banco de dados do servidor de licenças
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Configurar o banco de dados do servidor de licenças{#configure-the-license-server-database}

Para configurar o banco de dados de amostra configurando o esquema do banco de dados e preenchendo o banco de dados com dados de amostra:

1. Abra a linha de comando do MySQL.

   **No Windows -** Clique em  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **No Linux, etc.** - Tipo `MySQL`.

1. Execute o seguinte script SQL:

   mysql> origem &quot; `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   Este script adiciona a conta de usuário `dbuser`, estabelece uma conexão por meio de uma aplicação web e cria um esquema de banco de dados.

   >[!NOTE]
   >
   >Verifique se não há ponto e vírgula ( `;`) no final do script.

1. Edite o `PopulateSampleDB.sql` script que preenche dados de amostra nas tabelas para incluir dados para teste.

   Este script está localizado no `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` pasta.
1. Execute o [!DNL PopulateSampleDB] script para preencher os dados conforme descrito na etapa 2.

   >[!NOTE]
   >
   >Na primeira vez que você executar o [!DNL CreateSampleDB.sql] script o seguinte erro ocorre:

   Você pode ignorar esse erro com segurança. Isso só ocorre na primeira vez que você executa esse script.

Você precisa configurar o DBCP (Database Connection Pooling), que usa o Pool de Conexões de Banco de Dados Jakarta-Commons. Um TestDB de Origem de Dados JNDI é configurado para aproveitar este pool de conexões do servidor de aplicações. Para alterar a conexão de banco de dados para apontar para um servidor MySQL que não esteja em localhost, modifique um dos seguintes arquivos:

* A variável [!DNL META-INF\context.xml] arquivo, que especifica a localização, o nome de usuário e a senha do banco de dados do servidor de licenças que está na [!DNL flashaccess.war] arquivo.

* A variável `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` arquivo.

e recrie o arquivo WAR usando os arquivos atualizados.

Para alterar qualquer um desses parâmetros, edite o [!DNL context.xml] arquivo no [!DNL WebContent] e use o script Ant para recriar o arquivo WAR. Para ajustar o banco de dados, altere as configurações da fonte de dados JNDI neste arquivo.

Se você depurar o projeto de implementação de referência no Eclipse, adicione `$CATALINA_HOME\lib\tomcat-dbcp.jar` à sua configuração executar/depurar.

>[!NOTE]
>
>Se você executar o [!DNL flashaccess.war] em um servidor Tomcat 6.0 independente, essa etapa não é necessária.
