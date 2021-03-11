---
description: Para começar a usar o Primetime DRM Cloud, fornecido pela ExpressPlay, é necessário configurar contas Adobe Cert e ExpressPlay com a ajuda do representante do Adobe.
title: Obter provisionamento (contas etc.)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Obter Provisionamento (Contas, etc.) {#get-provisioned-accounts-etc}

Para começar a usar o Primetime DRM Cloud, fornecido pela ExpressPlay, é necessário configurar contas Adobe Cert e ExpressPlay com a ajuda do representante do Adobe.

1. Entre em contato com o representante do Adobe e solicite as contas Adobe Cert e ExpressPlay necessárias para implementar o Multi-DRM com TVSDK.

       Forneça ao representante do Adobe o endereço de email que você usará como ponto de contato. O Adobe cria duas contas para você:
   
   * ***Conta do Portal de Certificados***  - ( <span></span>https://certportal.primetime.adobe.com) : A equipe de gerenciamento de registro de certificado DRM/ ** Acesso ao Adobe / Primetime envia um email para os endereços fornecidos. O email inclui o certificado de Adobe, juntamente com um link para a documentação de inscrição do certificado do portal Adobe (os documentos mais recentes estão aqui: [Guia de Registro de Certificado](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md)).

   * ***Conta do ExpressPlay***  - o Adobe envia um email contendo um link usado para se registrar na sua conta do ExpressPlay Admin.

1. Faça logon no portal do Adobe cert usando seu Adobe ID (use o mesmo endereço de email fornecido ao representante do Adobe). Se você ainda não tiver uma Adobe ID, poderá criar uma rapidamente seguindo o link *Get an Adobe ID* no portal de certificado:

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. No portal Adobe cert , solicite um certificado *Trial*.

   Para o teste Multi-DRM, um único certificado de avaliação cobrirá todos esses aspectos da proteção de conteúdo: embalagem, licenciamento e transporte. Você precisará fornecer seu próprio [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md) para fazer uma solicitação de certificado:
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   O Adobe enviará um email indicando a aceitação ou rejeição de sua solicitação de certificado. Você pode ver o status da solicitação de certificado na guia *Histórico de solicitações* no portal de certificado:
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. Crie a conta do ExpressPlay Admin.

   Siga o link para ExpressPlay que o Adobe forneceu. Isso abre a página *Create an Account* no ExpressPlay. Preencha as informações necessárias e envie o formulário. Você receberá um email de `operations@expressplay.com` contendo um link de ativação válido por uma semana. Após ativar, configure o serviço ExpressPlay:
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   Após criar seu serviço, você verá sua própria página de Administrador. Junto com alguns campos de rastreamento de atividade, você verá seus autenticadores de cliente de Produção e Teste *a1/> (chaves de API) e seus URLs de serviço de Produção e Teste:*

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. Se estiver usando o FairPlay, há etapas adicionais envolvidas (no site de desenvolvedor da Apple) para configurar com o ExpressPlay. Consulte [Ativar o serviço ExpressPlay para FairPlay](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay) para obter instruções.
