---
description: Você pode usar o empacotador Bento4 do ExpressPlay para preparar conteúdo para qualquer solução de DRM compatível com o Primetime Cloud DRM, fornecido pela ExpressPlay.
seo-description: Você pode usar o empacotador Bento4 do ExpressPlay para preparar conteúdo para qualquer solução de DRM compatível com o Primetime Cloud DRM, fornecido pela ExpressPlay.
seo-title: ExpressPlay Packager / Cloud DRM / TVSDK
title: ExpressPlay Packager / Cloud DRM / TVSDK
uuid: 0d2f5a8d-15c4-42ba-acb8-1dc8d5bc62de
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---


# ExpressPlay Packager / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

Você pode usar o empacotador Bento4 do ExpressPlay para preparar conteúdo para qualquer solução de DRM compatível com o Primetime Cloud DRM, fornecido pela ExpressPlay.

Esta tarefa descreve como usar uma ferramenta de terceiros para preparar conteúdo protegido, neste caso *Ferramentas do ExpressPlay Bento4*, para uso com diversas soluções de DRM. Para obter informações adicionais, consulte a documentação *Bento4 tools* no site [ExpressPlay](https://www.expressplay.com/developer/).
1. Adquira uma conta ExpressPlay e obtenha as informações do Autenticador do cliente ExpressPlay.

   Consulte [start Rápido da Nuvem DRM Primetime.](../../quick-start/quick-overview.md)
1. Se você estiver criptografando conteúdo para o Primetime Access, adquira o SDK de acesso ao Adobe Primetime do Adobe, juntamente com os certificados necessários (certificados de licença, transporte e empacotamento).
1. Forneça uma CEK (Content Encryption Key) e uma CEKSID (Content Encryption Key Armazenamento ID) para uso nos sistemas DRM. (Gera-os aleatoriamente usando o OpenSSL ou similar.)

   O CEK é a chave real que você usa para criptografar seus arquivos de vídeo. Você pode armazená-lo com segurança em seu próprio servidor em seu próprio sistema de gerenciamento de chaves ou pode usar a [solução de armazenamento de chaves](https://www.expressplay.com/developer/key-storage/) do ExpressPlay.

   Um CEKSID é o identificador de um CEK específico. Você não passa (normalmente) a chave de criptografia por aí. Por exemplo, ao solicitar um token de licença, forneça o CEKSID.

1. Se você estiver criptografando conteúdo para o Access, utilize seu CEK para criar metadados do Primetime Access associados ao seu conteúdo.

1. Fragmente seu conteúdo para prepará-lo para a ferramenta *Bento4 MP4DASH*.

   Para esta etapa, você pode usar a ferramenta *MP4FRAGMENT*. Você só precisa fragmentar o conteúdo uma vez. Por exemplo:

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. Use a ferramenta *Bento4 MPDASH* para &quot;DASH-ify&quot; e criptografe seu conteúdo fragmentado.

   Use esse comando para especificar todos os sistemas DRM que serão utilizados e passe os metadados do Primetime Access gerados nas etapas anteriores. Por exemplo:

   ```
   /mp4dash -f  
   --use-segment-list  
   --use-segment-timeline  
   --encryption-key=<CEKSID>:<CEK>  
   --playready  
   --Widevine  
   --Widevine-header=provider:intertrust#content_id:2a  
   --primetime  
   --primetime-metadata=@AAXS.metadata 
    Fragmented.mp4 -o DASH_OUTPUT
   ```

1. Crie um &quot;servidor storefront&quot;.

       Este servidor precisa lidar com as seguintes operações:
   
   1. Seleção de conteúdo pelo cliente. Essa implementação precisa incluir um terminal para que os clientes solicitem um token de conteúdo para uma ID de conteúdo específica.
   1. Direito ao cliente
   1. Solicitações de token de licença (ExpressPlay) do cliente ( [solicitação de token de licença do ExpressPlay / referência de resposta](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. Crie seu cliente.

   O cliente deve incluir uma chamada para seu servidor storefront. O Adobe recomenda que o cliente chame o storefront depois que o usuário selecionar algum conteúdo e depois que o usuário for autenticado. Em seguida, passe o token retornado do ExpressPlay para o player para uso em solicitações de licença. Apresentações para implementar o componente DRM dos seus players estão aqui:

   * TVSDK do navegador para HTML5
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Com o token de licença em mãos, o cliente agora pode derivar o URL da solicitação do token e fazer a solicitação de licença para o ExpressPlay e, em seguida, reproduzir o conteúdo protegido e selecionado para o usuário.
