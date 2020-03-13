---
seo-title: Garantir a compatibilidade com o Flash Media Rights Management Server 1.x
title: Garantir a compatibilidade com o Flash Media Rights Management Server 1.x
uuid: 0160ca02-ebe6-4090-bf32-1d1a46088844
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Garantir a compatibilidade com o Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}

O Flash Media Rights Management Server 1.x e o Adobe Access usam metadados diferentes para empacotar conteúdo e solicitar licenças. Para que o Adobe Access use o conteúdo FMRMS versão 1.x, os metadados devem ser convertidos.

O SDK do Adobe Access oferece suporte a duas opções para conversão de metadados:

* Offline (recomendado)

   Gere os metadados do Adobe Access em um processo offline e armazene-os para uso quando um cliente os solicitar. A Adobe recomenda essa opção. Se os metadados forem gerados offline, o servidor de licenças não precisará de acesso aos CEKs 1.x ou à credencial do empacotador. Além disso, a conversão offline oferece melhor desempenho, pois o License Server não precisa gerar os metadados em tempo real.

* Sob demanda

   Gere os metadados do Adobe Access sob demanda quando um cliente os solicitar. Quando um cliente do Adobe Access baixa o conteúdo da versão 1.x, ele envia os metadados DRM (também conhecidos como cabeçalho DRM) para o SDK do Adobe Access. O SDK converte os metadados do DRM no formato atual. O SDK criptografa e incorpora a chave de criptografia de conteúdo (CEK) nos metadados e envia o conteúdo de volta para o cliente do Adobe Access. (Os metadados do Adobe Access 1.x não contêm o CEK.)

   Para converter os metadados, o Adobe Access exige acesso às chaves de criptografia de conteúdo do Adobe Access 1.x. Ao migrar do Flash Media Rights Management Server 1.x, você pode continuar a armazenar as chaves de criptografia de conteúdo no banco de dados do LiveCycle ES ou pode implementar uma solução personalizada para armazenar com segurança as chaves de criptografia de conteúdo em outro lugar. Se você optar por continuar armazenando as chaves de criptografia de conteúdo no banco de dados do LiveCycle ES, siga as recomendações descritas em &quot;Protegendo o acesso a conteúdo confidencial no banco de dados&quot; em *Proteção e Segurança do LiveCycle ES*.

Para obter mais informações sobre como garantir a compatibilidade com o conteúdo empacotado usando o Flash Media Rights Management Server 1.x, consulte a Referência *da API do* Adobe Access.
