---
description: Você pode usar o pacote Bento4 da ExpressPlay para preparar o conteúdo para qualquer solução de DRM compatível com o Primetime Cloud DRM, fornecido pela ExpressPlay.
title: ExpressPlay Packager / Cloud DRM / TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# ExpressPlay Packager / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

Você pode usar o pacote Bento4 da ExpressPlay para preparar o conteúdo para qualquer solução de DRM compatível com o Primetime Cloud DRM, fornecido pela ExpressPlay.

Esta tarefa descreve como usar uma ferramenta de terceiros para preparar conteúdo protegido, neste caso *ExpressPlay Bento4 Tools*, para uso com uma variedade de soluções de DRM. Para obter informações adicionais, consulte a documentação das ferramentas *Bento4* no site [ExpressPlay](https://www.expressplay.com/developer/).
1. Adquira uma conta do ExpressPlay e obtenha as informações do Autenticador do cliente do ExpressPlay.

   Consulte [Início rápido da nuvem DRM do Primetime.](../../quick-start/quick-overview.md)
1. Se estiver criptografando o conteúdo do Primetime Access , adquira o SDK do Primetime Adobe Access do Adobe, juntamente com os certificados necessários (certificados de licença, transporte e empacotamento).
1. Forneça uma Chave de criptografia de conteúdo (CEK) e uma CEKSID (Content Encryption Key Storage ID) para uso nos sistemas DRM. (Você os gera aleatoriamente usando OpenSSL ou similar.)

   A CEK é a chave real que você usa para criptografar seus arquivos de vídeo. Você pode armazená-lo com segurança em seu próprio servidor no seu próprio sistema de gerenciamento de chaves ou usar a [solução de armazenamento de chaves](https://www.expressplay.com/developer/key-storage/) do ExpressPlay.

   O CEKSID é o identificador de um CEK específico. Você não passa (normalmente) a chave de criptografia. Por exemplo, ao solicitar um token de licença, forneça o CEKSID.

1. Se estiver criptografando conteúdo para o Access, utilize o CEK para criar metadados do Primetime Access associados ao conteúdo.

1. Fragmente seu conteúdo para prepará-lo para a ferramenta *Bento4 MP4DASH*.

   Para esta etapa você pode usar a ferramenta *MP4FRAGMENT*. Você só precisa fragmentar o conteúdo uma vez. Por exemplo:

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. Use a ferramenta *Bento4 MPDASH* para &quot;DASH-ify&quot; e criptografe seu conteúdo fragmentado.

   Use este comando para especificar todos os sistemas DRM que você utilizará e transmitir todos os metadados de Acesso Primetime gerados a partir das etapas anteriores. Por exemplo:

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
   
   1. Seleção de cliente do conteúdo. Essa implementação precisa incluir um terminal para que os clientes solicitem um token de conteúdo para uma ID de conteúdo específica.
   1. Direito ao cliente
   1. Solicitações de token de licença (ExpressPlay) do cliente ( [Solicitação de token de licença do ExpressPlay / referência de resposta](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. Crie seu cliente.

   O cliente deve incluir uma chamada para o servidor da loja. O Adobe recomenda que o cliente chame a loja depois que o usuário selecionar algum conteúdo e depois que o usuário for autenticado. Em seguida, passe o token retornado do ExpressPlay para o seu player para usar em solicitações de licença. As introduções para implementar o componente DRM de seus players estão aqui:

   * TVSDK do navegador para HTML5
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Com o token de licença em mãos, o cliente agora pode derivar o URL da solicitação do token e fazer a solicitação de licença para o ExpressPlay e, em seguida, reproduzir o conteúdo protegido e selecionado para o usuário.
