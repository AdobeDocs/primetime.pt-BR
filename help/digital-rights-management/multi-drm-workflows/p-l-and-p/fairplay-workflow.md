---
description: Os fluxos de trabalho de DRM envolvem empacotar seu conteúdo, fornecer licenciamento para o conteúdo e reproduzir o conteúdo protegido de seu próprio aplicativo de vídeo. O fluxo de trabalho é geralmente semelhante para cada solução de DRM, mas com algumas diferenças estão nos detalhes.
title: Fluxo de Trabalho Multi-DRM para FairPlay
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---


# Fluxo de trabalho de vários DRM para FairPlay {#multi-drm-workflow-for-fairplay}

Os fluxos de trabalho de DRM envolvem empacotar seu conteúdo, fornecer licenciamento para o conteúdo e reproduzir o conteúdo protegido de seu próprio aplicativo de vídeo. O fluxo de trabalho é geralmente semelhante para cada solução de DRM, mas com algumas diferenças estão nos detalhes.

Esse fluxo de trabalho de vários DRM o orienta pela configuração, empacotamento, licenciamento e reprodução de conteúdo HLS protegido com o Apple FairPlay. Esse workflow também inclui instruções opcionais para implementar a reprodução offline e a rotação de licenças.

## Ativar o serviço ExpressPlay para FairPlay {#enable-expressplay-service-for-fairplay}

A solução FairPlay DRM da Apple requer alguma configuração quando você a usa com os serviços ExpressPlay DRM. Isso envolve obter credenciais da Apple e carregá-las no ExpressPlay.

Siga estas etapas para habilitar o serviço ExpressPlay para proteção de conteúdo FairPlay.

