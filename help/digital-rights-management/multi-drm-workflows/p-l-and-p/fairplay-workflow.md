---
description: Os fluxos de trabalho de DRM envolvem empacotar o conteúdo, fornecer licenciamento para o conteúdo e reproduzir o conteúdo protegido de seu próprio aplicativo de vídeo. O fluxo de trabalho é geralmente semelhante para cada solução de DRM, mas com algumas diferenças está nos detalhes.
title: Fluxo de trabalho de vários DRMs para FairPlay
exl-id: a66cecda-762b-48f7-afed-6fef6303d169
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# Fluxo de trabalho de vários DRMs para FairPlay {#multi-drm-workflow-for-fairplay}

Os fluxos de trabalho de DRM envolvem empacotar o conteúdo, fornecer licenciamento para o conteúdo e reproduzir o conteúdo protegido de seu próprio aplicativo de vídeo. O fluxo de trabalho é geralmente semelhante para cada solução de DRM, mas com algumas diferenças está nos detalhes.

Esse fluxo de trabalho de Multi-DRM orienta você na configuração, empacotamento, licenciamento e reprodução de conteúdo HLS protegido com o Apple FairPlay. Esse fluxo de trabalho também inclui instruções opcionais para implementar a reprodução offline e a rotação de licenças.

## Habilitar o serviço ExpressPlay para FairPlay {#enable-expressplay-service-for-fairplay}

A solução FairPlay DRM da Apple requer configuração quando você a usa com os serviços ExpressPlay DRM. Isso envolve obter credenciais do Apple e carregá-las no ExpressPlay.

Siga estas etapas para habilitar o serviço ExpressPlay para a proteção de conteúdo FairPlay.

