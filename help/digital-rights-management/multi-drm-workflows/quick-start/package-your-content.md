---
description: O empacotamento de conteúdo é o processo de preparação de conteúdo de vídeo para reprodução na Web. O empacotamento inclui a transformação de vídeo bruto em arquivos de manifesto e, opcionalmente, a criptografia do conteúdo usando diferentes soluções DRM para dispositivos e navegadores diferentes.
seo-description: O empacotamento de conteúdo é o processo de preparação de conteúdo de vídeo para reprodução na Web. O empacotamento inclui a transformação de vídeo bruto em arquivos de manifesto e, opcionalmente, a criptografia do conteúdo usando diferentes soluções DRM para dispositivos e navegadores diferentes.
seo-title: Empacote seu conteúdo
title: Empacote seu conteúdo
uuid: b9bc6104-a1ea-4ea0-a0a4-af8a606e5d47
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Empacote seu conteúdo {#package-your-content}

O empacotamento de conteúdo é o processo de preparação de conteúdo de vídeo para reprodução na Web. O empacotamento inclui a transformação de vídeo bruto em arquivos de manifesto e, opcionalmente, a criptografia do conteúdo usando diferentes soluções DRM para dispositivos e navegadores diferentes.

Para preparar seu conteúdo, você pode usar o Adobe Offline Packager ou outras ferramentas, como o empacotador Bento4 do ExpressPlay. Os Packagers preparam o vídeo para reprodução (por exemplo, fragmentando o arquivo original e colocando-o em um manifesto) e protegem o vídeo com a solução DRM escolhida (PlayReady, Widevine, FairPlay, Access etc.):

* [Adobe Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [ExpressPlay Packagers](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. Compacte ou obtenha conteúdo para usar para testar sua configuração.

   Um dos pontos cruciais a lembrar para o empacotamento é que a ID-chave (ID de conteúdo) usada nessa etapa de empacotamento é a mesma que você deve fornecer na solicitação subsequente do token de licença. A ID da chave é o único item que identifica seu CEK (que pode ser armazenado em seu próprio banco de dados de gerenciamento de chave) ou armazenado usando o Serviço [de armazenamento de chave do](https://www.expressplay.com/developer/key-storage/)ExpressPlay.

   >[!NOTE]
   >
   >Para aqueles que estão familiarizados com o Adobe Access, essa é uma diferença importante em como as diferentes soluções funcionam. No Access, a chave de Licença está incorporada nos Metadados DRM e é transmitida para frente e para trás com o conteúdo protegido. Nos sistemas Multi-DRM descritos aqui, a Licença real não é aprovada, mas armazenada com segurança e obtida por meio da ID da chave.

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

Este é um exemplo de empacotamento usando o Adobe Offline Packager for Widevine. O Packager usa um arquivo de configuração (por exemplo, [!DNL widevine.xml]), que se parece com o seguinte:

```
<config> 
<in_path>sample.mp4</in_path> 
<out_type>dash</out_type> 
<out_path>dash2</out_path> 
<drm/> 
<drm_sys>widevine</drm_sys> 
<frag_dur>4</frag_dur> 
<target_dur>6</target_dur> 
<key_file_path>keyfile.bin</key_file_path> 
<widevine_content_id>2a</widevine_content_id> 
<widevine_provider>intertrust</widevine_provider> 
<widevine_key_id>7debe705d938c76bfd886f077b8fa5f7</widevine_key_id> 
</config>
```

* `in_path` - Essa entrada aponta para o local do vídeo de origem em sua máquina de embalagem local.
* `out_type` - Esta entrada descreve o tipo de saída empacotada, neste caso DASH (para proteção de Widevine em HTML5).
* `out_path` - O local na máquina local para onde deseja que a saída seja enviada.
* `drm_sys` - A solução DRM para a qual você está empacotando. Isto será `widevine`, `fairplay`ou `playready`.

* `frag_dur` e `target_dur` são entradas de duração específicas do DASH pertencentes à reprodução do vídeo.

* `key_file_path` - Este é o local do arquivo de licença no seu computador de empacotamento que serve como sua Chave de criptografia de conteúdo (CEK). É uma string hexadecimal de 16 bytes codificada em Base 64.
* `widevine_content_id` - Viúva &quot;estereotipada&quot;; é sempre `2a`. (Não confunda isso com o `widevine_key_id`.)

* `widevine_provider` - Para os nossos propósitos, sempre defina para `intertrust`.

* `widevine_key_id` - Este é o identificador da licença especificada na `key_file_path` entrada. Em outras palavras, isso identifica a chave que você usa para criptografar o conteúdo. Essa ID é uma string HEX de 16 bytes que você mesmo cria.

Conforme declarado na documentação [do](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)Packager, &quot;Como prática recomendada, crie um arquivo de configuração que contenha as opções comuns que você deseja usar para gerar as saídas. Em seguida, crie a saída fornecendo opções específicas como um argumento de linha de comando.&quot; Nesse caso, nosso arquivo de configuração está bastante completo, portanto, você pode criar sua saída da seguinte maneira:

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>Parâmetros de linha de comando têm prioridade sobre os parâmetros do arquivo de configuração. Neste exemplo, tudo o que é necessário está no arquivo de configuração, mas substituímos o caminho de saída especificado no arquivo de configuração por `-out_path test_dash/`.

