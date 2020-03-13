---
description: Para começar a usar a Primetime DRM Cloud, fornecida pela ExpressPlay, é necessário configurar as contas do Adobe Cert e ExpressPlay com a ajuda do seu representante da Adobe.
seo-description: Para começar a usar a Primetime DRM Cloud, fornecida pela ExpressPlay, é necessário configurar as contas do Adobe Cert e ExpressPlay com a ajuda do seu representante da Adobe.
seo-title: Obter provisionamento (contas etc.)
title: Obter provisionamento (contas etc.)
uuid: 51b95676-2121-4d8b-8756-9fd097185a13
translation-type: tm+mt
source-git-commit: 9792aff8586c46aabb5bfb70864cfe98c28e602d

---


# Obter provisionamento (contas etc.) {#get-provisioned-accounts-etc}

Para começar a usar a Primetime DRM Cloud, fornecida pela ExpressPlay, é necessário configurar as contas do Adobe Cert e ExpressPlay com a ajuda do seu representante da Adobe.

1. Entre em contato com seu representante da Adobe e solicite as contas do Adobe Cert e do ExpressPlay de que você precisará para implementar o Multi-DRM com TVSDK.

       Forneça ao seu representante da Adobe o endereço de email que você usará como ponto de contato. A Adobe então cria duas contas para você:
   
   * ***Conta*** do Portal de certificados - (<span></span>https://certportal.primetime.adobe.com) : A equipe *de gerenciamento de inscrição de certificados DRM do* Adobe Access / Primetime envia um email para os endereços fornecidos. O email inclui o URL do portal de certificados da Adobe, juntamente com um link para a documentação de inscrição de certificados da Adobe (os documentos mais recentes estão aqui: Guia [de inscrição de](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md)certificados).

   * ***Conta*** do ExpressPlay - a Adobe envia um email com um link que você usa para se registrar na sua conta do ExpressPlay Admin.

1. Faça logon no portal de certificados da Adobe usando sua Adobe ID (use o mesmo endereço de email fornecido ao seu representante da Adobe). Se você ainda não tiver uma Adobe ID, poderá criar uma rapidamente seguindo o link *Obter uma Adobe ID* no portal de certificados:

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. No portal de certificados da Adobe, solicite um certificado de *avaliação* .

   Para a avaliação de Multi-DRM, um único certificado de avaliação cobrirá todos estes aspectos da proteção de conteúdo: embalagem, licenciamento e transporte. Será necessário fornecer seu próprio [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md) para fazer uma solicitação de certificado:
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   A Adobe enviará um email indicando a aceitação ou rejeição de sua solicitação de certificado. Você pode ver o status de sua solicitação(s) de certificado na guia Histórico *de* solicitações no portal de certificados:
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. Crie sua conta de administrador do ExpressPlay.

   Siga o link para o ExpressPlay fornecido pela Adobe a você. Isso abre a página *Criar uma conta* no ExpressPlay. Preencha as informações necessárias e envie o formulário. Você receberá um email com um link de ativação `operations@expressplay.com` válido por uma semana. Depois de ativar, configure o serviço ExpressPlay:
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   Ao criar seu serviço, você receberá sua própria página de Administrador. Junto com alguns campos de rastreamento de atividade, você verá os autenticadores ** de clientes de Produção e Teste (chaves de API) e os URLs de serviço de Produção e Teste:

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. Se você estiver usando o FairPlay, há etapas adicionais envolvidas (no site de desenvolvedores da Apple) para configurar o ExpressPlay. Consulte [Habilitar o serviço ExpressPlay para o FairPlay](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay) para obter instruções.
