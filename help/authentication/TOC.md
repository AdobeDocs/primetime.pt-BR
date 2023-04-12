---
product: adobe primetime
audience: end-user
user-guide-title: Autenticação do Primetime
user-guide-description: null
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# Ajuda da autenticação do Primetime {#authentication}

+ [Visão geral da autenticação do Primetime](home.md)
+ Conceitos de autenticação do Primetime {#authentication-concepts}
   + [Papel técnico](technical-paper.md)
   + [Visão geral para programadores](programmer-overview.md)
   + [Visão geral do MVPD](mvpd-overview.md)
+ Guias de início rápido {#kickstart-guides}
   + [Guia de início rápido do programador](programmer-kickstart-guide.md)
   + [Guia de início rápido do MVPD](mvpd-kickstart-guide.md)
+ Guia de integração do programador {#programmer-integration-guide}
   + [Visão geral do guia de integração do programador](programmer-integration-guide-overview.md)
   + [O fluxo de direito do programador](entitlement-flow.md)
   + [Casos de uso do programador](programmer-use-cases.md)
   + [Transmitindo informações do cliente (dispositivo, conexão e aplicativo)](passing-client-information-device-connection-and-application.md)
   + REST API {#restapi}
      + [Visão geral da REST API](rest-api-overview.md)
      + [Livro da API REST (servidor para servidor)](rest-api-cookbook-servertoserver.md)
      + [Guia da API REST (cliente para servidor)](rest-api-cookbook-clienttoserver.md)
      + Referência da API de restante {#rest-api-reference}
         + [Referência da API REST](rest-api-reference.md)
         + [Solicitação de código de registro](registration-code-request.md)
         + [Registro de Devolução](return-registration-record.md)
         + [Excluir Registro](delete-registration-record.md)
         + [Fornecer Lista MVPD](provide-mvpd-list.md)
         + [Iniciar Autenticação](initiate-authentication.md)
         + [Verificar Token de Autenticação](check-authentication-token.md)
         + [Recuperar token de autenticação](retrieve-authentication-token.md)
         + [Iniciar Autorização](initiate-authorization.md)
         + [Recuperar token de autorização](retrieve-authorization-token.md)
         + [Obter token de mídia curta](obtain-short-media-token.md)
         + [Verificar o fluxo de autenticação por aplicação web de segunda tela](check-authentication-flow-by-second-screen-web-app.md)
         + [Recuperar Lista de Recursos Pré-Autorizados](retrieve-list-of-preauthorized-resources.md)
         + [Recuperar a lista de recursos pré-autorizados pelo aplicativo web de segunda tela](retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md)
         + [Iniciar logout](initiate-logout.md)
         + [Metadados do usuário](user-metadata.md)
         + [Recuperar solicitação de perfil](retrieve-profilerequest.md)
         + [Troca de Token](token-exchange.md)
         + [Visualização gratuita do Temp Pass and Promotional Temp Pass](free-preview-for-temp-pass-and-promotional-temp-pass.md)
   + SDK do AccessEnabler {#accessenabler-sdk}
      + SDK do JavaScript {#javascriptsdk}
         + [Visão geral do SDK do JavaScript](javascript-sdk-overview.md)
         + [Guia do SDK do JavaScript](javascript-sdk-cookbook.md)
         + [Referência da API do SDK do JavaScript](javascript-sdk-api-reference.md)
         + Diretrizes {#js-sdk-guidelines}
            + [Logon e Logout sem Atualização](refreshless-login-and-logout.md)
         + API JavaScript {#js-api}
            + [Pré-autorizar](js-preauthorize.md)
      + SDK do iOS/tvOS {#ios-sdk}
         + [Visão geral do SDK do iOS/tvOS](iostvos-sdk-overview.md)
         + [Guia do SDK do iOS/tvOS](iostvos-sdk-cookbook.md)
         + [Referência da API do SDK do iOS/tvOS](iostvos-sdk-api-reference.md)
         + Diretrizes {#ios-tvos-sdk-guidelines}
            + [Registro do aplicativo iOS/tvOS](iostvos-application-registration.md)
            + Diretrizes de migração {#migration-guidelines}
               + [Guia de migração do iOS/tvOS v3.x](iostvos-v3x-migration-guide.md)
         + API do iOS/tvOS {#ios-tvos-api}
            + [Pré-autorizar](preauthorize.md)
      + Android SDK {#androidsdk}
         + [Visão geral do SDK do Android](android-sdk-overview.md)
         + [Guia do SDK do Android](android-sdk-cookbook.md)
         + [Referência da API do SDK do Android](android-sdk-api-reference.md)
         + Diretrizes {#androidguidelines}
            + [Registro do aplicativo Android](android-application-registration.md)
            + [Android SDK com registro de cliente dinâmico](android-sdk-with-dynamic-client-registration.md)
         + API do Android{#androidapi}
            + [Pré-autorizar](preauthorize-android.md)
      + Amazon FireOS SDK {#fireossdk}
         + [Amazon FireOS SSO - Guia de lançamento do programador](amazon-firetv-sso-programmer-kickoff-guide.md)
         + [Amazon FireOS SSO usando o guia da API sem cliente](amazon-fireos-sso-using-clientless-api-cookbook.md)
         + [Visão geral técnica do Amazon FireOS](amazon-fireos-technical-overview.md)
         + [Guia de integração do Amazon FireOS](amazon-fireos-integration-cookbook.md)
         + [Referência da API do Amazon FireOS](amazon-fireos-native-client-api-reference.md)
         + [Registro do aplicativo Amazon FireOS](amazon-fireos-application-registration.md)
         + [SDK do FireOS com registro de cliente dinâmico](fireos-sdk-with-dynamic-client-registration.md)
   + Platform SSO {#platform-sso}
      + Apple SSO {#apple-sso}
         + [Visão geral do Apple SSO](apple-sso-overview.md)
         + [Guia SSO do Apple (REST API)](apple-sso-cookbook-rest-api.md)
         + [Guia SSO do Apple (SDK do iOS/tvOS)](apple-sso-cookbook-iostvos-sdk.md)
      + Roku SSO {#roku-sso}
         + [Roku SSO](roku-sso-overview.md)
   + Metadados de conteúdo {#content-metadata}
      + [Identificação do recurso protegido](identify-protected-resources.md)
   + Integração do servidor de conteúdo {#content-serv-int}
      + [Como integrar o Verificador de token de mídia](media-token-verifier-int.md)
   + Apêndices {#appendices}
      + [Dicas de depuração](appendix-b-debugging-tips.md)
+ Guia de integração do MVPD {#mvpd-int-guide}
   + [Recursos de integração](mvpd-integr-features.md)
   + [Autenticação](authn-usecase.md)
   + [Autenticação usando o protocolo OAuth 2.0](authn-oauth2-protocol.md)
   + [Autorização](authz-usecase.md)
   + [Autorização prévia](mvpd-preflight-authz.md)
   + [Logout do MVPD](usecase-mvpd-logout.md)
   + [Troca de metadados de conteúdo](mvpd-content-metadata-exchange.md)
   + [Troca de metadados do usuário](mvpd-user-metadata-exchng.md)
   + [Serviço Web MVPD Proxy](proxy-mvpd-webserv.md)
   + [Integração de SAML do MVPD proxy](proxy-mvpd-saml-int.md)
   + [Escopo do provedor de serviços](serv-provider-scoping.md)
   + [Endereços IP permitidos do MVPD](mvpd-listing-ip-addres.md)
+ Recursos de autenticação do Primetime {#auth-features}
   + Integração do Adobe Analytics {#analytics-int}
      + [Integração dos dados do lado do servidor de autenticação do Primetime ao Adobe Analytics](integrate-authn-servr-data-analytics.md)
      + [Uso de Experience Cloud ID na autenticação do Primetime](exp-cloud-id-authn.md)
   + Monitoramento do serviço de direito {#entitlement-service-monitoring}
      + [Visão geral do monitoramento do serviço de direito](entitlement-service-monitoring-overview.md)
      + [API de monitoramento do serviço de direito](entitlement-service-monitoring-api.md)
      + [Métricas do lado do servidor](understanding-serverside-metrics.md)
   + Passagem temporária {#temp-pass}
      + [Passagem temporária](temp-pass.md)
      + [Passagem temporária promocional](promotional-temp-pass.md)
   + Logon único {#sso}
      + [Suporte para logon único](sso-support.md)
      + [SSO por autenticação passiva](sso-passive-authn.md)
   + Autenticação com base em casa {#home-based-auth}
      + [Autenticação com base em casa para TV em qualquer lugar](home-based-authn-tve.md)
      + [Status do HBA para MVPDs](hba-status-mvpds.md)
   + Metadados do usuário {#user-metadat}
      + [Metadados do usuário](user-metadata-feature.md)
   + [Autorização prévia](preflight-authz.md)
   + Relatório de erros {#error-reportn}
      + [Relatório de erros](error-reporting.md)
      + [Códigos de erro aprimorados](enhanced-error-codes.md)
   + Registro do cliente {#client-regn}
      + [Registro dinâmico de clientes](dynamic-client-registration.md)
      + [API de registro de cliente dinâmico](dynamic-client-registration-api.md)
      + [Dynamic Client Registration Management](dynamic-client-registration-management.md)
   + Serviço de degradação {#degrn-service}
      + [Visão geral da API de degradação](degradation-api-overview.md)
   + Disponibilidade da privacidade {#privacy-readiness}
      + [Visão geral do suporte de privacidade](privacy-supp-overview.md)
      + [Como fazer uma solicitação de privacidade](make-privacy-req.md)
+ Dicas e solução de problemas {#tips-troubleshoot}
   + [Permitir MVPDs na caixa de diálogo de seleção](allow-mvpd-selectn-dialog.md)
   + [Impedir que MVPDs apareçam na caixa de diálogo de seleção](prevent-mvpd-selectn-dialog.md)
+ Suporte {#support}
   + [Procedimentos de escalonamento](escalation-procedures.md)
   + [Monitoramento de PayTV do Primetime Adobe](monitoring-adobe-pay-tv-pass.md)
   + [Requisitos mínimos do sistema](minimum-system-requirements.md)
+ Notas de versão {#release-notes}
   + [Notas de versão do Primetime Authentication 2.64.1](auth-rn-2641.md)
   + [Notas de versão do Primetime Authentication 2.64](auth-rn-264.md)
   + [Notas de versão do Primetime Authentication 2.63](auth-rn-263.md)
   + [Notas de versão do Primetime Authentication iOS / tvOS 3.7.0](authn-rn-ios-tvos-370.md)
+ Notas técnicas {#tech-notes}
   + SDKs de autenticação do Primetime {#primetime-authentication-sdks}
      + [Perguntas e respostas sobre certificados](certificates-qa.md)
      + SDK do JavaScript {#javascript}
         + [Limitações do SDK JS para o navegador Safari](js-sdk-limitations-for-safari-browser.md)
         + [Atualizações de cookies - Sinalizadores SameSite e Secure](cookies-updates--samesite-and-secure-flags.md)
      + Android SDK {#android}
         + [Ativar o Acessar o logon único (SSO) do Android SDK em aplicativos Android 10](access-enabler-android-sdk-single-signon-sso-on-android-10-devices.md)
         + [Autenticação Adobe Primetime e o novo modelo de permissões &quot;Marshmallow&quot; do Android 6](adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model.md)
      + SDK do iOS/tvOS {#iostvos}
         + [Suporte a WKWebView no iOS SDK 3.1+](wkwebview-support-on-ios-sdk-31.md)
         + [Suporte SFSafariViewController no iOS SDK 3.2+](sfsafariviewcontroller-support-on-ios-sdk-32.md)
         + [SSO no iOS ao usar o Criador de acesso de autenticação do Primetime](sso-on-ios-when-using-the-primetime-authentication-access-enabler.md)
         + [Erro de Autenticação do iOS - não é possível encontrar adobepass.ios.app](ios-authentication-error-adobepassiosapp-cannot-be-found.md)
         + [Redefinir aprovação temporária no iOS](reset-temp-pass-on-ios.md)
         + [Depuração do SDK do AccessEnabler iOS/tvOS usando registros de aplicativos do Console](debugging-the-accessenabler-iostvos-sdk-using-console-app-logs.md)
         + [Caminho de atualização do AccessEnabler iOS/tvOS 3.7.0](accessenabler-iostvos-370-upgrade-path.md)
   + Ambientes de autenticação do Primetime {#primetime-authentication-environments}
      + [Compreensão dos ambientes do Adobe](understanding-the-adobe-environments.md)
      + [Como configurar seu ambiente e testar no Pre-Qual](setting-up-your-environment-and-testing-in-prequal.md)
      + [Como testar os fluxos de autenticação e autorização usando o site de teste Adobe API](test-authn-authz-flows-using-adobes-api-test-site.md)
   + API sem cliente {#clientless-api}
      + [Implementação de API sem cliente - Códigos de erro / mensagens com motivo provável / causa](clientless-api-implementation-error-codes--messages-with-probable-reason--cause.md)
      + [Fluxo da API sem cliente na ausência de ID do dispositivo](clientless-api-flow-in-the-absence-of-device-id.md)
      + [Sem cliente: Evite usar &#39;&amp;&#39;reg_code na solicitação /authentication](clientless-avoid-using-reg-code-in-authenticate-request.md)
      + [Ativando os serviços de direito do Primetime para um programador no Xbox 360 e XboxOne sem cliente](enabling-primetime-entitlement-services-for-a-programmer-on-xbox-360-and-xboxone-clientless-solution.md)
      + [Tipo de dispositivo sem cliente e métricas](benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)
   + Experiência do usuário {#user-exp}
      + [Como migrar a página de logon do MVPD do iFrame para pop-up](migr-mvpd-login-iframe-popup.md)
      + [Recurso de comprovação: Como ativar, solucionar ou determinar o problema](preflight-feature.md)
   + Ferramentas e utilitários {#tools-and-utilities}
      + [Uso do proxy Charles](using-charles-proxy.md)
   + Conceitos {#concepts}
      + [Como entender IDs de usuário](understanding-user-ids.md)
+ [Guia do usuário do Painel TVE](tve-dashboard-user-guide.md)
+ [Glossário](glossary.md)
