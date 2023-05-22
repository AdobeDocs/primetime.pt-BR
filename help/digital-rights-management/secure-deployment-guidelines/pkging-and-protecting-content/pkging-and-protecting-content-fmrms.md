---
description: O Flash Media Rights Management Server 1.x e o Adobe Primetime DRM usam diferentes metadados para empacotar conteúdo e solicitar licenças. Para que o Primetime DRM use o conteúdo do FMRMS versão 1.x, os metadados devem ser convertidos.
title: Garantia de compatibilidade com o Flash Media Rights Management Server 1.x
exl-id: 737c853f-4e27-47e6-9248-857c7800795a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Garantia de compatibilidade com o Flash Media Rights Management Server 1.x {#ensuring-compatibility-with-flash-media-rights-management-server-x}

O Flash Media Rights Management Server 1.x e o Adobe Primetime DRM usam diferentes metadados para empacotar conteúdo e solicitar licenças. Para que o Primetime DRM use o conteúdo do FMRMS versão 1.x, os metadados devem ser convertidos.

O SDK do DRM do Primetime é compatível com as seguintes opções de conversão de metadados:

* Offline (recomendado)

   Gere os metadados de DRM do Primetime em um processo offline e armazene-os até que sejam solicitados por um cliente. Se os metadados forem gerados offline, o servidor de licença não precisará acessar os CEKs 1.x ou a credencial do empacotador. A conversão offline oferece melhor desempenho porque o License Server não precisa gerar os metadados em tempo real.
* Sob demanda

   Os metadados de DRM do Primetime são gerados quando os metadados são solicitados por um cliente. Quando um cliente DRM do Primetime baixa o conteúdo da versão 1.x, o cliente envia os metadados DRM para o SDK DRM do Primetime. O SDK converte os metadados de DRM no formato atual, criptografa e incorpora a chave de criptografia de conteúdo (CEK) nos metadados e envia o conteúdo de volta para o cliente DRM do Primetime.

   >[!NOTE]
   >
   >Os metadados do Primetime DRM 1.x não incluem o CEK.

   Para converter os metadados, o DRM do Primetime requer acesso às chaves de criptografia de conteúdo do DRM 1.x do Primetime. Ao migrar do Flash Media Rights Management Server 1.x, você pode continuar a armazenar as chaves de criptografia de conteúdo no banco de dados do LiveCycle ES ou implementar uma solução personalizada para armazenar com segurança as chaves de criptografia de conteúdo em outro local. Se decidir armazenar as chaves de criptografia de conteúdo no banco de dados LiveCycle ES, siga as recomendações descritas em *Proteção do acesso a conteúdo confidencial no banco de dados* in **Fortalecimento e segurança para LiveCycle®2**.

Para obter mais informações sobre como garantir a compatibilidade com o conteúdo empacotado usando o Flash Media Rights Management Server 1.x, consulte as APIs do Adobe Primetime DRM em [Referências da API do Adobe Primetime](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).
