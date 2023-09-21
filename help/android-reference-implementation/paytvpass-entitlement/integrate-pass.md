---
description: Personalize sua implementação de referência para integrar a autenticação da Adobe Primetime ao seu ambiente de produção.
title: Integrar autenticação do Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# Integrar autenticação do Primetime {#integrate-primetime-authentication}

Personalize sua implementação de referência para integrar a autenticação da Adobe Primetime ao seu ambiente de produção.

A integração da Implementação de referência do serviço de autenticação Primetime funciona como uma demonstração pronta para uso. No entanto, para usar a integração em um player pronto para produção, você deve implementar as seguintes personalizações:

1. Ative ou desative os fluxos de direito.

   A variável `EntitlementManager` Primeiro, inicialize e obtenha uma instância do SDK de autenticação do Primetime para ser habilitada. Se a variável `EntitlementManager` não inicializar essa biblioteca, o gerenciador será desativado.
1. Ativar o `EntitlementManger`, da classe do aplicativo principal:

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. Use o `ManagerFactory` classe para obter uma ocorrência de `EntitlementManager`.

   Você sempre deve usar o `ManagerFactory` para obter uma instância do `EntitlementManager`, como a `ManagerFactory` O mantém uma única instância do EntitlementManager para o seu aplicativo. Nunca instancie o `EntitlementManager` ou `EntitlementManagerOn` usando seus construtores.

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   A variável `ManagerFactory` retorna uma instância de `EntitlementManagerOn`, com os fluxos de direito ativados, se você tiver chamado anteriormente `EntitlementManager.initializeAccessEnabler`. Se você não chamar primeiro `EntitlementManager.initializeAccessEnabler`, depois o `ManagerFactory` retornará uma instância de `EntitlementManager`, com os fluxos de direito desativados. 1. Configure a ID do Solicitante.

   A Implementação de referência vem pré-configurada com a ID do solicitante de teste definida como: &quot;REF&quot;. Você pode usar essa ID de solicitante para testar seu aplicativo. Quando estiver pronto para usar a ID do solicitante fornecida a você pelo representante de autenticação do Primetime, atualize a [!DNL res/values/strings.xml] com a ID do solicitante.

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

   Além disso, talvez seja necessário alterar os URLs que seu aplicativo usa para se conectar aos serviços de autenticação do Primetime. Isso inclui os URLs do servidor de preparo e produção de autenticação do Primetime e um URL para um Serviço de verificação de token. Consulte seu representante da Adobe Primetime para obter detalhes. 1. Assine a ID do solicitante.

   Para estabelecer a identidade do Programador no sistema de autenticação do Primetime, a ID do Solicitante do Programador é enviada para o sistema de autenticação do Primetime. Como camada adicional de segurança, a ID do solicitante deve ser assinada pelo programador antes de enviá-la para o Adobe. O Adobe recomenda que o Programador configure um serviço para assinar a ID do solicitante em uma rede confiável.

   A implementação de referência do Primetime demonstra como assinar a ID do solicitante. No entanto, isso é apenas para fins de demonstração. Adobe recomenda que o certificado de autenticação e o código gerador de assinaturas, em `com.adobe.primetime.reference.crypto`, não devem ser incluídos em um aplicativo de produção. Em vez disso, você deve movê-lo para um serviço em rede confiável.

1. Configurar o ambiente do servidor.

   O serviço de autenticação do Primetime pode ser executado em dois ambientes separados:

   * Preparo - O ambiente de preparo é usado para testar o aplicativo.
   * Produção - O ambiente de produção é usado para implantações ativas do aplicativo.

   Você define os URIs para os ambientes de preparo e produção que usam o aplicativo; no entanto, deve definir qual deles é usado pelo aplicativo dentro do código. No `com.adobe.primetime.reference.manager.EntitlementManger` , defina o `environmentUri` variável para `STAGING_URI` ou `PRODUCTION_URI` dependendo do ambiente de serviço de autenticação do Primetime que você estiver usando.

   >[!NOTE]
   >
   >A ID do solicitante (&quot;REF&quot;) fornecida deve ser usada somente com o ambiente de preparo.

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

1. Personalizar a Grade de Seleção do MVPD.

   A página de seleção do provedor de conteúdo exibe uma tabela dos nove principais MVPDs que o usuário pode selecionar. O aplicativo extrai os nove principais MVPDs de uma lista ordenada dentro do aplicativo que correspondem aos MVPDs disponíveis integrados ao Programador no sistema de autenticação do Primetime. A lista ordenada dos MVPDs primários é digitada na ID do MVPD no sistema de autenticação Primetime, não no nome de exibição do MVPD. É importante verificar se as IDs de MVPD na lista de MVPDs primários correspondem às IDs de MVPD integradas à conta do Programador, pois, em alguns casos, as IDs podem ser diferentes nas integrações. Abaixo está a lista ordenada de MVPDs primários encontrados na classe `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`.

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

   A tabela a seguir fornece um exemplo de como a lista ordenada de MVPDs primários é usada. A primeira coluna lista os MVPDs integrados ao Programador. A segunda coluna é a lista ordenada (encurtada) de MVPDs. A terceira coluna é a lista de resultados usada para exibir os seis principais MVPDs para o usuário.

   Esse exemplo usa os seis principais MVPDs em vez dos nove reais apenas para manter o exemplo simples. Observe como a lista de resultados contém a interseção das duas primeiras listas e tem a mesma ordem que a segunda lista. Além disso, observe que o U-verse da AT&amp;T não está na lista final, pois apenas os primeiros seis MVPDs correspondentes são usados.

| MVPDs disponíveis | MVPDs primários | Exibidos 6 MVPDs |
|--- |--- |--- |
| <ol><li>Comcast XFINITY</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>Prato</li><li>Estorno em AT&amp;T</li><li>CableOne</li><li>Brighthouse</li><li>Banda larga atlântica</li><li>UAU!</li><li>MetroCast</li><li>DirectTV </li><li>Cox</li><li>Cablevision Optimum</li></ol> | <ol><li>Comcast XFINITY</li><li>DirectTV</li><li>Prato</li><li> TWC</li><li>Cox</li><li>Carta</li><li>Verizon FiOS</li><li>Cablevision Optimum</li><li>Estorno em AT&amp;T</li></ol> | <ol><li>Comcast XFINITY</li><li>DirectTV</li><li>Prato</li><li>TWC</li><li>Cox</li><li>Cablevision Optimum</li></ol> |
