---
description: Usamos o empacotador Bento4 e o empacotador off-line Adobe para criar conteúdo DASH criptografado. Bento4 assume como entrada conteúdo mp4 não criptografado.
title: Empacotar seu conteúdo com Bento4
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Conteúdo de empacotamento para Widevine e PlayReady {#package-for-widevine}

Usamos o empacotador Bento4 e o empacotador off-line Adobe para criar conteúdo DASH criptografado. Bento4 assume como entrada conteúdo mp4 não criptografado.

## Empacotar seu conteúdo com Bento4{#package-your-content-with-bento}

O empacotador Bento4 espera que o mp4 de entrada seja pré-fragmentado. A distribuição do empacotador Bento4 inclui uma ferramenta para isso.

**Chamando Bento4**

As invocações de empacotador Bento4 típicas seriam semelhantes aos exemplos abaixo:

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
```

O exemplo abaixo combina esquemas PlayReady e Widevine. Nesse caso específico, o empacotador está adicionando dados de inicialização da proteção de conteúdo Widevine e da proteção de conteúdo PlayReady ao conteúdo DASH de saída.

```
/mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

onde

O valor para a variável `--encryption-key` o sinalizador está no formulário `<base16 encoded key id>:<base16 encoded encryption key>`.

A variável `--widevine-header=provider:intertrust#content_id:2a` O sinalizador informa ao empacotador para incluir a caixa de push no manifesto, que o TVSDK exige atualmente para reprodução.

O valor de `-playready-header` é para aquisição de licença do PlayReady.

## Empacotar o conteúdo com o Adobe Offline Packager {#package-your-content-with-adobe-offline-packager}

O Adobe Offline Packager assume como entrada o conteúdo mp4 não criptografado.

**Chamando o Adobe Offline Packager**

Uma invocação típica do empacotador offline da Adobe seria semelhante à chamada abaixo:

```
java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path "Jaigo.mp4"
-out_path "Jaigo_DASH"
-key_file_path "Jaigo_DASH/_info/key.B64.random"
-widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
-widevine_provider intertrust
-playready_LA_URL
http://pr.test.expressplay.com/playready/RightsManager.asmx
-playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
-content_id c595f214d84dc7ecf31a8ebf1b7ddda5
```

Nesse caso específico, o empacotador offline está adicionando dados de inicialização da proteção de conteúdo Widevine e da proteção de conteúdo PlayReady ao conteúdo DASH de saída. O valor de `-key_file_path` é para uma chave codificada em base64. O valor de `-playready_LA_URL` é para aquisição de licença do PlayReady.

O argumento conf_path aponta para o arquivo de configuração que conteria o seguinte:

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

Como alguns dispositivos Android — principalmente o Amazon Fire TV — não oferecem suporte à descriptografia de áudio, a criptografia de áudio é opcional.
