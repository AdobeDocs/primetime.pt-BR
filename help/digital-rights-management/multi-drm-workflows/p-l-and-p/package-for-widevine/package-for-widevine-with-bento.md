---
description: Usamos o empacotador Bento4 e o empacotador offline da Adobe para criar conteúdo DASH criptografado. Bento4 assume como entrada conteúdo mp4 não criptografado.
seo-description: Usamos o empacotador Bento4 e o empacotador offline da Adobe para criar conteúdo DASH criptografado. Bento4 assume como entrada conteúdo mp4 não criptografado.
seo-title: Compacte seu conteúdo com o Bento4
title: Compacte seu conteúdo com o Bento4
uuid: 88323a4e-d0b5-4a41-acec-7126d3e0c90b
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Conteúdo de empacotamento para Widevine e PlayReady {#package-for-widevine}

Usamos o empacotador Bento4 e o empacotador offline da Adobe para criar conteúdo DASH criptografado. Bento4 assume como entrada conteúdo mp4 não criptografado.

## Compacte seu conteúdo com o Bento4{#package-your-content-with-bento}

O empacotador Bento4 espera que a entrada mp4 seja pré-fragmentada. A distribuição do empacotador Bento4 inclui uma ferramenta para isso.

**Chamando Bento4**

As invocações típicas do empacotador Bento4 seriam semelhantes aos exemplos abaixo:

    ./mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —legendas
    —chave de criptografia=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd 09fc0747c7c5ac215b3b
    —widevine
    —widevine-header=provider:intertrust#content_id:2a &quot;CC_300_640x360.mp4&quot;
    -o &quot;CC_300_640x36 0_DASH&quot;
>
    ./mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —legendas
    —chave de criptografia=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd 09fc0747c7c5ac215b3b
    —playready
    —playready-header=\&quot;LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\&quot;

O exemplo abaixo combina esquemas PlayReady e Widevine. Nesse caso específico, o empacotador está adicionando dados de inicialização de proteção de conteúdo do Widevine e PlayReady ao conteúdo de saída DASH.

    /mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —legendas
    —chave de criptografia=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd 09fc0747c7c5ac215b3b
    —playready
    —playready-header=\&quot;LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\&quot;
    —widevine
    —widevine-header=provider:intertrust#content_id:2a &quot;CC_300_640x360.mp4&quot;
    
    
    - o &quot;CC_300_640x360_DASH&quot;onde

O valor do `--encryption-key` sinalizador está no formulário `<base16 encoded key id>:<base16 encoded encryption key>`.

O sinalizador `--widevine-header=provider:intertrust#content_id:2a` informa ao empacotador que inclua a caixa pssh no manifesto, que o TVSDK atualmente requer para reprodução.
O valor para `-playready-header` é para aquisição de licença PlayReady.

## Compacte seu conteúdo com o Adobe Offline Packager {#package-your-content-with-adobe-offline-packager}

O Adobe Offline Packager utiliza como entrada conteúdo mp4 não criptografado.

**Chamada do Adobe Offline Packager**

Uma chamada típica do adobe offline packager seria semelhante à chamada abaixo:

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dc7ecf3 1a8ebf1b7dda5
    -widevine_provider intertrust
    -playready_LA_
    URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7dda5
    -content_id c595f211 4d84dc7ecf31a8ebf1b7dda5

Nesse caso específico, o empacotador offline está adicionando dados de inicialização de proteção de conteúdo do Widevine e PlayReady ao conteúdo de saída DASH. O valor de `-key_file_path` é para uma chave codificada em base64. O valor de `-playready_LA_URL` é para aquisição de licença PlayReady.

O argumento conf_path aponta para o arquivo de configuração que conteria o seguinte:

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>falso&lt;/encrypt_audio>
    &lt;/config>

Porque certos dispositivos Android... principalmente a Amazon Fire TV. não suporta a descriptografia de áudio, a criptografia de áudio é opcional.