1. Obtenha credenciais da Apple.

   Essas credenciais são provisionadas exclusivamente para cada provedor de serviços. Você deve solicitá-los preenchendo o seguinte formulário: [https://developer.apple.com/contact/fps/](https://developer.apple.com/contact/fps/).

   >[!NOTE]
   >
   >Selecione **[!UICONTROL Content Provider]** para Função primária.

   Depois que sua solicitação for aprovada, a Apple enviará a você um *Pacote de implantação de streaming do FairPlay*.
1. Gere uma solicitação de assinatura de certificado.

   Você pode usar [!DNL openssl] para gerar seu par de chaves públicas/privadas e sua solicitação de certificado assinado (CSR).

   1. Gere seu par de chaves.

      ```
      openssl genrsa -aes256 -out privatekey.pem 1024 
      ```

   1. Gere sua CSR.

      ```
      openssl req -new -sha1 -key privatekey.pem -out certreq.csr  
        -subj "/CN=SubjectName /OU=OrganizationalUnit /O=Organization /C=US"
      ```

      >[!NOTE]
      >
      >As instruções para esta etapa estão localizadas em seu *Pacote de implantação de streaming do FairPlay*, mas estão incluídas aqui para sua conveniência. Se tiver problemas com essa parte do processo, verifique as instruções em *FairPlayCertificateCreation.pdf* (no pacote de implantação).

1. Faça upload de seu CSR por meio do portal do desenvolvedor da Apple.
   1. O Team Agent da sua equipe de desenvolvimento deve fazer logon em [!DNL developer.apple.com/account].
   1. Clique em **[!UICONTROL Certificates, Identifiers & Profiles]**, selecione o menu suspenso **[!UICONTROL iOS, tvOS, watchOS]** no canto superior esquerdo da página e clique em **[!UICONTROL Certificates->Production]** à esquerda da página.
   1. Clique no botão **[!UICONTROL +]** no canto superior direito da página para solicitar um novo certificado. Selecione a opção **[!UICONTROL FairPlay Streaming Certificate]** em **[!UICONTROL Production]**.

      A caixa de diálogo *Adicionar certificado iOS* é aberta.
   1. No *Adicionar certificado iOS*, faça o upload do arquivo CSR gerado na Etapa 2.b. e clique em **[!UICONTROL Generate]**.

      Sua Chave Secreta do Aplicativo (ASK) é exibida na mesma caixa de diálogo.
   1. Anote seu ASK e armazene-o em um local seguro.
   1. Chave em seu ASK para concluir a geração de certificados e clique em **[!UICONTROL Continue]**.
   1. Depois de verificar que salvou o ASK, clique em **[!UICONTROL Generate]** para continuar.

      >[!NOTE]
      >
      >É importante salvar uma cópia do seu ASK e armazená-la com segurança. *Se o seu ASK estiver comprometido, você não poderá mais proteger seu conteúdo com o FairPlay Streaming.* Somente um (1) ASK é alocado para sua equipe. O valor não será fornecido novamente e você não poderá recuperá-lo posteriormente.

   1. Baixe seu certificado FPS.

      Certifique-se de salvar uma cópia de backup de sua chave privada (da Etapa 2.a.) e sua chave pública (o Certificado FPS que você baixou nesta etapa) em um local seguro.
1. Configure sua conta do ExpressPlay com suas credenciais do FairPlay.
   1. Digamos o nome do certificado que você baixou na Etapa 3.h. é [!DNL fairplay.cer].
   1. Abra o arquivo [!DNL fairplay.cer] com o utilitário Acesso ao chaveiro da Apple.
   1. Filtre seus muitos certificados inserindo &quot; `fairplay`&quot; no campo de pesquisa localizado no canto superior direito.
   1. Identifique o certificado FairPlay da sua empresa.

      O nome da sua empresa deve estar associado ao certificado emitido pela Apple.
   1. Expanda o certificado selecionando a seta de expansão e clique com o botão direito do mouse na chave privada.
   1. Selecione **[!UICONTROL Export "Your Company Name"]** e salve o arquivo [!DNL .p12].

      Você será solicitado a atribuir uma senha para proteger esse arquivo. Anote essa senha, pois será necessário enviá-la com seu pacote de credenciais.
   1. Faça logon em sua conta em [www.expressplay.com](https://www.expressplay.com).
   1. Clique em **[!UICONTROL DRM SERVICES]** no canto superior esquerdo e selecione a guia **[!UICONTROL FairPlay]**.
   1. Faça upload de suas credenciais do FairPlay para sua conta do ExpressPlay.

      1. Crie um arquivo de texto que contenha o valor de seu ASK (deve ter 32 caracteres, por exemplo: `1234567890abcdef1234567890abcdef`) e selecione este arquivo para upload.
      1. Selecione o arquivo PKCS12 na Etapa 4.f. para upload.
      1. Insira a senha do arquivo PKCS12 da Etapa 4.f.
      1. Clique no botão Upload .

Agora você pode criar aplicativos iOS ou páginas HTML5 com proteção de conteúdo FairPlay junto com seu certificado [!DNL fairplay.cer] usando o serviço ExpressPlay para FairPlay.

<!--<a id="fig_sjr_2pn_sv"></a>-->

![](assets/multi_drm_expressplay_drm_services_web.png)

### Compacte seu conteúdo para o FairPlay {#package-your-content-for-fairplay}

Para empacotar conteúdo, você pode usar o Adobe Offline Packager ou outras ferramentas, como o Bento4 Packager do ExpressPlay.

Os empacotadores preparam o vídeo para reprodução (por exemplo, fragmentando o arquivo original e colocando-o em um manifesto) e protegem o vídeo com a solução de DRM escolhida (neste caso, FairPlay):

* [Adobe Offline Packager for FairPlay DRM](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=21)
* [Pacotes do ExpressPlay - Bento4 para HLS](https://www.bento4.com/developers/hls/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_hls_web.png)

1. Compacte seu conteúdo.

   Este é um exemplo de empacotamento usando o Adobe Offline Packager. O Packager usa um arquivo de configuração (por exemplo, [!DNL fairplay.xml]), que tem a seguinte aparência:

   ```
   <config>
   <in_path>mp4_file_path</in_path>
   <out_type>hls</out_type>
   <out_path>out_file_path</out_path>
   <drm/>
   <drm_sys>FAIRPLAY</drm_sys>
   <frag_dur>4</frag_dur>
   <target_dur>6</target_dur>
   <key_file_path>creds/fairplay.bin</key_file_path>
   <iv_file_path>creds/iv.bin</iv_file_path>
   <key_url>user_provided_value</key_url>
   <content_id>_default_</content_id>
   </config>
   ```

   * `in_path` - Essa entrada aponta para o local do vídeo de origem em sua máquina de embalagem local.
   * `out_type` - Esta entrada descreve o tipo de saída embalada, neste caso HLS para FairPlay.
   * `out_path` - O local na máquina local onde você deseja que a saída vá.
   * `drm_sys` - A solução de DRM para a qual você está fazendo o empacotamento. Esse é `FAIRPLAY` neste caso.
   * `frag_dur` - Duração do fragmento em segundos.
   * `target_dur` - A duração do target para a saída HLS.
   * `key_file_path` - Esse é o local do arquivo de licença em sua máquina de embalagem que serve como sua Chave de criptografia de conteúdo (CEK). É uma string hexadecimal codificada em Base 64 de 16 bytes.
   * `iv_file_path` - Esse é o local do arquivo IV em sua máquina de embalagem.
   * `key_url` - O parâmetro URI da  `EXT-X-KEY` tag do  [!DNL .m3u8] arquivo.
   * `content_id` - Valor padrão.

   Conforme declarado na [Documentação do Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=7), &quot;Como prática recomendada, crie um arquivo de configuração que contenha as opções comuns que você deseja usar para gerar as saídas. Em seguida, crie a saída fornecendo opções específicas como um argumento de linha de comando.&quot;

   ```
   java -jar OfflinePackager.jar -in_path sample.mp4 -out_type hls 
   -out_path out_file_path -drm -drm_sys FAIRPLAY -key_file_path "creds/fairplay.bin" 
   -key_url "user_provided_value"
   ```

   O arquivo M3U8 gerado tem um atributo `EXT-X-KEY` que aparece da seguinte maneira:

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="user_provided_value",​
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1" 
   ```

### Definindo políticas para o FairPlay {#setting-policies-for-fairplay}

Você pode definir políticas para conteúdo protegido pelo FairPlay usando um servidor de direito. Você pode configurar o seu próprio ou usar um servidor de direito de amostra fornecido pelo Adobe.

O Adobe fornece uma amostra do Servidor de Direitos do ExpressPlay (SEES) que mostra como fazer *direito baseado em tempo* e *vínculo de dispositivo*. Este exemplo de servidor de direito é criado sobre os serviços do ExpressPlay.

[Servidor de referência: Exemplo de SEES (ExpressPlay Entitlement Server)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

* [Serviço de referência: Direito baseado no tempo](../../multi-drm-workflows/feature-topics/sees-reference-server-time-entitlement.md)
* [Serviço de referência: Direito de vinculação de dispositivo](../../multi-drm-workflows/feature-topics/sees-reference-server-binding-entitlement.md)

## Licenciamento e reprodução para FairPlay {#licensing-and-playback-for-fairplay}

O licenciamento e a reprodução de conteúdo protegido pelo FairPlay exigem a troca de esquemas de URL, entre o esquema usado no arquivo de manifesto do vídeo (skd:) e o usado nas solicitações de token do ExpressPlay (https:).

Instruções para implementar o licenciamento e a reprodução em um cliente TVSDK do iOS estão aqui: [Habilite o Apple FairPlay em aplicativos TVSDK](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md). Opcionalmente, também é possível implementar a reprodução offline e a rotação de licença do FairPlay.

## HLS Offline com FairPlay {#section_047A05D1E3B64883858BC601CFC8F759}

Você pode querer tornar possível que os usuários reproduzam conteúdo protegido pelo FairPlay quando seu licenciamento não for recuperável porque o player está isolado da Web (como em um avião).

Antes de iniciar esta tarefa, baixe e leia o documento da Apple **&quot;Reprodução offline com o FairPlay Streaming e HTTP Live Streaming&quot;**. Leia o guia para saber como baixar segmentos de TS (Transport Stream) e salvá-los no computador local.

Implemente o play offline para o FairPlay com este workflow:

1. Baixe o segmento HLS TS.
1. Solicite licença de aluguel persistente do servidor FairPlay (consulte **&quot;Política de aluguel persistente do FairPlay&quot;**).
1. Salve o `persistentContentKey`.
1. Reproduzir o conteúdo do FairPlay offline.

>[!NOTE]
>
>O FairPlay Streaming no cliente não inicia a descriptografia se a chave de conteúdo persistente tiver expirado. No entanto, ela continuará a experiência do usuário se a chave de conteúdo expirar durante a reprodução.
>
>Consulte o documento [Trabalhar com HTTP Live Streaming](https://developer.apple.com/library/content/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/HTTPLiveStreaming/HTTPLiveStreaming.html#//apple_ref/doc/uid/TP40016757-CH11-SW3) para obter mais detalhes.

### Rotação de licença do FairPlay {#section_D32AA08C61474B4F876AC2A5F18CB879}

O Rotação de licença é um esquema para impedir o hacking de licenças de conteúdo que é reproduzido por um longo período.

Em um manifesto M3U8, cada tag-chave será aplicada aos segmentos TS a seguir até a próxima tag-chave ou até o fim do arquivo.

Para adicionar a rotação da licença, faça o seguinte:

* Insira uma nova tag de chave do FairPlay durante o tempo de rotação da licença.

   É possível adicionar qualquer número de tags principais.

   Para conteúdos lineares, mantenha a tag principal mais recente na janela M3U8. O iOS solicitará o próximo M3U8 quando restarem cerca de dois segmentos TS para serem reproduzidos (cerca de 20 segundos). Se o novo M3U8 contiver novas tags principais, todas as solicitações principais ocorrerão imediatamente. As chaves existentes anteriores não serão solicitadas novamente. O iOS aguardará a conclusão de todas as solicitações principais para que a reprodução seja iniciada.

   Para conteúdo VOD com rotação de licença, todas as solicitações principais ocorrerão no início da reprodução.

   A seguir, uma amostra de M3U8 com rotação de chave:

   ```
   #EXTM3U
   #EXT-X-TARGETDURATION:10
   #EXT-X-VERSION:5
   #EXT-X-MEDIA-SEQUENCE:0
   #EXT-X-PLAYLIST-TYPE:VOD
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="skd://one?cek=1dc2cc71d913f4f74eca0c4632
   212b25&iv=e21f0f72b6363ff6143737cb1e9ca8d7",KEYFORMAT="com.apple.streaming
   keydelivery",KEYFORMATVERSIONS="1"
   #EXTINF:10,
   fileSequence0.ts
   #EXTINF:10,
   fileSequence1.ts
   #EXTINF:10,
   fileSequence2.ts
   #EXTINF:10,
   fileSequence3.ts
   #EXTINF:10,
   fileSequence4.ts
   #EXTINF:10,
   fileSequence5.ts
   #EXTINF:10,
   fileSequence6.ts
   #EXTINF:10,
   fileSequence7.ts
   #EXTINF:10,
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="skd://two?cek=f6efc698b96cf8f4fa46d5237d
   337c77&iv=18401077091784bcda8079acf978dc95",KEYFORMAT="com.apple.streaming
   keydelivery",KEYFORMATVERSIONS="1"
   #EXTINF:10,
   fileSequence8.ts
   #EXTINF:10,
   ```
