---
description: Você pode usar o empacotador Bento4 da ExpressPlay para preparar conteúdo para qualquer uma das soluções DRM suportadas pelo Primetime Cloud DRM, habilitado pela ExpressPlay.
title: ExpressPlay Packager / Cloud DRM / TVSDK
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# ExpressPlay Packager / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

Você pode usar o empacotador Bento4 da ExpressPlay para preparar conteúdo para qualquer uma das soluções DRM suportadas pelo Primetime Cloud DRM, habilitado pela ExpressPlay.

Esta tarefa descreve como usar uma ferramenta de terceiros para preparar conteúdo protegido, neste caso *Ferramentas ExpressPlay Bento4*, para uso com várias soluções de DRM. Para obter informações adicionais, consulte a seção *Ferramentas Bento4* documentação sobre o [ExpressPlay](https://www.expressplay.com/developer/) site.
1. Adquira uma conta ExpressPlay e obtenha as informações do Autenticador do cliente ExpressPlay.

   Consulte [Início rápido da nuvem DRM do Primetime.](../../quick-start/quick-overview.md)
1. Se você estiver criptografando o conteúdo para Acesso ao Primetime, adquira o SDK de Acesso ao Adobe do Primetime do Adobe, juntamente com os certificados necessários (certificados de Licença, Transporte e Empacotamento).
1. Forneça uma Chave de criptografia de conteúdo (CEK) e uma ID de armazenamento de chave de criptografia de conteúdo (CEKSID) para uso nos sistemas DRM. (Você os gera aleatoriamente usando o OpenSSL ou similar.)

   O CEK é a chave real que você usa para criptografar os arquivos de vídeo. Você pode armazená-lo com segurança em seu próprio servidor em seu próprio sistema de gerenciamento de chaves ou pode usar o [principal solução de armazenamento](https://www.expressplay.com/developer/key-storage/).

   Um CEKSID é o identificador de um CEK específico. Você (geralmente) não passa a chave de criptografia. Por exemplo, ao solicitar um token de licença, você fornece o CEKSID.

1. Se você estiver criptografando o conteúdo para acesso, utilize seu CEK para criar metadados de acesso do Primetime associados ao seu conteúdo.

1. Fragmente seu conteúdo para prepará-lo para a *Bento4 MP4DASH* ferramenta.

   Para esta etapa, você pode usar o *MP4FRAGMENT* ferramenta. Você só precisa fragmentar o conteúdo uma vez. Por exemplo:

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. Use o *Bento4 MPDASH* para &quot;DASH-ify&quot; e criptografar o conteúdo fragmentado.

   Use este comando para especificar todos os sistemas DRM que você utilizará e transmitir quaisquer metadados de acesso do Primetime gerados pelas etapas anteriores. Por exemplo:

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

1. Crie um &quot;servidor de vitrine&quot;.

       Este servidor precisa lidar com as seguintes operações:
   
   1. Seleção de conteúdo pelo cliente. Essa implementação precisa incluir um terminal para que os clientes solicitem um token de conteúdo para uma ID de conteúdo específica.
   1. Direitos do cliente
   1. Solicitações de token de licença (ExpressPlay) do cliente ( [Referência de resposta/solicitação de token de licença do ExpressPlay](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. Crie seu cliente.

   O cliente deve incluir uma chamada para o servidor da loja. O Adobe recomenda que o cliente chame a loja depois que o usuário selecionar algum conteúdo e depois que o usuário for autenticado. Em seguida, passe o token retornado do ExpressPlay para o player para usar em solicitações de licença. As introduções para implementar o componente de DRM dos seus players estão aqui:

   * TVSDK do navegador para HTML5
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Com o token de licença em mãos, o cliente agora pode derivar o URL de solicitação do token e fazer a solicitação de licença para o ExpressPlay e, em seguida, reproduzir o conteúdo protegido selecionado para o usuário.
