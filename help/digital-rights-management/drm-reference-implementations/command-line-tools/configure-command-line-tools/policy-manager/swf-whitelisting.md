---
seo-title: Lista de permissões do aplicativo SWF
title: Lista de permissões do aplicativo SWF
uuid: e3021ae9-54f4-4bcf-a274-515ae765f74b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lista de permissões do aplicativo SWF{#swf-application-whitelisting}

Para adicionar um aplicativo SWF à lista de permissões, siga uma destas duas estratégias:

* Você pode especificar um URL para um SWF. Esta é uma abordagem muito flexível, especialmente em um ambiente de desenvolvimento no qual você está reconstruindo seu SWF regularmente.
* Você pode especificar um HASH SWF. Este é um valor de compilação criptográfico do seu SWF. Essa abordagem é menos flexível (mas muito mais rigorosa), já que o HASH do SWF mudará quando o aplicativo for alterado e reconstruído. Nessa situação, todo o conteúdo vinculado ao HASH anterior não será reproduzido no novo player e precisará ser reempacotado. A [!DNL PolicyManager.jar] ferramenta calculará automaticamente o hash se você especificar um [!DNL .swf] arquivo.

   Por outro lado, se você estiver usando o Primetime DRM via Flash/Adobe Media Server (FMS/AMS), poderá fornecer o caminho para seus SWFs específicos, e o FMS/AMS automaticamente hash os SWFs para que você os insira na política de DRM usada para disponibilizar o conteúdo transmitido pelo FMS/AMS.

Consulte `policy.allowedSWFApplication.n` nas propriedades ** de configuração para obter detalhes.
