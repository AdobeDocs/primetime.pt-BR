---
description: Personalize sua implementação de referência para integrar a autenticação do Adobe Primetime para seu ambiente de produção.
title: Integração da autenticação do Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---


# Integrar autenticação do Primetime {#integrate-primetime-authentication}

Personalize sua implementação de referência para integrar a autenticação do Adobe Primetime para seu ambiente de produção.

A integração de implementação de referência do serviço de autenticação do Primetime funciona pronta para uso como uma demonstração. No entanto, para usar a integração em um reprodutor pronto para produção, você deve implementar as seguintes personalizações:

1. Ative ou desative os fluxos de direito.

   O `EntitlementManager` deve primeiro inicializar e obter uma instância do SDK de autenticação do Primetime para ser habilitada. Se o `EntitlementManager` não inicializar essa biblioteca, o gerenciador será desativado.
1. Ative o `EntitlementManger`, da classe de aplicativo principal:

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. Use a classe `ManagerFactory` para obter uma instância do `EntitlementManager`.

   Você sempre deve usar o `ManagerFactory` para obter uma instância do `EntitlementManager`, pois o `ManagerFactory` mantém uma única instância do EntitlementManager para seu aplicativo. Nunca instancie as classes `EntitlementManager` ou `EntitlementManagerOn` usando seus construtores.

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   O `ManagerFactory` retorna uma instância de `EntitlementManagerOn`, com os fluxos de direito ativados, se você chamou anteriormente de `EntitlementManager.initializeAccessEnabler`. Se você não chamar `EntitlementManager.initializeAccessEnabler` pela primeira vez, `ManagerFactory` retornará uma instância de `EntitlementManager`, com os fluxos de direito desativados. 1. Configure a ID do solicitante.

   A implementação de referência vem pré-configurada com a ID de solicitação de teste definida como: &quot;REF&quot;. Você pode usar essa ID do Solicitante para testar seu aplicativo. Quando estiver pronto para usar a ID do Solicitante fornecida a você pelo representante de autenticação do Primetime, atualize o arquivo [!DNL res/values/strings.xml] do aplicativo com sua ID do Solicitante.

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

   Além disso, pode ser necessário alterar os URLs usados pelo aplicativo para se conectar aos serviços de autenticação do Primetime. Isso inclui os URLs do servidor de preparação e produção da autenticação do Primetime e um URL para um serviço de verificação de token. Consulte seu representante da Adobe Primetime para obter detalhes. 1. Assine a ID do solicitante.

   Para estabelecer a identidade do Programador no sistema de autenticação Primetime, a ID do Solicitante do Programador é enviada para o sistema de autenticação Primetime. Como camada adicional de segurança, a ID do solicitante deve ser assinada pelo programador antes de enviá-la para o Adobe. O Adobe recomenda que o Programador configure um serviço para assinar a ID do Solicitante em uma rede confiável.

   A implementação de referência do Primetime demonstra como assinar a ID do solicitante, no entanto, isso é apenas para fins de demonstração. A Adobe recomenda enfaticamente que o certificado de assinatura e o código do gerador de assinatura, em `com.adobe.primetime.reference.crypto`, não sejam incluídos em um aplicativo de produção. Em vez disso, você deve movê-lo para um serviço em rede confiável.

1. Configure o ambiente do servidor.

   O serviço de autenticação do Primetime pode ser executado em dois ambientes separados:

   * Armazenamento temporário - O ambiente de preparo é usado para testar seu aplicativo.
   * Produção - O ambiente de produção é usado para implantações ativas do seu aplicativo.

   Você define os URIs para os ambientes de preparação e produção usando o aplicativo, no entanto, deve definir qual deles é usado pelo aplicativo dentro do código. Na classe `com.adobe.primetime.reference.manager.EntitlementManger`, defina a variável `environmentUri` para `STAGING_URI` ou `PRODUCTION_URI`, dependendo do ambiente de serviço de autenticação do Primetime que você está usando.

   >[!NOTE]
   >
   >A ID do Solicitante (&quot;REF&quot;) fornecida só deve ser usada com o ambiente de preparo.

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

1. Personalize a Grade de Seleção MVPD.

   A página de seleção do provedor de conteúdo exibe uma tabela dos nove MVPDs principais que o usuário pode selecionar. O aplicativo extrai os nove principais MVPDs de uma lista ordenada no aplicativo que corresponde aos MVPDs disponíveis integrados ao Programador no sistema de autenticação do Primetime. A lista ordenada dos MVPDs primários é digitada na ID do MVPD dentro do sistema de autenticação do Primetime, não no nome de exibição do MVPD. É importante verificar se as IDs do MVPD na lista principal de MVPDs correspondem às IDs do MVPD integradas à conta do programador, já que em alguns casos as IDs podem ser diferentes em integrações. Abaixo está a lista ordenada de MVPDs primários encontrados na classe `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`.

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

   A tabela a seguir fornece um exemplo de como a lista ordenada de MVPDs primários é usada. A primeira coluna lista os MVPDs integrados ao Programador. A segunda coluna é a lista ordenada (reduzida) de MVPDs. A terceira coluna é a lista de resultados usada para exibir os seis MVPDs principais para o usuário.

   Este exemplo usa os seis MVPDs principais em vez dos nove reais apenas para manter o exemplo simples. Observe como a lista de resultados contém a interseção das duas primeiras listas e tem a mesma ordem da segunda lista. Além disso, observe que o inverso da AT&amp;T não está na lista final, pois apenas os seis primeiros MVPDs correspondentes são usados.

| MVPDs disponíveis | MVPDs Primários | 6 MVPDs exibidos |
|--- |--- |--- |
| <ol><li>XFINIDADE DE Comcast</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>Dish</li><li>Inverso da AT&amp;T</li><li>CableOne</li><li>Brighthouse</li><li>Banda larga atlântica</li><li>Uau!</li><li>MetroCast</li><li>DirectTV </li><li>Cox</li><li>Cablevision Optimum</li></ol> | <ol><li>XFINIDADE DE Comcast</li><li>DirectTV</li><li>Dish</li><li> TWC</li><li>Cox</li><li>Carta</li><li>Verizon FiOS</li><li>Cablevision Optimum</li><li>Inverso da AT&amp;T</li></ol> | <ol><li>XFINIDADE DE Comcast</li><li>DirectTV</li><li>Dish</li><li>TWC</li><li>Cox</li><li>Cablevision Optimum</li></ol> |
