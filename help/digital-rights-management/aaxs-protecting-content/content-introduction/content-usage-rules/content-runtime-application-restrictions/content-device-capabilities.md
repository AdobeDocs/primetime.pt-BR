---
title: Recursos do dispositivo necessários para reproduzir conteúdo protegido
description: Recursos do dispositivo necessários para reproduzir conteúdo protegido
copied-description: true
exl-id: 5f2089e9-3176-46a7-9998-2dad0e77e453
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Recursos do dispositivo necessários para reproduzir conteúdo protegido {#device-capabilities-required-to-play-protected-content}

Especifica os recursos de hardware necessários para acessar o conteúdo. As informações sobre os recursos de hardware estão disponíveis para dispositivos que usam o kit de portabilidade.

Os recursos do dispositivo podem ser identificados pelos atributos especificados na tabela a seguir:

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
>Esta regra de uso é suportada pelos clientes Adobe Access versões 2.0.2 e superiores. O comportamento em clientes mais antigos depende da versão mínima do cliente suportada pelo servidor de licenças. Consulte [Versão Mínima do Cliente](../../../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md).
