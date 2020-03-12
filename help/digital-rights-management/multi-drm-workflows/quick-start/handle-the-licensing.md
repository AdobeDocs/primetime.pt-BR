---
description: O licenciamento é o principal mecanismo pelo qual os usuários têm permissão ou a capacidade de reproduzir um conteúdo protegido de vídeo é negada. Um usuário legítimo (autorizado) pode receber uma licença (uma chave) para descriptografar e reproduzir uma parte específica do conteúdo criptografado do provedor de conteúdo.
seo-description: O licenciamento é o principal mecanismo pelo qual os usuários têm permissão ou a capacidade de reproduzir um conteúdo protegido de vídeo é negada. Um usuário legítimo (autorizado) pode receber uma licença (uma chave) para descriptografar e reproduzir uma parte específica do conteúdo criptografado do provedor de conteúdo.
seo-title: Licenciamento
title: Licenciamento
uuid: 9f433d62-5609-4d88-95fd-c1e7c0f6aa75
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Licenciamento{#licensing}

O licenciamento é o principal mecanismo pelo qual os usuários têm permissão ou a capacidade de reproduzir um conteúdo protegido de vídeo é negada. Um usuário legítimo (autorizado) pode receber uma licença (uma chave) para descriptografar e reproduzir uma parte específica do conteúdo criptografado do provedor de conteúdo.

Antes que seu aplicativo ou página da Web em um dispositivo de usuário final possa reproduzir conteúdo protegido por DRM, ele deve adquirir um token de um servidor de direitos ou vitrines que você, o cliente, opere. A Adobe fornece um servidor de referência de amostra para essa finalidade: Servidor [de referência: Servidor de direito ExpressPlay de amostra (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

Seu servidor de direito ou vitrine solicitará um token de licença do ExpressPlay Server relevante somente depois de verificar com seus próprios sistemas de back-end para determinar se o usuário específico está autorizado a assistir ao conteúdo solicitado. A resposta retornada da solicitação do token de licença é um URL pronto para uso para o servidor de licença ou a resposta contém o URL em uma estrutura JSON, dependendo da solução DRM com a qual você está trabalhando.

>[!NOTE]
>
>A solicitação de token de licença não pode ser feita do próprio cliente:
>1. Os direitos devem ser verificados num ambiente fidedigno; e
>1. O autenticador do cliente deve ser mantido em segredo.


1. Faça a solicitação do token de licença.

   Para um cenário de início rápido, no qual você deseja apenas verificar se os vários componentes envolvidos estão trabalhando juntos, é possível usar algo como [!DNL curl] para fazer sua solicitação de token de licença (em vez de inicialmente colocar um aplicativo em funcionamento e testar chamadas a partir daí). Por exemplo:

   * Widevine:

   ```
   curl "https://wv-gen.test.expressplay.com/hms/wv/token?customerAuthenticator= 
   <Customer Authenticator> 
   &kid 
   <indexterm>
   CEKSID 
     <indexterm>
     as query parameter kid 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEKSID> 
      &contentKey 
    <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>WidevineToken 
   ```

   Token de teste da Widevine de amostra:

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   Observe que a resposta da Widevine é uma string de URL &quot;pronta para uso&quot;.

   * PlayReady:

   ```
   curl "https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator= 
   <Customer Authenticator> 
      &kid 
   <indexterm>
   CEKSID 
   <indexterm>
   as query parameter kid 
   <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<Key ID> 
      &contentKey 
   <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>playreadyToken
   ```

   Amostra do token de teste PlayReady:

   ```
   {"licenseAcquisitionUrl":"https://pr.test.expressplay.com/playready/RightsManager.asmx", 
   "token":"AQAAAxBbWv4AAABgV8_GaWjU80mObLQdfwEdy1lenXmcqvx5VLyqixigtwXLthzjPxq9QDT-TYbudNrMSOpUAy 
   G_2Qt8RdTGJ2_Q_xtRfnj7H6C-yt6By40IhNaSQ0nNYUsY1_MtCrHXIltlVhN2Ekr_RNyTNvCjYs0V5TqzOPY"} 
   ```

   Observe que a resposta PlayReady é um objeto JSON, com URL e elementos de token separados.

   * FairPlay:

   ```
   curl "https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
    <Customer Authenticator> 
    &kid 
    <indexterm>
      CEKSID 
    <indexterm>
      as query parameter kid 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<Key ID> 
          &contentKey 
    <indexterm>
      CEK 
    <indexterm>
      as query parameter contentKey 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
    &iv=<IV ID> 
    &<Any additional licensing attributes desired>"
   ```

   Amostra do token de teste do FairPlay:

   ```
   https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
   AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
   RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
   O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
   ```

   Observe que a resposta do FairPlay é uma string de URL &quot;pronta para uso&quot;.
