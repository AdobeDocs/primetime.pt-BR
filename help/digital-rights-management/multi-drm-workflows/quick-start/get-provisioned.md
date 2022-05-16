---
description: Para começar a usar o Primetime DRM Cloud, fornecido pela ExpressPlay, é necessário configurar contas Adobe Cert e ExpressPlay com a ajuda do representante do Adobe.
title: Obter provisionamento (contas etc.)
exl-id: 2543d997-3495-4545-9395-072c07431aba
source-git-commit: a0917e128862184ce18050792c2ee2ac265050d2
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Obter provisionamento (contas etc.) {#get-provisioned-accounts-etc}

Para começar a usar o Primetime DRM Cloud, fornecido pela ExpressPlay, é necessário configurar contas Adobe Cert e ExpressPlay com a ajuda do representante do Adobe.

1. Entre em contato com o representante do Adobe e solicite as contas Adobe Cert e ExpressPlay necessárias para implementar o Multi-DRM com TVSDK.

   Forneça ao representante do Adobe o endereço de email que você usará como ponto de contato. O Adobe cria duas contas para você:

   * ***Conta do Portal de Certificados*** - ( https://certportal.primetime.adobe.com) : O *Equipe de Gerenciamento de Inscrição de Certificados DRM de Acesso ao Adobe / Primetime* envia um email para os endereços que você os forneceu. O email inclui o certificado de Adobe, juntamente com um link para a documentação de inscrição do certificado do portal Adobe (os documentos mais recentes estão aqui: [Guia de inscrição de certificados](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md)).

   * ***Conta do ExpressPlay*** - O Adobe envia um email contendo um link usado para se registrar na sua conta do Administrador do ExpressPlay.

1. Faça logon no portal do Adobe cert usando seu Adobe ID (use o mesmo endereço de email fornecido ao representante do Adobe). Se você ainda não tiver uma Adobe ID, poderá criar uma rapidamente seguindo a variável *Obter uma Adobe ID* link do portal de certificados:

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. No portal Adobe cert , solicite um *Avaliação* cert.

   Para o teste Multi-DRM, um único certificado de avaliação cobrirá todos esses aspectos da proteção de conteúdo: embalagem, licenciamento e transporte. Você precisará fornecer seu próprio [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md) para solicitar um certificado:
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   O Adobe enviará um email indicando a aceitação ou rejeição de sua solicitação de certificado. Você pode ver o status da(s) solicitação(ões) de certificado na *Histórico da solicitação* no portal de certificado:
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. Crie a conta do ExpressPlay Admin.

   Siga o link para ExpressPlay que o Adobe forneceu. Isso abre o *Criar uma conta* em ExpressPlay. Preencha as informações necessárias e envie o formulário. Você receberá um email de `operations@expressplay.com` contém um link de ativação que funciona por uma semana. Após ativar, configure o serviço ExpressPlay:
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   Após criar seu serviço, você verá sua própria página de Administrador. Junto com alguns campos de rastreamento de atividade, você verá sua Produção e teste *autenticadores do cliente* (Chaves de API) e os URLs do serviço de Produção e Teste:

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. Se estiver usando o FairPlay, há etapas adicionais envolvidas (no site de desenvolvedor do Apple) para configurar o ExpressPlay. Consulte [Ativar o serviço ExpressPlay para FairPlay](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay) para obter instruções.
