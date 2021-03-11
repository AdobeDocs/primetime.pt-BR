---
title: Configuração inicial do Gerenciador de Flashes Access
description: Configuração inicial do Gerenciador de Flashes Access
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Configuração inicial do Gerenciador de Flashes Access {#initial-flash-access-manager-setup}

Use o procedimento a seguir para configurar o Gerenciador de Flashes Access:

1. Implante o Servidor do Packager. Este servidor só deve estar disponível para usuários em seu firewall (não implante este software em uma máquina voltada para o público). Para obter mais informações sobre como implantar o servidor, consulte [Implantando o servidor de licença e o pacote de pastas monitorado](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md).

   * Copie [!DNL flashaccess-packager.war] para a pasta de aplicativos Web do Tomcat.
   * Copie [!DNL flashaccess-refimpl-packager.properties] dos recursos para um local no classpath.
   * Inicie o servidor. Você verá alguns erros devido a problemas no arquivo de propriedades; isso é esperado, pois as propriedades ainda não foram preenchidas.

1. Instale o aplicativo AIR do Flash Access Manager inicializando o arquivo [!DNL .air] (requer o AIR 1.5 ou superior).
1. Inicie o aplicativo AIR do Flash Access Manager.

   Se o servidor estiver sendo executado em outro lugar que não `https://localhost:8080*`, você verá erros informando que o aplicativo não pode se conectar ao servidor. Ignore a caixa de diálogo de erro e preencha o URL correto para o URL do servidor do pacote na guia Preferências. Se o servidor estiver sendo executado no URL especificado e o arquivo de propriedades estiver no classpath, a tela Preferências será preenchida com os valores no arquivo de propriedades. Depois de definir o URL do servidor do empacotador, o aplicativo AIR lembra dessa configuração e você não precisará inseri-lo na próxima vez que iniciar o aplicativo.
1. Preencha os valores na guia Preferências e clique em **[!UICONTROL Save]**.
1. Se quiser usar as Pastas vigiadas, será necessário reiniciar o servidor para recuperar dos erros que você viu na Etapa 3. Se as preferências estiverem configuradas corretamente, nenhum erro será exibido durante a inicialização.

