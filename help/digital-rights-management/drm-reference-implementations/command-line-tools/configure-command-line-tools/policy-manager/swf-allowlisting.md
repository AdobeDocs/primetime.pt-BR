---
title: Lista de permissões do aplicativo SWF
description: Lista de permissões do aplicativo SWF
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Lista de permissões do aplicativo SWF {#swf-application-allowlisting}

Para lista de permissões um aplicativo SWF, siga uma destas duas estratégias:

* Você pode especificar um URL para um SWF. Essa é uma abordagem muito flexível, especialmente em um ambiente de desenvolvimento no qual você está reconstruindo seu SWF regularmente.
* Você pode especificar um SWF HASH. Este é um valor de resumo criptográfico do seu SWF. Essa abordagem é menos flexível (mas muito mais rigorosa), já que o HASH de SWF mudará quando o aplicativo for alterado e recriado. Nessa situação, todo o conteúdo vinculado ao HASH anterior não será reproduzido no novo reprodutor e terá que ser reempacotado. A variável [!DNL PolicyManager.jar] A ferramenta calculará automaticamente o hash se você especificar um [!DNL .swf] arquivo.

  Por outro lado, se estiver usando o DRM do Primetime via Flash/Adobe Media Server (FMS/AMS), você poderá fornecer o caminho para seu(s) SWF(s) específico(s), e o FMS/AMS aplicará automaticamente a função de hash nos SWF para inserção na política de DRM usada para empacotar o conteúdo transmitido pelo FMS/AMS.

Consulte `policy.allowedSWFApplication.n` in *Propriedades de configuração* para obter detalhes.
