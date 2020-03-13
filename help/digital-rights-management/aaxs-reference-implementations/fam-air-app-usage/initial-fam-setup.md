---
description: nulo
seo-description: nulo
seo-title: Configuração inicial do Flash Access Manager
title: Configuração inicial do Flash Access Manager
uuid: e9041f7c-b098-4121-88bf-ff3e6369e01b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configuração inicial do Flash Access Manager {#initial-flash-access-manager-setup}

Use o seguinte procedimento para configurar o Flash Access Manager:

1. Implante o servidor Packager. Este servidor só deve estar disponível para usuários dentro do firewall (não implante este software em uma máquina voltada para o público). Para obter mais informações sobre como implantar o servidor, consulte [Implantação do servidor de licenças e do empacotador de pastas](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md)assistido.

   * Copie [!DNL flashaccess-packager.war] para a pasta de aplicativos da Web do Tomcat.
   * Copie [!DNL flashaccess-refimpl-packager.properties] de recursos para um local no classpath.
   * Inicie o servidor. Você verá alguns erros devido a problemas no arquivo de propriedades; isso é esperado, pois as propriedades ainda não foram preenchidas.

1. Instale o aplicativo Flash Access Manager AIR iniciando o [!DNL .air] arquivo (requer AIR 1.5 ou superior).
1. Inicie o aplicativo Flash Access Manager AIR.

   Se o servidor estiver sendo executado em outro lugar que não [*!DNL https:// localhost:8080*], você verá erros informando que o aplicativo não pode se conectar ao servidor. Descarte a caixa de diálogo de erro e preencha o URL correto para o URL do servidor Packager na guia Preferências. Se o servidor estiver sendo executado no URL especificado e o arquivo de propriedades estiver no classpath, a tela Preferências será preenchida com os valores no arquivo de propriedades. Depois de definir o URL do servidor do empacotador, o aplicativo AIR se lembra dessa configuração e você não precisará inseri-la na próxima vez que iniciar o aplicativo.
1. Preencha os valores na guia Preferências e clique em **[!UICONTROL Save]**.
1. Se quiser usar as Pastas monitoradas, será necessário reiniciar o servidor para recuperar dos erros que você viu na Etapa 3. Se as preferências estiverem configuradas corretamente, nenhum erro será exibido durante a inicialização.

