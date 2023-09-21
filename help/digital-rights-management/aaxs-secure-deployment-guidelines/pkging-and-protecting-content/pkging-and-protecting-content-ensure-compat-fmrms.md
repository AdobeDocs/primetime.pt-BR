---
title: Garanta a compatibilidade com o Media Rights Management Server 1.x do Flash
description: Garanta a compatibilidade com o Media Rights Management Server 1.x do Flash
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Garanta a compatibilidade com o Media Rights Management Server 1.x do Flash{#ensure-compatibility-with-flash-media-rights-management-server-x}

O Flash Media Rights Management Server 1.x e o Adobe Access usam metadados diferentes para empacotar conteúdo e solicitar licenças. Para que o Adobe Access use o conteúdo do FMRMS versão 1.x, os metadados devem ser convertidos.

O SDK de acesso ao Adobe suporta duas opções para converter metadados:

* Offline (recomendado)

  Gere os metadados de Acesso ao Adobe em um processo offline e armazene-os para uso quando um cliente os solicitar. O Adobe recomenda essa opção. Se os metadados forem gerados offline, o servidor de licença não precisará acessar os CEKs 1.x ou a credencial do empacotador. Além disso, a conversão offline oferece melhor desempenho, pois o License Server não precisa gerar os metadados em tempo real.

* Sob demanda

  Gere os metadados de acesso Adobe sob demanda quando um cliente os solicitar. Quando um cliente de acesso ao Adobe baixa o conteúdo da versão 1.x, ele envia os metadados de DRM (também conhecidos como cabeçalho de DRM) para o SDK de acesso ao Adobe. O SDK converte os metadados de DRM para o formato atual. O SDK criptografa e incorpora a chave de criptografia de conteúdo (CEK) nos metadados e envia o conteúdo de volta para o cliente de acesso ao Adobe. (Os metadados do Adobe Access 1.x não contêm o CEK.)

  Para converter os metadados, o Adobe Access exige acesso às chaves de criptografia de conteúdo do Adobe Access 1.x. Ao migrar do Flash Media Rights Management Server 1.x, você pode continuar a armazenar as chaves de criptografia de conteúdo no banco de dados do LiveCycle ES ou pode implementar uma solução personalizada para armazenar com segurança as chaves de criptografia de conteúdo em outro lugar. Se você optar por continuar armazenando as chaves de criptografia de conteúdo no banco de dados LiveCycle ES, siga as recomendações descritas em &quot;Protegendo o acesso a conteúdo confidencial no banco de dados&quot; em *Fortalecimento e segurança para LiveCycle ES*.

Para obter mais informações sobre como garantir a compatibilidade com conteúdo empacotado usando o Flash Media Rights Management Server 1.x, consulte a *Referência da API de acesso do Adobe*.
