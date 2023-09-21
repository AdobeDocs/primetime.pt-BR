---
title: Configuração inicial do Gerenciador de Flashes Access
description: Configuração inicial do Gerenciador de Flashes Access
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Configuração inicial do Gerenciador de Flashes Access {#initial-flash-access-manager-setup}

Use o procedimento a seguir para configurar o Flash Access Manager:

1. Implante o servidor de empacotamento. Este servidor só deve estar disponível para usuários dentro do firewall (não implante este software em um computador voltado para o público). Para obter mais informações sobre a implantação do servidor, consulte [Implantando o servidor de licenças e o empacotador de pastas observado](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md).

   * Copiar [!DNL flashaccess-packager.war] para a pasta de aplicativos Web do Tomcat.
   * Copiar [!DNL flashaccess-refimpl-packager.properties] de recursos para um local no classpath.
   * Inicie o servidor. Você verá alguns erros devido a problemas no arquivo de propriedades; isso é esperado, pois as propriedades ainda não foram preenchidas.

1. Instale o aplicativo Flash Access Manager AIR iniciando o [!DNL .air] arquivo (requer AIR 1.5 ou superior).
1. Inicie o aplicativo Flash Access Manager AIR.

   Se o servidor estiver sendo executado em outro lugar que não `https://localhost:8080*`, você verá erros indicando que o aplicativo não pode se conectar ao servidor. Ignore a caixa de diálogo de erro e preencha o URL correto para o URL do servidor do empacotador na guia Preferências. Se o servidor estiver sendo executado na URL especificada e o arquivo de propriedades estiver no classpath, a tela Preferências será preenchida com os valores no arquivo de propriedades. Após definir o URL do servidor do empacotador, o aplicativo AIR se lembra dessa configuração e você não precisará inseri-la na próxima vez que iniciar o aplicativo.
1. Preencha os valores na guia Preferências e clique em **[!UICONTROL Save]**.
1. Se você quiser usar as Pastas monitoradas, será necessário reiniciar o servidor para se recuperar dos erros vistos na Etapa 3. Se as preferências estiverem configuradas corretamente, nenhum erro deverá aparecer durante a inicialização.
