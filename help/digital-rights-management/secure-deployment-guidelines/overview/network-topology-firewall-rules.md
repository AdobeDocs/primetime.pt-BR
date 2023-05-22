---
description: Ao determinar suas regras de firewall, considere os seguintes tipos de URLs
title: Regras de firewall
exl-id: 3f6f6d1a-5759-43b3-9f62-6feb02e0a5c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Regras de firewall {#firewall-rules}

Ao determinar suas regras de firewall, considere os seguintes tipos de URLs:

## URLs de entrada {#section_F111526A9DB844CBBF21A3CAE5F50880}

Você pode configurar o firewall externo para que ele exponha apenas os URLs para a funcionalidade do aplicativo que você deseja fornecer aos usuários finais.

Os usuários externos podem acessar os seguintes URLs usando o firewall externo:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_bqs_whz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">URL raiz </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Finalidade </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /flashaccess/getServerVersion/v3</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Para determinar a versão do servidor. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul_xr4_hdn_44"> 
     <li id="li_8C68877B0FAF427490BF826FB12BE2F2"><span class="filepath"> /flashaccess/authn/v1/*</span> </li> 
     <li id="li_BF44753FF42E40BD911D04996B962188"><span class="filepath"> /flashaccess/authn/v3/*</span> </li> 
     <li id="li_9B633CDDB3844644BD8E3BFE80FD1672"><span class="filepath"> /flashaccess/authn/v4/*</span> </li> 
     <li id="li_01B2E17BF4DB456383FD6E18E9DE28F5"><span class="filepath"> /flashaccess/authn/v5/*</span> </li> 
     <li id="li_096D349CCD7945B387CB80C3E99063C7"><span class="filepath"> /flashaccess/authn/v6/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Para autenticar usuários. </p> <p>Essa URL deve estar acessível se você usar as APIs do cliente Adobe Primetime DRM para autenticação de usuário. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul_yxs_rdn_44"> 
     <li id="li_4BEB80F46E8D4D0F90F9998AB7FAAEB7"><span class="filepath"> /flashaccess/license/v1/*</span> </li> 
     <li id="li_20DDE5B03284436F9DEF794867AFBC53"><span class="filepath"> /flashaccess/license/v3/*</span> </li> 
     <li id="li_6555F8689FF945338579C58DADC2E36D"><span class="filepath"> /flashaccess/license/v4/*</span> </li> 
     <li id="li_5112283BDCF1457099056733B633FAF1"><span class="filepath"> /flashaccess/license/v5/*</span> </li> 
     <li id="li_F73A570E2C1A45E1BBF21C1468B90D3A"><span class="filepath"> /flashaccess/license/v6/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Para emitir licenças para usuários finais. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul_ibl_5dn_44"> 
     <li id="li_3B984F500F6848EDBBA5ADC570417E34"><span class="filepath"> /flashaccess/sync/v3</span> </li> 
     <li id="li_3204CF10D68C4FDB97E369BD63FA3C2B"><span class="filepath"> /flashaccess/sync/v4</span> </li> 
     <li id="li_2222D27F73D0421396A4F0E18140B3F9"><span class="filepath"> /flashaccess/sync/v5</span> </li> 
     <li id="li_18020B7CE36B4C209F65FF01A00B6737"><span class="filepath"> /flashaccess/sync/v6/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Para sincronizar solicitações. </p> <p>Esta URL deve estar acessível se você especificar os requisitos de sincronização em suas licenças. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul_plq_ydn_44"> 
     <li id="li_61F51463E2BF4ABCA4F209754D8A8052"><span class="filepath"> /flashaccess/domain/v3</span> </li> 
     <li id="li_898E849D7EA24045978D35C336AEEAFE"><span class="filepath"> /flashaccess/domain/v4</span> </li> 
     <li id="li_CF7590FDAF694EDF9685434BE8EE10CA"><span class="filepath"> /flashaccess/domain/v5</span> </li> 
     <li id="li_CA73424FDFAA4BD8BBE2C1AD165D2C31"><span class="filepath"> /flashaccess/domain/v6/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Para registrar domínios. </p> <p>Este URL deve estar acessível se você implementar o suporte de domínio. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul_btm_c2n_44"> 
     <li id="li_8A0DC38312CB4D3DBD313B3DE089D39E"><span class="filepath"> /flashaccess/dereg/v3</span> </li> 
     <li id="li_5BA24F70381F465F832FF28925B622C1"><span class="filepath"> /flashaccess/dereg/v4</span> </li> 
     <li id="li_C761F14F3C97479CBA5C255739E01A28"><span class="filepath"> /flashaccess/dereg/v5</span> </li> 
     <li id="li_23A8AABE7499488EB61B7ED27CC65098"><span class="filepath"> /flashaccess/dereg/v6/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Para cancelar o registro de domínios. </p> <p>Este URL deve estar acessível se você implementar o suporte de domínio. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /flashaccess/headerconversion/v1/*</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Para permitir que o cliente converta metadados de DRM do FMRMS 1.x em metadados de DRM do Primetime. </p> <p>Observação: este URL deve usar SSL (HTTPS). </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /edcws/services/urn:EDCLicenseService/*</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL do serviço Web LiveCycle Rights Management ES. Se o conteúdo tiver sido publicado usando uma versão anterior do FMRMS, este URL permitirá que clientes mais antigos se conectem ao servidor. Esses clientes são solicitados a atualizar para o Adobe Primetime DRM. </p> <p class="- topic/p ">Observação: este URL deve usar SSL (HTTPS). </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul_382B69AB07204DD596BB375132224D96"> 
     <li id="li_24B4D42BECF8405281C73B782F8E7310"><span class="filepath"> /flashaccess/lreturn/v5</span> </li> 
     <li id="li_6B79563205D1421F89131E650D71E83B"><span class="filepath"> /flashaccess/lreturn/v6</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p>Para retornar licenças. </p> <p> O URL deve estar acessível se você implementar o suporte de retorno de licença. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>O firewall interno deve permitir conexões somente com o servidor de licenças do Primetime DRM por meio do proxy reverso e somente com os URLs na tabela. Para melhorar a escalabilidade, use HTTP para as conexões entre o proxy reverso e o Primetime DRM.

## URLs de saída {#section_FFF9F7BB353149F4A27F8788E9934A48}

URLs de saída permitem que o servidor de licenças baixe as CRLs do Adobe.

Esta é uma lista dos URLs de saída que você pode usar:

* `https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl`
* `https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl`
* `https://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl`
* `https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl`
