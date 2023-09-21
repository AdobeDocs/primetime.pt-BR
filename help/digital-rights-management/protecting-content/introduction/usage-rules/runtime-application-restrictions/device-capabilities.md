---
title: Recursos do dispositivo necessários para reproduzir conteúdo protegido
description: Recursos do dispositivo necessários para reproduzir conteúdo protegido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Recursos do dispositivo necessários para reproduzir conteúdo protegido {#device-capabilities-required-to-play-protected-content}

Os recursos de dispositivo necessários especificam os recursos de hardware necessários para acessar o conteúdo. As informações sobre os recursos de hardware estão disponíveis para dispositivos que usam o kit de portabilidade.

Os seguintes atributos podem identificar os recursos do dispositivo:

<table id="table_v3n_fks_n4"> 
 <tbody> 
  <tr> 
   <td><b>Atributo</b> </td> 
   <td><b>Valores suportados</b> </td> 
   <td><b>Corresponder critérios</b> </td> 
   <td><b>Descrição</b> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Barramento acessível a não usuários </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" ou "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Correspondência exata </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Se verdadeiro, o dispositivo não deve ter um barramento acessível ao usuário. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Raiz de hardware da confiança </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" ou "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Correspondência exata </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Se verdadeiro, o dispositivo deve ter uma raiz de hardware de confiança. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Esta regra de uso é compatível com clientes Adobe Primetime DRM versões 2.0.2 e posteriores. O comportamento em clientes mais antigos depende da versão mínima do cliente suportada pelo servidor de licenças.
>
>Consulte [Versão Mínima do Cliente](../../../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
