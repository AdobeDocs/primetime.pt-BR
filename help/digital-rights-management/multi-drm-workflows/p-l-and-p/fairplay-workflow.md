---
description: Os fluxos de trabalho do DRM envolvem empacotar seu conteúdo, fornecer licenciamento para o conteúdo e reproduzir o conteúdo protegido de seu próprio aplicativo de vídeo. O fluxo de trabalho é geralmente semelhante para cada solução DRM, mas com algumas diferenças estão nos detalhes.
seo-description: Os fluxos de trabalho do DRM envolvem empacotar seu conteúdo, fornecer licenciamento para o conteúdo e reproduzir o conteúdo protegido de seu próprio aplicativo de vídeo. O fluxo de trabalho é geralmente semelhante para cada solução DRM, mas com algumas diferenças estão nos detalhes.
seo-title: Fluxo de trabalho multi-DRM para FairPlay
title: Fluxo de trabalho multi-DRM para FairPlay
uuid: cd940a70-400c-435e-8322-55bd624164e1
translation-type: tm+mt
source-git-commit: 29149594c4b41956a091ef27093304e74ff15f2f

---


# Fluxo de trabalho multi-DRM para FairPlay {#multi-drm-workflow-for-fairplay}

Os fluxos de trabalho do DRM envolvem empacotar seu conteúdo, fornecer licenciamento para o conteúdo e reproduzir o conteúdo protegido de seu próprio aplicativo de vídeo. O fluxo de trabalho é geralmente semelhante para cada solução DRM, mas com algumas diferenças estão nos detalhes.

Esse fluxo de trabalho de vários DRM o orienta pela configuração, empacotamento, licenciamento e reprodução de conteúdo HLS protegido com o Apple FairPlay. Este fluxo de trabalho também inclui instruções opcionais para implementar a reprodução offline e a rotação de licenças.

## Habilitar o serviço ExpressPlay para o FairPlay {#enable-expressplay-service-for-fairplay}

A solução FairPlay DRM da Apple requer alguma configuração quando você a usa com os serviços ExpressPlay DRM. Isso envolve obter credenciais da Apple e carregá-las no ExpressPlay.

Siga estas etapas para habilitar o serviço ExpressPlay para proteção de conteúdo do FairPlay.

