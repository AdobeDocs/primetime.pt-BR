---
description: Personalize sua implementação de referência para integrar a autenticação do Adobe Primetime ao seu ambiente de produção.
seo-description: Personalize sua implementação de referência para integrar a autenticação do Adobe Primetime ao seu ambiente de produção.
seo-title: Integrar autenticação Primetime
title: Integrar autenticação Primetime
uuid: 34cdf1da-261e-462c-a194-4fcb439e5dfb
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Integrar autenticação Primetime {#integrate-primetime-authentication}

Personalize sua implementação de referência para integrar a autenticação do Adobe Primetime ao seu ambiente de produção.

A integração da Implementação de referência do serviço de autenticação Primetime funciona prontamente como uma demonstração. No entanto, para usar a integração em um player pronto para produção, você deve implementar as seguintes personalizações:

1. Ative ou desative os fluxos de direito.

   O `EntitlementManager` deve primeiro inicializar e obter uma instância do SDK de autenticação Primetime para ser ativada. Se a biblioteca `EntitlementManager` não for inicializada, o gerenciador será desativado.
1. Ative o `EntitlementManger`, da sua classe principal de aplicativo:

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. Use a `ManagerFactory` classe para obter uma instância do `EntitlementManager`.

   Você sempre deve usar o para obter uma instância do `ManagerFactory` , já que o `EntitlementManager``ManagerFactory` mantém uma única instância do EntitlementManager para seu aplicativo. Nunca instancie as classes `EntitlementManager` ou `EntitlementManagerOn` usando seus construtores.

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   O `ManagerFactory` retorna uma instância de `EntitlementManagerOn`, com os fluxos de direito ativados, se você já tiver chamado `EntitlementManager.initializeAccessEnabler`. Se você não fizer a primeira chamada `EntitlementManager.initializeAccessEnabler`, o `ManagerFactory` retornará uma instância de `EntitlementManager`, com os fluxos de direito desativados. 1. Configure a ID do solicitante.

   A Implementação de referência vem pré-configurada com a ID do solicitante de teste definida como: &quot;REF&quot;. Você pode usar essa ID do solicitante para testar seu aplicativo. Quando você estiver pronto para usar a ID do solicitante fornecida a você pelo representante de autenticação do Primetime, atualize o arquivo do aplicativo [!DNL res/values/strings.xml] com a ID do solicitante.

   ```xml
   <!-- Programmer Requestor ID, change to ID provided by your Adobe  
        Primetime pay-TV pass representative --> 
   <string name="adobepass_requestor_id">REF</string> 
   
   <!-- Adobe Primetime pay-TV pass service provider endpoint for production 
        environment --> 
   <string name="adobepass_sp_url_production">sp.auth.adobe.com</string> 
   
   <!-- Adobe Primetime pay-TV pass service provider endpoint for staging  
        environment --> 
   <string name="adobepass_sp_url_staging">sp.auth-staging.adobe.com</string>
   ```

   Além disso, talvez seja necessário alterar os URLs que seu aplicativo usa para se conectar aos serviços de autenticação Primetime. Eles incluem os URLs do servidor de produção e preparo de autenticação Primetime e um URL para um serviço de verificação de token. Consulte seu representante do Adobe Primetime para obter detalhes. 1. Assine a ID do solicitante.

   Para estabelecer a identidade do Programador no sistema de autenticação Primetime, a ID do solicitador do Programador é enviada para o sistema de autenticação Primetime. Como uma camada adicional de segurança, a ID do solicitante deve ser assinada pelo Programador antes de enviá-la para a Adobe. A Adobe recomenda que o Programador configure um serviço para assinar a ID do solicitante em uma rede confiável.

   A implementação da referência Primetime demonstra como assinar a ID do solicitante, no entanto, isso é apenas para fins de demonstração. A Adobe recomenda enfaticamente que o certificado de assinatura e o código do gerador de assinatura, em `com.adobe.primetime.reference.crypto`, não sejam incluídos em um aplicativo de produção. Em vez disso, você deve movê-lo para um serviço em rede confiável.

1. Configure o ambiente do servidor.

   O serviço de autenticação Primetime pode ser executado em dois ambientes separados:

   * Preparação - o ambiente de preparo é usado para testar seu aplicativo.
   * Produção - o ambiente de produção é usado para implantações ao vivo do aplicativo.
   Você define os URIs para os ambientes de armazenamento temporário e de produção usando o aplicativo, no entanto, é necessário definir qual deles é usado pelo aplicativo dentro do código. Na `com.adobe.primetime.reference.manager.EntitlementManger` classe, defina a `environmentUri` variável como `STAGING_URI` ou `PRODUCTION_URI` dependendo de qual ambiente do serviço de autenticação Primetime você está usando.

   >[!NOTE]
   >
   >A ID do solicitante (&quot;REF&quot;) fornecida só deve ser usada com o ambiente de preparo.

   `com.adobe.primetime.reference.manager.EntitlementManager`:

   ```java
     // Adobe Primetime authentication service provider endpoint for production environment 
     PRODUCTION_URI = 
         application.getResources().getString(R.string.adobepass_sp_url_production); 
   
     // Adobe Primetime authentication service provider endpoint for staging environment 
     STAGING_URI = 
       application.getResources().getString(R.string.adobepass_sp_url_staging); 
   
     // Set to STAGING_URI when testing against the staging/test environment 
     // Set to PRODUCTION_URI when deploying the application for production use 
     String environmentUri = STAGING_URI; 
   
     // Adobe Primetime authentication service URI used by this application 
     PAYTV_PASS_URI = environmentUri + "/adobe-services"; 
   
     // Token Verification Service URL 
     TVS_URL = "https://" + environmentUri + "/tvs/v1/validate";
   ```

1. Personalize a grade de seleção MVPD.

   A página de seleção do provedor de conteúdo exibe uma tabela dos nove MVPDs principais que o usuário pode selecionar. O aplicativo retira os nove principais MVPDs de uma lista ordenada dentro do aplicativo que corresponde aos MVPDs disponíveis integrados ao Programador no sistema de autenticação Primetime. A lista ordenada dos MVPDs principais é colocada na ID MVPD dentro do sistema de autenticação Primetime, não no nome de exibição MVPD. É importante verificar se as IDs MVPD na lista principal de MVPDs correspondem às IDs MVPD integradas à conta do Programador, já que em alguns casos as IDs podem ser diferentes nas integrações. Abaixo está a lista ordenada de MVPDs primários que foi encontrada na classe `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`.

   ```java
   /* Array of MVPDs to display in a Grid of icons 
   When displaying a grid, only the MVPDs which intersect this array and the 
   ArrayList of all MVPDs are displayed. 
   The array contents are ordered by display preference as only a maximum of 
   MAX_DISPLAY_ICONS are displayed. 
   */ 
   private static final String[] PRIMARY_MVPDS = { 
   "Comcast_SSO",                         // Comcast XFINITY 
   "DTV",                                 // DirectTV 
   "Dish",                                // Dish 
   "TWC",                                 // Time Warner Cable 
   "Cox",                                 // Cox 
   "Charter_Direct",                      // Charter 
   "Verizon",                             // Verizon FiOS 
   "Cablevision",                         // Cablevision Optimum 
   "ATT",                                 // AT&T U-verse 
   "Brighthouse",                         // Brighthouse 
   "Suddenlink",                          // Suddenlink 
   "Mediacom",                            // Mediacom 
   "CableOne",                            // CableOne 
   "WOW",                                 // WOW! 
   "RCN",                                 // RCN 
   "auth_atlanticbb_net",                 // Atlantic Broadband 
   "auth_armstrongmywire_com",            // Armstrong 
   "knology_auth-gateway_net",            // KNOLOGY 
   "serviceelectric_auth-gateway_net",    // Service Electric Cablevision 
   "msauth_midco_net",                    // Midcontinent Communications 
   "auth_metrocast_net",                  // MetroCast 
   "www_websso_mybrctv_com",              // Blue Ridge Communications 
   };
   ```

   A tabela a seguir fornece um exemplo de como a lista ordenada de MVPDs primários é usada. A primeira coluna lista os MVPDs integrados ao Programador. A segunda coluna é a lista ordenada (abreviada) de MVPDs. A terceira coluna é a lista de resultados usada para exibir os seis MVPDs principais para o usuário.

   Este exemplo usa os seis MVPDs principais em vez dos nove reais apenas para manter o exemplo simples. Observe como a lista de resultados contém a interseção das duas primeiras listas e tem a mesma ordem que a segunda. Além disso, observe que a AT&amp;T U-verse não está na lista final, já que apenas os seis primeiros MVPDs correspondentes são tomados.

| MVPDs disponíveis | MVPDs principais | 6 MVPDs exibidos |
|--- |--- |--- |
| <ol><li>XFINALIDADE DE COMPILAÇÃO</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>Prato</li><li>Inverso AT&amp;T</li><li>CableOne</li><li>Brighthouse</li><li>Banda larga atlântica</li><li>UAU!</li><li>MetroCast</li><li>DirectTV </li><li>Cox</li><li>Cablevision Optimum</li></ol> | <ol><li>XFINALIDADE DE COMPILAÇÃO</li><li>DirectTV</li><li>Prato</li><li> TWC</li><li>Cox</li><li>Carta</li><li>Verizon FiOS</li><li>Cablevision Optimum</li><li>Inverso AT&amp;T</li></ol> | <ol><li>XFINALIDADE DE COMPILAÇÃO</li><li>DirectTV</li><li>Prato</li><li>TWC</li><li>Cox</li><li>Cablevision Optimum</li></ol> |