1. Obtenha credenciais do Apple.

   Essas credenciais são provisionadas exclusivamente para cada provedor de serviços. Você deve solicitá-los preenchendo o seguinte formulário: [https://developer.apple.com/contact/fps/](https://developer.apple.com/contact/fps/).

   >[!NOTE]
   >
   >Selecionar **[!UICONTROL Content Provider]** para a função principal.

   Depois que sua solicitação for aprovada, a Apple lhe enviará um *Pacote de Implantação de Streaming FairPlay*.
1. Gerar uma solicitação de assinatura de certificado.

   Você pode usar [!DNL openssl] para gerar seu par de chaves públicas/privadas e sua solicitação assinada por certificado (CSR).

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
      >As instruções para esta etapa estão localizadas em seu *Pacote de Implantação de Streaming FairPlay*, mas estão incluídos aqui para sua conveniência. Se tiver problemas com esta parte do processo, verifique as instruções em *FairPlayCertificateCreation.pdf* (no pacote de implantação).

1. Faça upload da CSR por meio do portal do desenvolvedor do Apple.
   1. O Agente de equipe da equipe de desenvolvimento deve fazer logon no [!DNL developer.apple.com/account].
   1. Clique em **[!UICONTROL Certificates, Identifiers & Profiles]**, em seguida, selecione a **[!UICONTROL iOS, tvOS, watchOS]** no canto superior esquerdo da página e, em seguida, clique em **[!UICONTROL Certificates->Production]** à esquerda da página.
   1. Clique em **[!UICONTROL +]** no canto superior direito da página para solicitar um novo certificado. Selecione o **[!UICONTROL FairPlay Streaming Certificate]** opção em **[!UICONTROL Production]**.

      A variável *Adicionar certificado do iOS* será aberta.
   1. No *Adicionar certificado do iOS*, carregue o arquivo CSR gerado na Etapa 2.b. e clique em **[!UICONTROL Generate]**.

      A chave secreta do aplicativo (ASK) é exibida na mesma caixa de diálogo.
   1. Anote a sua pergunta e guarde-a em um local seguro.
   1. Insira a chave na sua ASK para concluir a geração do certificado e clique em **[!UICONTROL Continue]**.
   1. Depois de verificar que salvou sua pergunta, clique em **[!UICONTROL Generate]** para continuar.

      >[!NOTE]
      >
      >É importante que você salve uma cópia de sua ASK e armazene-a com segurança. *Se sua pergunta estiver comprometida, você não poderá mais proteger seu conteúdo com o FairPlay Streaming.* Apenas uma (1) pergunta é alocada para a sua equipe. O valor não será fornecido novamente e você não poderá recuperá-lo posteriormente.

   1. Baixe o certificado FPS.

      Certifique-se de salvar uma cópia de backup da sua chave privada (da Etapa 2.a) e da sua chave pública (o Certificado FPS que você baixou nesta etapa) em um local seguro.
1. Configure sua conta do ExpressPlay com suas credenciais do FairPlay.
   1. Digamos que o nome do certificado baixado na etapa 3.h. seja [!DNL fairplay.cer].
   1. Abra o [!DNL fairplay.cer] com o utilitário Apple Keychain Access.
   1. Filtre seus vários certificados inserindo &quot; `fairplay`&quot; no campo de pesquisa localizado na parte superior direita.
   1. Identifique o certificado FairPlay da sua empresa.

      O nome da sua empresa deve estar associado ao certificado emitido pela Apple.
   1. Expanda o certificado selecionando a seta de expansão e clique com o botão direito do mouse em sua chave privada.
   1. Selecionar **[!UICONTROL Export "Your Company Name"]** e salve a variável [!DNL .p12] arquivo.

      Você será solicitado a atribuir uma senha para proteger este arquivo. Anote essa senha, pois será necessário enviá-la com seu pacote de credenciais.
   1. Fazer logon em sua conta em [www.expressplay.com](https://www.expressplay.com).
   1. Clique em **[!UICONTROL DRM SERVICES]** na parte superior esquerda, selecione a **[!UICONTROL FairPlay]** guia.
   1. Faça upload das credenciais do FairPlay para sua conta ExpressPlay.

      1. Crie um arquivo de texto que contenha o valor de sua ASK (deve ter 32 caracteres, por exemplo: `1234567890abcdef1234567890abcdef`) e selecione esse arquivo para upload.
      1. Selecione o arquivo PKCS12 na Etapa 4.f. para fazer upload.
      1. Digite a senha do arquivo PKCS12 da Etapa 4.f.
      1. Clique no botão Upload.

Agora você pode criar aplicativos iOS ou páginas HTML5 com proteção de conteúdo FairPlay, juntamente com seu [!DNL fairplay.cer] usando o serviço ExpressPlay para FairPlay.

<!--<a id="fig_sjr_2pn_sv"></a>-->

![](assets/multi_drm_expressplay_drm_services_web.png)

### Empacotar seu conteúdo para FairPlay {#package-your-content-for-fairplay}

Para empacotar seu conteúdo, você pode usar o Adobe Offline Packager ou outras ferramentas, como o Bento4 do ExpressPlay.

Os empacotadores preparam o vídeo para reprodução (por exemplo, fragmentando o arquivo original e colocando-o em um manifesto) e protegem o vídeo com a solução DRM escolhida (neste caso, FairPlay):

* [Adobe Offline Packager para FairPlay DRM](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=21)
* [Encapsuladores ExpressPlay - Bento4 para HLS](https://www.bento4.com/developers/hls/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_hls_web.png)

1. Empacotar o conteúdo.

   Veja um exemplo de empacotamento usando o Adobe Offline Packager. O Packager usa um arquivo de configuração (por exemplo, [!DNL fairplay.xml]), que tem esta aparência:

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

   * `in_path` - Essa entrada aponta para o local do vídeo de origem na máquina de empacotamento local.
   * `out_type` - Esta entrada descreve o tipo de saída empacotada, neste caso HLS para FairPlay.
   * `out_path` - O local no computador local para onde você deseja que a saída seja enviada.
   * `drm_sys` - A solução DRM para a qual você está empacotando. Isso é `FAIRPLAY` neste caso.
   * `frag_dur` - Duração do fragmento em segundos.
   * `target_dur` - A duração alvo para saída HLS.
   * `key_file_path` - Esse é o local do arquivo de licença em sua máquina de empacotamento que serve como sua Chave de criptografia de conteúdo (CEK). É uma sequência hexadecimal codificada na Base 64 de 16 bytes.
   * `iv_file_path` - Este é o local do arquivo IV em sua máquina de empacotamento.
   * `key_url` - O parâmetro URI do `EXT-X-KEY` da tag [!DNL .m3u8] arquivo.
   * `content_id` - Valor padrão.

   Tal como referido no [Documentação do Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=7), &quot;Como prática recomendada, crie um arquivo de configuração que contenha as opções comuns que você deseja usar para gerar as saídas. Em seguida, crie a saída fornecendo opções específicas como argumento de linha de comando.&quot;

   ```
   java -jar OfflinePackager.jar -in_path sample.mp4 -out_type hls 
   -out_path out_file_path -drm -drm_sys FAIRPLAY -key_file_path "creds/fairplay.bin" 
   -key_url "user_provided_value"
   ```

   O arquivo M3U8 gerado tem um `EXT-X-KEY` atributo que aparece da seguinte maneira:

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="user_provided_value",​
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1" 
   ```

### Definição de políticas para FairPlay {#setting-policies-for-fairplay}

Você pode definir políticas para conteúdo protegido por FairPlay usando um servidor de direitos. Você pode configurar o seu próprio ou usar um servidor de direitos de amostra fornecido pelo Adobe.

O Adobe fornece um Exemplo de Servidor de Direitos ExpressPlay (SEES) que mostra como fazer *baseado em tempo* e *vinculação de dispositivos* direito. Este exemplo de servidor de direito é criado sobre os serviços ExpressPlay.

[Servidor de Referência: Exemplo de Servidor de Direitos ExpressPlay (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

* [Serviço de Referência: Direito com Base no Tempo](../../multi-drm-workflows/feature-topics/sees-reference-server-time-entitlement.md)
* [Serviço de Referência: Direito de Vinculação de Dispositivo](../../multi-drm-workflows/feature-topics/sees-reference-server-binding-entitlement.md)

## Licenciamento e reprodução para FairPlay {#licensing-and-playback-for-fairplay}

O licenciamento e a reprodução de conteúdo protegido pelo FairPlay exigem a troca de esquemas de URL, entre o esquema usado no arquivo de manifesto de vídeo (skd:) e o usado nas solicitações de token do ExpressPlay (https:).

As instruções para implementar o licenciamento e a reprodução de um cliente iOS TVSDK estão aqui: [Habilitar o Apple FairPlay em aplicativos TVSDK](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md). Também é possível implementar a reprodução offline e a rotação de licenças para o FairPlay.

## HLS Offline com FairPlay {#section_047A05D1E3B64883858BC601CFC8F759}

Talvez você queira permitir que os usuários reproduzam conteúdo protegido pelo FairPlay quando o licenciamento não for recuperável, pois o reprodutor está isolado da Web (como em um avião).

Antes de começar esta tarefa, baixe e leia o documento do Apple **&quot;Reprodução offline com FairPlay Streaming e HTTP Live Streaming&quot;**. Leia o guia para saber como baixar segmentos de transmissão (TS) e salvá-los em seu computador local.

Implementar reprodução offline para FairPlay com este fluxo de trabalho:

1. Baixe o segmento HLS TS.
1. Solicitar licença de Aluguel Persistente do servidor FairPlay (consulte **&quot;FairPlay Política de Aluguel Persistente&quot;**).
1. Salve o `persistentContentKey`.
1. Reproduzir o conteúdo FairPlay offline.

>[!NOTE]
>
>A transmissão FairPlay no cliente não inicia a descriptografia se a chave de conteúdo persistente tiver expirado. No entanto, ela continuará a experiência do usuário se a chave de conteúdo expirar durante a reprodução.
>
>Consulte [Trabalhar com transmissão HTTP em tempo real](https://developer.apple.com/library/content/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/HTTPLiveStreaming/HTTPLiveStreaming.html#//apple_ref/doc/uid/TP40016757-CH11-SW3) para obter mais detalhes.

### Rotação de licença do FairPlay {#section_D32AA08C61474B4F876AC2A5F18CB879}

A rotação de licenças é um esquema para evitar o hacking de licenças de conteúdo reproduzido por muito tempo.

Em um manifesto M3U8, cada tag de chave será aplicada aos seguintes segmentos TS até a próxima tag de chave ou até o final do arquivo.

Para adicionar rotação de licença, faça o seguinte:

* Insira uma nova tag de chave FairPlay durante o tempo de rotação da licença.

   É possível adicionar qualquer número de tags principais.

   Para conteúdo linear, mantenha a tag de chave mais recente na janela M3U8. O iOS solicitará o próximo M3U8 quando houver cerca de dois segmentos TS restantes para serem reproduzidos (cerca de 20 segundos). Se o novo M3U8 contiver novas tags principais, todas as solicitações principais ocorrerão imediatamente. As chaves existentes anteriores não serão solicitadas novamente. O iOS aguardará a conclusão de todas as solicitações principais antes de iniciar a reprodução.

   Para conteúdos de VOD com rotação de licença, todas as solicitações de chave ocorrerão no início da reprodução.

   A seguir, há uma amostra de M3U8 com rotação de chaves:

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
