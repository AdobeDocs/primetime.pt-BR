---
description: O Flash Media Rights Management Server 1.x e o Adobe Primetime DRM usam metadados diferentes para disponibilizar conteúdo e solicitar licenças. Para que o Primetime DRM use o conteúdo FMRMS versão 1.x, os metadados devem ser convertidos.
seo-description: O Flash Media Rights Management Server 1.x e o Adobe Primetime DRM usam metadados diferentes para disponibilizar conteúdo e solicitar licenças. Para que o Primetime DRM use o conteúdo FMRMS versão 1.x, os metadados devem ser convertidos.
seo-title: Garantia de compatibilidade com o Flash Media Rights Management Server 1.x
title: Garantia de compatibilidade com o Flash Media Rights Management Server 1.x
uuid: dd70941e-9015-4fb0-b265-557b6252e051
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Garantir a compatibilidade com o Flash Media Rights Management Server 1.x {#ensuring-compatibility-with-flash-media-rights-management-server-x}

O Flash Media Rights Management Server 1.x e o Adobe Primetime DRM usam metadados diferentes para disponibilizar conteúdo e solicitar licenças. Para que o Primetime DRM use o conteúdo FMRMS versão 1.x, os metadados devem ser convertidos.

O SDK do DRM Primetime oferece suporte às seguintes opções para conversão de metadados:

* Offline (recomendado)

   Gere os metadados do DRM do Primetime em um processo offline e armazene os metadados até que sejam solicitados por um cliente. Se os metadados forem gerados offline, o servidor de licenças não precisará de acesso aos CEKs 1.x ou à credencial do empacotador. A conversão offline do oferta melhora o desempenho, pois o License Server não precisa gerar os metadados em tempo real.
* Sob demanda

   Os metadados DRM do Primetime são gerados quando os metadados são solicitados por um cliente. Quando um cliente DRM Primetime baixa o conteúdo da versão 1.x, o cliente envia os metadados DRM para o SDK DRM Primetime. O SDK converte os metadados do DRM no formato atual, criptografa e incorpora a chave de criptografia de conteúdo (CEK) nos metadados e envia o conteúdo de volta para o cliente Primetime DRM.

   >[!NOTE]
   >
   >Os metadados do Primetime DRM 1.x não incluem o CEK.

   Para converter os metadados, o Primetime DRM requer acesso às chaves de criptografia de conteúdo Primetime DRM 1.x. Ao migrar do Flash Media Rights Management Server 1.x, você pode continuar a armazenar as chaves de criptografia de conteúdo no banco de dados ES do LiveCycle ou implementar uma solução personalizada para armazenar com segurança as chaves de criptografia de conteúdo em outro local. Se você decidir armazenar as chaves de criptografia de conteúdo no banco de dados ES do LiveCycle, siga as recomendações descritas em *Protegendo o acesso a conteúdo sigiloso no banco de dados* em **Proteção e segurança para o LiveCycle® ES2**.

Para obter mais informações sobre como garantir a compatibilidade com o conteúdo empacotado usando o Flash Media Rights Management Server 1.x, consulte as APIs do Adobe Primetime DRM em [Adobe Primetime API References](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).
