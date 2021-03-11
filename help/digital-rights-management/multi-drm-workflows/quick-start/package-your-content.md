---
description: O empacotamento de conteúdo é o processo de preparação do conteúdo de vídeo para reprodução na Web. O empacotamento inclui a transformação de vídeo bruto em arquivos de manifesto e, opcionalmente, a criptografia do conteúdo usando diferentes soluções de DRM para diferentes dispositivos e navegadores.
title: Encapsulamento seu conteúdo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Compacte seu conteúdo {#package-your-content}

O empacotamento de conteúdo é o processo de preparação do conteúdo de vídeo para reprodução na Web. O empacotamento inclui a transformação de vídeo bruto em arquivos de manifesto e, opcionalmente, a criptografia do conteúdo usando diferentes soluções de DRM para diferentes dispositivos e navegadores.

Para preparar seu conteúdo, você pode usar o Adobe Offline Packager ou outras ferramentas, como o Bento4 Packager do ExpressPlay. Os empacotadores preparam o vídeo para reprodução (por exemplo, fragmentando o arquivo original e colocando-o em um manifesto) e protegem o vídeo com a solução DRM escolhida (PlayReady, Widevine, FairPlay, Access etc.):

* [Pacote Offline do Adobe](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [Pacotes do ExpressPlay](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. Compacte ou obtenha conteúdo para usar nos testes de configuração.

   Um dos pontos cruciais a lembrar para o empacotamento é que a ID de chave (ID de conteúdo) usada nessa etapa do empacotamento é a mesma que você deve fornecer na solicitação de token de licença subsequente. A ID da chave é o único item que identifica o CEK (que pode ser armazenado no seu próprio banco de dados de gerenciamento de chaves ou armazenado usando o [Serviço de armazenamento de chaves do ExpressPlay](https://www.expressplay.com/developer/key-storage/).

   >[!NOTE]
   >
   >Para aqueles que estão familiarizados com o Adobe Access, essa é uma diferença importante em como as diferentes soluções funcionam. No Access, a chave de licença é incorporada aos metadados de DRM e transmitida para frente e para trás com o conteúdo protegido. Nos sistemas Multi-DRM descritos aqui, a Licença real não é transmitida, mas armazenada em segurança e obtida por meio da ID da chave.

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

Este é um exemplo de empacotamento usando o Adobe Offline Packager for Widevine. O Packager usa um arquivo de configuração (por exemplo, [!DNL widevine.xml]), que tem a seguinte aparência:

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
* `out_type` - Essa entrada descreve o tipo da saída empacotada, neste caso DASH (para proteção de Widevine em HTML5).
* `out_path` - O local na máquina local onde você deseja que a saída vá.
* `drm_sys` - A solução de DRM para a qual você está fazendo o empacotamento. Isso será `widevine`, `fairplay` ou `playready`.

* `frag_dur` e  `target_dur` são entradas de duração específicas de DASH pertencentes à reprodução de vídeo.

* `key_file_path` - Esse é o local do arquivo de licença em sua máquina de embalagem que serve como sua Chave de criptografia de conteúdo (CEK). É uma string hexadecimal codificada em Base 64 de 16 bytes.
* `widevine_content_id` - Viúva &quot;estereotipada&quot;; é sempre  `2a`. (Não confunda com `widevine_key_id`.)

* `widevine_provider` - Para nosso propósito, sempre defina isso como  `intertrust`.

* `widevine_key_id` - Esse é o identificador da licença especificada na  `key_file_path` entrada. Em outras palavras, isso identifica a chave usada para criptografar o conteúdo. Essa ID é uma cadeia de caracteres HEX de 16 bytes criada por você mesmo.

Conforme declarado na [Documentação do Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf), &quot;Como prática recomendada, crie um arquivo de configuração que contenha as opções comuns que você deseja usar para gerar as saídas. Em seguida, crie a saída fornecendo opções específicas como um argumento de linha de comando.&quot; Nesse caso, nosso arquivo de configuração é bastante completo, portanto, você pode criar sua saída da seguinte maneira:

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>Os parâmetros da linha de comando têm prioridade sobre os parâmetros do arquivo de configuração. Neste exemplo, tudo o que é necessário está no arquivo de configuração, mas substituímos o caminho de saída especificado no arquivo de configuração por `-out_path test_dash/`.

