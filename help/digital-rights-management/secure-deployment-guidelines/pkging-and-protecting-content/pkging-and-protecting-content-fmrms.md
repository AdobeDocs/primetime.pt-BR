---
description: O Flash Media Rights Management Server 1.x e o Adobe Primetime DRM usam metadados diferentes para empacotar conteúdo e solicitar licenças. Para que o DRM do Primetime use o conteúdo FMRMS versão 1.x, os metadados devem ser convertidos.
title: Garantir a compatibilidade com o Flash Media Rights Management Server 1.x
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# Garantir a compatibilidade com o Flash Media Rights Management Server 1.x {#ensuring-compatibility-with-flash-media-rights-management-server-x}

O Flash Media Rights Management Server 1.x e o Adobe Primetime DRM usam metadados diferentes para empacotar conteúdo e solicitar licenças. Para que o DRM do Primetime use o conteúdo FMRMS versão 1.x, os metadados devem ser convertidos.

O SDK de DRM do Primetime oferece suporte às seguintes opções para conversão de metadados:

* Offline (recomendado)

   Gere os metadados de DRM do Primetime em um processo offline e armazene os metadados até que sejam solicitados por um cliente. Se os metadados forem gerados offline, o servidor de licenças não precisará acessar os CEKs 1.x ou a credencial do empacotador. A conversão offline oferece melhor desempenho, pois o License Server não precisa gerar os metadados em tempo real.
* Sob demanda

   Os metadados DRM do Primetime são gerados quando os metadados são solicitados por um cliente. Quando um cliente DRM do Primetime baixa o conteúdo da versão 1.x, o cliente envia os metadados DRM para o SDK de DRM do Primetime. O SDK converte os metadados de DRM no formato atual, criptografa e incorpora a chave de criptografia de conteúdo (CEK) nos metadados e envia o conteúdo para o cliente de DRM do Primetime.

   >[!NOTE]
   >
   >Os metadados DRM 1.x do Primetime não incluem o CEK.

   Para converter os metadados, o DRM do Primetime requer acesso às chaves de criptografia de conteúdo do Primetime DRM 1.x. Ao migrar do Flash Media Rights Management Server 1.x, você pode continuar a armazenar as chaves de criptografia de conteúdo no banco de dados do LiveCycle ES ou implementar uma solução personalizada para armazenar com segurança as chaves de criptografia de conteúdo em outro local. Se decidir armazenar as chaves de criptografia de conteúdo no banco de dados ES do LiveCycle, siga as recomendações descritas em *Protegendo o acesso a conteúdo confidencial no banco de dados* em **Otimização e Segurança para LiveCycle® ES2**.

Para obter mais informações sobre como garantir a compatibilidade com o conteúdo empacotado usando o Flash Media Rights Management Server 1.x, consulte as APIs de DRM do Adobe Primetime em [Referências da API do Adobe Primetime](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).
