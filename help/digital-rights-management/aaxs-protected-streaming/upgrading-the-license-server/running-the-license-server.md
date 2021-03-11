---
description: Para atualizar um servidor executando o Adobe Access Server para transmissão protegida, substitua o arquivo flashaccess server.war implantado em seu servidor de aplicativos pelo arquivo incluído com o Adobe Access mais recente. Se desejar usar as novas opções de configuração descritas acima, atualize o flashaccess-tenant.xml do seu servidor. Você também precisa atualizar jsafe.dll ou libjsafe.so para a versão incluída com o Adobe Access mais recente.
title: Execução do Adobe Access Server para transmissão protegida
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Execução do Adobe Access Server para transmissão protegida{#running-the-adobe-access-server-for-protected-streaming}

Para atualizar um servidor executando o Adobe Access Server para transmissão protegida, substitua o arquivo flashaccess server.war implantado em seu servidor de aplicativos pelo arquivo incluído com o Adobe Access mais recente. Se desejar usar as novas opções de configuração descritas acima, atualize o flashaccess-tenant.xml do seu servidor. Você também precisa atualizar jsafe.dll ou libjsafe.so para a versão incluída com o Adobe Access mais recente.

Antes de executar o Adobe Access Server for Protected Streaming, o Adobe recomenda que você verifique se os arquivos de configuração são válidos usando os utilitários fornecidos com o servidor de licença. Para obter mais detalhes, consulte &quot;[Validador de configuração](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Para iniciar o Tomcat e o servidor de licenças, execute &quot;catalina.bat start&quot; ou &quot;catalina.sh start&quot; no diretório bin do Tomcat.

Depois que o servidor tiver iniciado, verifique se ele está configurado corretamente abrindo *https:// license-server-host:port/flashaccess server/tenant-name/flashaccess/license/v1* em uma janela do navegador. Se a configuração do locatário tiver sido carregada com êxito, uma mensagem de confirmação será exibida.