1. Obtenha credenciais da Apple.

   Essas credenciais são provisionadas exclusivamente para cada provedor de serviços. Você deve solicitar preenchendo o seguinte formulário: [https://developer.apple.com/contact/fps/](https://developer.apple.com/contact/fps/).

   >[!NOTE]
   >
   >Selecione **[!UICONTROL Content Provider]** para Função Principal.

   Assim que sua solicitação for aprovada, a Apple lhe enviará um Pacote *de implantação de streaming do* FairPlay.
1. Gerar uma solicitação de assinatura de certificado.

   Você pode usar [!DNL openssl] para gerar seu par de chave pública/privada e sua solicitação assinada por certificado (CSR).

   1. Gere seu par de chaves.

      ```
      openssl genrsa -aes256 -out privatekey.pem 1024 
      ```

   1. Gere seu CSR.

      ```
      openssl req -new -sha1 -key privatekey.pem -out certreq.csr  
        -subj "/CN=SubjectName /OU=OrganizationalUnit /O=Organization /C=US"
      ```

      >[!NOTE]
      >
      >As instruções para esta etapa estão localizadas no Pacote *de implantação do* FairPlay Streaming, mas estão incluídas aqui para sua conveniência. Se tiver problemas com essa parte do processo, verifique as instruções em *FairPlayCertificateCreation.pdf* (no pacote de implantação).

1. Carregue seu CSR pelo portal de desenvolvedores da Apple.
   1. O Agente de Equipe da sua equipe de desenvolvimento deve se conectar [!DNL developer.apple.com/account].
   1. Clique em **[!UICONTROL Certificates, Identifiers & Profiles]**, selecione o **[!UICONTROL iOS, tvOS, watchOS]** menu suspenso no canto superior esquerdo da página e, em seguida, clique em **[!UICONTROL Certificates->Production]** à esquerda da página.
   1. Clique no **[!UICONTROL +]** botão no canto superior direito da página para solicitar um novo certificado. Selecione a **[!UICONTROL FairPlay Streaming Certificate]** opção em **[!UICONTROL Production]**.

      A caixa de diálogo *Adicionar certificado* do iOS é aberta.
   1. Em *Adicionar certificado* iOS, carregue o arquivo CSR gerado na Etapa 2.b. e clique em **[!UICONTROL Generate]**.

      Sua Chave Secreta do Aplicativo (ASK) é exibida na mesma caixa de diálogo.
   1. Anote seu ASK e armazene-o em um local seguro.
   1. Chave em seu ASK para concluir a geração do certificado e clique em **[!UICONTROL Continue]**.
   1. Depois de verificar se salvou o ASK, clique **[!UICONTROL Generate]** para continuar.

      >[!NOTE] {important=&quot;high&quot;}
      >
      >É importante que você salve uma cópia do seu ASK e armazene-a com segurança. *Se o seu ASK estiver comprometido, você não poderá mais proteger seu conteúdo com o FairPlay Streaming.* Somente um (1) ASK é alocado para sua equipe. O valor não será fornecido novamente e você não poderá recuperá-lo posteriormente.

   1. Baixe seu certificado FPS.

      Certifique-se de salvar uma cópia de backup de sua chave privada (da Etapa 2.a.) e sua chave pública (o Certificado FPS que você baixou nessa etapa) em um local seguro.
1. Configure sua conta ExpressPlay com suas credenciais do FairPlay.
   1. Digamos o nome do certificado que você baixou na Etapa 3.h. é [!DNL fairplay.cer].
   1. Abra o [!DNL fairplay.cer] arquivo com o utilitário Apple Keychain Access.
   1. Filtre seus muitos certificados digitando &quot; `fairplay`&quot; no campo de pesquisa localizado no canto superior direito.
   1. Identifique o certificado do FairPlay de sua empresa.

      O nome da sua empresa deve estar associado ao certificado emitido pela Apple.
   1. Expanda o certificado selecionando a seta de expansão e clique com o botão direito do mouse na sua chave privada.
   1. Selecione **[!UICONTROL Export "Your Company Name"]** e salve o [!DNL .p12] arquivo.

      Você será solicitado a atribuir uma senha para proteger esse arquivo. Anote esta senha, pois será necessário enviá-la com seu pacote de credenciais.
   1. Faça logon em sua conta em [www.expressplay.com](https://www.expressplay.com).
   1. Clique **[!UICONTROL DRM SERVICES]** no canto superior esquerdo e selecione a **[!UICONTROL FairPlay]** guia.
   1. Carregue suas credenciais do FairPlay em sua conta do ExpressPlay.

      1. Crie um arquivo de texto que contenha o valor de seu ASK (deve ter 32 caracteres, por exemplo: `1234567890abcdef1234567890abcdef`) e selecione este arquivo para upload.
      1. Selecione o arquivo PKCS12 na Etapa 4.f. para upload.
      1. Digite a senha do arquivo PKCS12 na Etapa 4.f.
      1. Clique no botão Carregar.

Agora você pode criar aplicativos iOS ou páginas HTML5 com proteção de conteúdo do FairPlay junto com seu [!DNL fairplay.cer] certificado usando o serviço ExpressPlay para FairPlay.

<!--<a id="fig_sjr_2pn_sv"></a>-->

![](assets/multi_drm_expressplay_drm_services_web.png)

### Compacte seu conteúdo para o FairPlay {#package-your-content-for-fairplay}

Para empacotar seu conteúdo, você pode usar o Adobe Offline Packager ou outras ferramentas, como o empacotador Bento4 do ExpressPlay.

Os Packagers preparam o vídeo para reprodução (por exemplo, fragmentando o arquivo original e colocando-o em um manifesto) e protegem o vídeo com a solução DRM escolhida (neste caso, FairPlay):

* [Adobe Offline Packager for FairPlay DRM](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=21)
* [Packagers ExpressPlay - Bento4 para HLS](https://www.bento4.com/developers/hls/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_hls_web.png)

1. Empacote seu conteúdo.

   Este é um exemplo de empacotamento usando o Adobe Offline Packager. O Packager usa um arquivo de configuração (por exemplo, [!DNL fairplay.xml]), que se parece com o seguinte:

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
   * `out_type` - Esta entrada descreve o tipo de saída empacotada, neste caso HLS para FairPlay.
   * `out_path` - O local na máquina local para onde deseja que a saída seja enviada.
   * `drm_sys` - A solução DRM para a qual você está empacotando. Isto é `FAIRPLAY` neste caso.
   * `frag_dur` - Duração do fragmento em segundos.
   * `target_dur` - A duração alvo para a saída HLS.
   * `key_file_path` - Este é o local do arquivo de licença no seu computador de empacotamento que serve como sua Chave de criptografia de conteúdo (CEK). É uma string hexadecimal de 16 bytes codificada em Base 64.
   * `iv_file_path` - Esta é a localização do arquivo IV na sua máquina de embalagem.
   * `key_url` - O parâmetro URI da `EXT-X-KEY` tag do [!DNL .m3u8] arquivo.
   * `content_id` - Valor padrão.
   Conforme declarado na documentação [do](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=7)Packager, &quot;Como prática recomendada, crie um arquivo de configuração que contenha as opções comuns que você deseja usar para gerar as saídas. Em seguida, crie a saída fornecendo opções específicas como um argumento de linha de comando.&quot;

   ```
   java -jar OfflinePackager.jar -in_path sample.mp4 -out_type hls 
   -out_path out_file_path -drm -drm_sys FAIRPLAY -key_file_path "creds/fairplay.bin" 
   -key_url "user_provided_value"
   ```

   O arquivo M3U8 gerado tem um `EXT-X-KEY` atributo que aparece da seguinte forma:

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="user_provided_value",​
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1" 
   ```

### Definindo políticas para o FairPlay {#setting-policies-for-fairplay}

Você pode definir políticas para conteúdo protegido pelo FairPlay usando um servidor de direito. Você pode configurar seu próprio servidor ou usar um servidor de direito de amostra fornecido pela Adobe.

A Adobe fornece um exemplo do ExpressPlay Entitlement Server (SEES) que mostra como fazer um direito baseado *em* tempo e de vinculação *de* dispositivo. Este exemplo de servidor de direito foi criado sobre os serviços do ExpressPlay.

[Servidor de referência: Servidor de direito ExpressPlay de amostra (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

* [Serviço de referência: Direito baseado em tempo](../../multi-drm-workflows/feature-topics/sees-reference-server-time-entitlement.md)
* [Serviço de referência: Direito de vinculação de dispositivo](../../multi-drm-workflows/feature-topics/sees-reference-server-binding-entitlement.md)

## Licenciamento e reprodução para o FairPlay {#licensing-and-playback-for-fairplay}

O licenciamento e a reprodução de conteúdo protegido pelo FairPlay exigem a troca de esquemas de URL, entre o esquema usado no arquivo de manifesto do vídeo (skd:) e o usado nas solicitações de token do ExpressPlay (https:).

As instruções para implementar o licenciamento e a reprodução de um cliente TVSDK do iOS estão aqui: [Ative o Apple FairPlay em aplicativos](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)TVSDK. Opcionalmente, também é possível implementar a reprodução offline e a rotação de licenças para o FairPlay.

## HLS offline com FairPlay {#section_047A05D1E3B64883858BC601CFC8F759}

Você pode desejar que os usuários possam reproduzir conteúdo protegido pelo FairPlay quando seu licenciamento não for recuperável porque o player está isolado da Web (como em um avião).

Antes de começar esta tarefa, baixe e leia o documento da Apple **&quot;Reprodução offline com o FairPlay Streaming e HTTP Live Streaming&quot;**. Leia o guia para saber como baixar segmentos de TS (Transport Stream) e salvá-los no computador local.

Implemente o play offline para o FairPlay com este fluxo de trabalho:

1. Baixe o segmento HLS TS.
1. Solicite licença de aluguel persistente do servidor FairPlay (consulte **&quot;Política de aluguel persistente do FairPlay&quot;**).
1. Salve o `persistentContentKey`.
1. Reproduzir o conteúdo do FairPlay offline.

>[!NOTE]
>
>O FairPlay Streaming no cliente não inicia a descriptografia se a chave de conteúdo persistente tiver expirado. No entanto, ela continuará a experiência do usuário se a chave de conteúdo expirar durante a reprodução.
>
>Consulte [Trabalhar com o documento HTTP Live Streaming](https://developer.apple.com/library/content/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/HTTPLiveStreaming/HTTPLiveStreaming.html#//apple_ref/doc/uid/TP40016757-CH11-SW3) para obter mais detalhes.

### Rotação de licença do FairPlay {#section_D32AA08C61474B4F876AC2A5F18CB879}

A rotação de licenças é um esquema para impedir o hacking de licenças de conteúdo que é reproduzido por muito tempo.

Em um manifesto M3U8, cada tag-chave será aplicada aos seguintes segmentos TS até a próxima tag-chave ou até o final do arquivo.

Para adicionar a rotação da licença, faça o seguinte:

* Insira uma nova tag de chave do FairPlay durante o tempo de rotação da licença.

   Qualquer número de tags-chave pode ser adicionado.

   Para conteúdo linear, mantenha a tag-chave mais recente na janela M3U8. O iOS solicitará o próximo M3U8 quando houver cerca de dois segmentos TS restantes para serem reproduzidos (cerca de 20 segundos). Se o novo M3U8 contiver novas tags-chave, todas as solicitações-chave ocorrerão imediatamente. As chaves existentes anteriores não serão solicitadas novamente. O iOS aguardará a conclusão de todas as solicitações principais para que a reprodução seja iniciada.

   Para conteúdo VOD com rotação de licença, todas as solicitações principais ocorrerão no início da reprodução.

   Veja a seguir uma amostra M3U8 com rotação de chaves:

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
