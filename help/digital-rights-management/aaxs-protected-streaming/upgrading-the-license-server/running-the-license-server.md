---
description: Para atualizar um servidor executando o Adobe Access Server for Protected Streaming, substitua o arquivo flashaccess server.war implantado no servidor de aplicativos pelo arquivo incluído no Adobe Access mais recente. Se desejar usar as novas opções de configuração descritas acima, atualize o flashaccess-locatário.xml do servidor. Você também precisa atualizar jsafe.dll ou libjsafe.so para a versão incluída com o Adobe Access mais recente.
seo-description: Para atualizar um servidor executando o Adobe Access Server for Protected Streaming, substitua o arquivo flashaccess server.war implantado no servidor de aplicativos pelo arquivo incluído no Adobe Access mais recente. Se desejar usar as novas opções de configuração descritas acima, atualize o flashaccess-locatário.xml do servidor. Você também precisa atualizar jsafe.dll ou libjsafe.so para a versão incluída com o Adobe Access mais recente.
seo-title: Execução do Adobe Access Server para transmissão protegida
title: Execução do Adobe Access Server para transmissão protegida
uuid: 3819500d-ad2f-49eb-8aa4-e50a55461608
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Execução do Adobe Access Server para transmissão protegida{#running-the-adobe-access-server-for-protected-streaming}

Para atualizar um servidor executando o Adobe Access Server for Protected Streaming, substitua o arquivo flashaccess server.war implantado no servidor de aplicativos pelo arquivo incluído no Adobe Access mais recente. Se você quiser usar as novas opções de configuração descritas acima, atualize flashaccess-locatário.xml do servidor. Você também precisa atualizar jsafe.dll ou libjsafe.so para a versão incluída com o Adobe Access mais recente.

Antes de executar o Adobe Access Server for Protected Streaming, a Adobe recomenda que você verifique se os arquivos de configuração são válidos usando os utilitários fornecidos com o servidor de licenças. Para obter mais detalhes, consulte &quot;Validador[de configuração](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Para iniciar o Tomcat e o servidor de licenças, execute &quot;catalina.bat start&quot; ou &quot;catalina.sh start&quot; no diretório bin do Tomcat.

Depois que o servidor for iniciado, verifique se ele está configurado corretamente abrindo *https:// license-server-host:port/flashaccess server/nomedousuário/flashaccess/license/v1* em uma janela do navegador. Se a configuração do locatário tiver sido carregada com êxito, uma mensagem de confirmação será exibida.
