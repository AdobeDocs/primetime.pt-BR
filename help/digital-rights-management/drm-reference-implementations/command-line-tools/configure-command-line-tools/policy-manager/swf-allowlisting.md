---
title: Lista de permissões de aplicativos SWF
description: Lista de permissões de aplicativos SWF
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# O aplicativo SWF permite listar {#swf-application-allowlisting}

Para lista de permissões um aplicativo SWF, você pode seguir uma destas duas estratégias:

* Você pode especificar um URL para um SWF. Essa é uma abordagem muito flexível, especialmente em um ambiente de desenvolvimento no qual você está reconstruindo seu SWF regularmente.
* Você pode especificar um HASH SWF. Este é um valor de compilação criptográfica do seu SWF. Essa abordagem é menos flexível (mas muito mais rígida), já que o HASH do SWF será alterado quando o aplicativo mudar e for reconstruído. Nessa situação, todo o conteúdo vinculado ao HASH anterior não será reproduzido no novo reprodutor e terá que ser reempacotado. A ferramenta [!DNL PolicyManager.jar] calculará automaticamente o hash se você especificar um arquivo [!DNL .swf].

   Por outro lado, se estiver usando o Primetime DRM via Flash/Adobe Medium Server (FMS/AMS), você pode fornecer o caminho para seus SWFs específicos e o FMS/AMS automaticamente hash os SWFs para que você insira na política de DRM usada para empacotar o conteúdo transmitido por FMS/AMS.

Consulte `policy.allowedSWFApplication.n` em *Propriedades de configuração* para obter detalhes.
