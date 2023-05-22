---
description: Para atualizar um servidor que executa o Adobe Access Server para transmissão protegida, substitua o arquivo flashaccessserver.war implantado em seu servidor de aplicativos pelo arquivo incluído com o Acesso ao Adobe mais recente. Se quiser usar as novas opções de configuração descritas acima, atualize o flashaccess-tenant.xml do servidor. Você também precisa atualizar o jsafe.dll ou libjsafe.so para a versão incluída com o acesso Adobe mais recente.
title: Execução do Adobe Access Server para transmissão protegida
exl-id: 02ba87c9-d4ec-4d39-926e-5d98b1858349
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Execução do Adobe Access Server para transmissão protegida{#running-the-adobe-access-server-for-protected-streaming}

Para atualizar um servidor que executa o Adobe Access Server para transmissão protegida, substitua o arquivo flashaccessserver.war implantado em seu servidor de aplicativos pelo arquivo incluído com o Acesso ao Adobe mais recente. Se quiser usar as novas opções de configuração descritas acima, atualize o flashaccess-tenant.xml do servidor. Você também precisa atualizar o jsafe.dll ou libjsafe.so para a versão incluída com o acesso Adobe mais recente.

Antes de executar o Adobe Access Server para Protected Streaming, o Adobe recomenda que você verifique se os arquivos de configuração são válidos usando os utilitários fornecidos com o servidor de licenças. Para obter mais detalhes, consulte &quot;[Validador de configuração](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Para iniciar o Tomcat e o servidor de licenças, execute &quot;catalina.bat start&quot; ou &quot;catalina.sh start&quot; no diretório bin do Tomcat.

Depois que o servidor for iniciado, verifique se ele está configurado corretamente abrindo *https:// host do servidor de licenças:porta/flashaccessserver/nome-do-locatário/flashaccess/licença/v1* em uma janela do navegador. Se a configuração do locatário foi carregada com sucesso, uma mensagem de confirmação será exibida.
