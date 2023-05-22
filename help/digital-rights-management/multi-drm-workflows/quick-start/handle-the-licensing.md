---
description: O licenciamento é o principal mecanismo pelo qual os usuários têm a capacidade de reproduzir um conteúdo de vídeo protegido. Um usuário legítimo (autorizado) pode receber uma licença (uma chave) para descriptografar e reproduzir uma parte específica do conteúdo criptografado de seu provedor de conteúdo.
title: Licenciamento
exl-id: 60aa3e77-f821-41b3-ba0e-1a2c05b2bb1a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Licenciamento{#licensing}

O licenciamento é o principal mecanismo pelo qual os usuários têm a capacidade de reproduzir um conteúdo de vídeo protegido. Um usuário legítimo (autorizado) pode receber uma licença (uma chave) para descriptografar e reproduzir uma parte específica do conteúdo criptografado de seu provedor de conteúdo.

Antes que o aplicativo ou página da Web no dispositivo de um usuário final possa reproduzir conteúdo protegido por DRM, ele deve adquirir um token de um servidor de frente de loja ou de direito que você, o cliente, opera. O Adobe fornece um exemplo de servidor de referência para esta finalidade: [Servidor de Referência: Exemplo de Servidor de Direitos ExpressPlay (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

Seu direito ou servidor de loja solicitará um token de licença do ExpressPlay Server relevante somente após verificar com seus próprios sistemas de back-end para determinar se o usuário específico está autorizado a assistir ao conteúdo solicitado. A resposta retornada pela solicitação de token de licença é um URL pronto para uso do servidor de licenças ou a resposta contém o URL em uma estrutura JSON, dependendo da solução DRM com a qual você está trabalhando.

>[!NOTE]
>
>A solicitação de token de licença não pode ser feita do próprio cliente:
>1. Os direitos devem ser verificados em um ambiente confiável; e
>1. O autenticador do cliente deve ser mantido em segredo.


1. Faça a solicitação de token de licença.

   Para um cenário de início rápido, no qual você deseja apenas garantir que os vários componentes envolvidos estejam trabalhando juntos, convém usar algo como [!DNL curl] para fazer sua solicitação de token de licença (em vez de inicialmente colocar um aplicativo em funcionamento e testar chamadas a partir daí). Por exemplo:

   * Vinha:

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

   Exemplo de token de teste Widevine:

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   Observe que a resposta do Widevine é uma string de URL &quot;pronta para uso&quot;.

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

   Exemplo de token de teste PlayReady:

   ```
   {"licenseAcquisitionUrl":"https://pr.test.expressplay.com/playready/RightsManager.asmx", 
   "token":"AQAAAxBbWv4AAABgV8_GaWjU80mObLQdfwEdy1lenXmcqvx5VLyqixigtwXLthzjPxq9QDT-TYbudNrMSOpUAy 
   G_2Qt8RdTGJ2_Q_xtRfnj7H6C-yt6By40IhNaSQ0nNYUsY1_MtCrHXIltlVhN2Ekr_RNyTNvCjYs0V5TqzOPY"} 
   ```

   Observe que a resposta do PlayReady é um objeto JSON, com URL separados e elementos de token.

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

   Token de teste FairPlay de amostra:

   ```
   https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
   AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
   RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
   O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
   ```

   Observe que a resposta do FairPlay é uma string de URL &quot;pronta para uso&quot;.
