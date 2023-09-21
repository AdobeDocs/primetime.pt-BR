---
description: O conteúdo de empacotamento é o processo de preparação do conteúdo de vídeo para reprodução na Web. O empacotamento inclui a transformação de vídeo bruto em arquivos manifest e, opcionalmente, a criptografia do conteúdo usando diferentes soluções de DRM para diferentes dispositivos e navegadores.
title: Empacotar o conteúdo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Empacotar o conteúdo {#package-your-content}

O conteúdo de empacotamento é o processo de preparação do conteúdo de vídeo para reprodução na Web. O empacotamento inclui a transformação de vídeo bruto em arquivos manifest e, opcionalmente, a criptografia do conteúdo usando diferentes soluções de DRM para diferentes dispositivos e navegadores.

Para preparar seu conteúdo, você pode usar o Adobe Offline Packager ou outras ferramentas, como o Bento4 do ExpressPlay. Os empacotadores preparam o vídeo para reprodução (por exemplo, fragmentando o arquivo original e colocando-o em um manifesto) e protegem o vídeo com a solução de DRM escolhida (PlayReady, Widevine, FairPlay, Access etc.):

* [Adobe Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [Encapsuladores ExpressPlay](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. Empacote ou obtenha conteúdo para usar para testar sua configuração.

   Um dos pontos cruciais a serem lembrados para o empacotamento é que a ID de chave (ID de conteúdo) usada nesta etapa do empacotamento é a mesma que você deve fornecer em sua solicitação de token de licença subsequente. A ID da chave é o único item que identifica o CEK (que pode ser armazenado em seu próprio banco de dados de gerenciamento de chaves ou armazenado usando [Serviço de armazenamento de chaves do ExpressPlay](https://www.expressplay.com/developer/key-storage/).

   >[!NOTE]
   >
   >Para os que estão familiarizados com o Adobe Access, essa é uma diferença importante em como as diferentes soluções funcionam. No Access, a chave de licença é incorporada aos metadados de DRM e transmitida para frente e para trás com o conteúdo protegido. Nos sistemas Multi-DRM descritos aqui, a Licença real não é passada, mas armazenada com segurança e obtida por meio da ID da chave.

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

Este é um exemplo de empacotamento usando o Adobe Offline Packager para Widevine. O Packager usa um arquivo de configuração (por exemplo, [!DNL widevine.xml]), que tem esta aparência:

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

* `in_path` - Essa entrada aponta para o local do vídeo de origem na máquina de empacotamento local.
* `out_type` - Esta entrada descreve o tipo de saída empacotada, neste caso DASH (para proteção Widevine no HTML5).
* `out_path` - O local no computador local para onde você deseja que a saída seja enviada.
* `drm_sys` - A solução DRM para a qual você está empacotando. Isso será `widevine`, `fairplay`ou `playready`.

* `frag_dur` e `target_dur` são entradas de duração específicas ao DASH relacionadas à reprodução de vídeo.

* `key_file_path` - Esse é o local do arquivo de licença em sua máquina de empacotamento que serve como sua Chave de criptografia de conteúdo (CEK). É uma sequência hexadecimal codificada na Base 64 de 16 bytes.
* `widevine_content_id` - Este é Widevine &quot;boilerplate&quot;; é sempre `2a`. (Não confunda com o `widevine_key_id`.)

* `widevine_provider` - Para nossos propósitos, sempre defina este como `intertrust`.

* `widevine_key_id` - Este é o identificador da licença especificada na `key_file_path` entrada. Em outras palavras, isso identifica a chave usada para criptografar o conteúdo. A ID é uma sequência HEX de 16 bytes que você mesmo cria.

Tal como referido no [Documentação do Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf), &quot;Como prática recomendada, crie um arquivo de configuração que contenha as opções comuns que você deseja usar para gerar as saídas. Em seguida, crie a saída fornecendo opções específicas como argumento de linha de comando.&quot; Nesse caso, nosso arquivo de configuração está razoavelmente completo, portanto, você pode criar sua saída da seguinte maneira:

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>Os parâmetros da linha de comando têm prioridade sobre os parâmetros do arquivo de configuração. Neste exemplo, tudo o que é necessário está no arquivo de configuração, mas substituímos o caminho de saída especificado no arquivo de configuração por `-out_path test_dash/`.
