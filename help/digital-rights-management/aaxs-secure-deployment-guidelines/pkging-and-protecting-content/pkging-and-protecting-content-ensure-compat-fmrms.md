---
seo-title: Verifique a compatibilidade com o Flash Media Rights Management Server 1.x
title: Verifique a compatibilidade com o Flash Media Rights Management Server 1.x
uuid: 0160ca02-ebe6-4090-bf32-1d1a46088844
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Verifique a compatibilidade com o Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}

O Flash Media Rights Management Server 1.x e o Adobe Access usam metadados diferentes para empacotar conteúdo e solicitar licenças. Para que o Acesso ao Adobe use o conteúdo FMRMS versão 1.x, os metadados devem ser convertidos.

O SDK de acesso ao Adobe oferece suporte a duas opções para conversão de metadados:

* Offline (recomendado)

   Gere os metadados de Adobe Access em um processo offline e armazene-os para uso quando um cliente os solicitar. O Adobe recomenda essa opção. Se os metadados forem gerados offline, o servidor de licenças não precisará de acesso aos CEKs 1.x ou à credencial do empacotador. Além disso, a conversão offline do oferta melhora o desempenho, pois o License Server não precisa gerar os metadados em tempo real.

* Sob demanda

   Gere os metadados de Adobe Access sob demanda quando um cliente os solicitar. Quando um cliente do Adobe Access baixa o conteúdo da versão 1.x, ele envia os metadados DRM (também conhecidos como cabeçalho DRM) para o SDK de acesso ao Adobe. O SDK converte os metadados do DRM no formato atual. O SDK criptografa e incorpora a chave de criptografia de conteúdo (CEK) nos metadados e envia o conteúdo de volta ao cliente do Adobe Access. (Os metadados do Adobe Access 1.x não contêm o CEK.)

   Para converter os metadados, o Adobe Access requer acesso às chaves de criptografia de conteúdo do Adobe Access 1.x. Ao migrar do Flash Media Rights Management Server 1.x, você pode continuar a armazenar as chaves de criptografia de conteúdo no banco de dados ES do LiveCycle ou pode implementar uma solução personalizada para armazenar com segurança as chaves de criptografia de conteúdo em outro lugar. Se você optar por continuar armazenando as chaves de criptografia de conteúdo no banco de dados ES do LiveCycle, siga as recomendações descritas em &quot;Protegendo o acesso a conteúdo sigiloso no banco de dados&quot; em *Proteção e segurança para o LiveCycle ES*.

Para obter mais informações sobre como garantir a compatibilidade com o conteúdo empacotado usando o Flash Media Rights Management Server 1.x, consulte *Adobe Access API Reference*.
