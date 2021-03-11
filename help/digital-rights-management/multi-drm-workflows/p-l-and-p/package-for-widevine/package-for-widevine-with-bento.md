---
description: Usamos o pacote Bento4 e o Adobe offline packager para criar conteúdo DASH criptografado. O Bento4 assume como entrada conteúdo mp4 não criptografado.
title: Compacte seu conteúdo com o Bento4
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Conteúdo de empacotamento para Widevine e PlayReady {#package-for-widevine}

Usamos o pacote Bento4 e o Adobe offline packager para criar conteúdo DASH criptografado. O Bento4 assume como entrada conteúdo mp4 não criptografado.

## Embale seu conteúdo com o Bento4{#package-your-content-with-bento}

O empacotador Bento4 espera que o mp4 de entrada seja pré-fragmentado. A distribuição do empacotador Bento4 inclui uma ferramenta para isso.

**Chamada de Bento4**

As invocações típicas do Bento4 packager seriam semelhantes aos exemplos abaixo:

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

O exemplo abaixo combina esquemas PlayReady e Widevine. Nesse caso específico, o empacotador está adicionando dados de inicialização da proteção de conteúdo Widevine e PlayReady ao conteúdo DASH de saída.

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

em que

O valor do sinalizador `--encryption-key` está no formato `<base16 encoded key id>:<base16 encoded encryption key>`.

O sinalizador `--widevine-header=provider:intertrust#content_id:2a` informa ao empacotador para incluir a caixa de push no manifesto, que o TVSDK atualmente requer para reprodução.

O valor de `-playready-header` é para aquisição da licença PlayReady.

## Compacte seu conteúdo com o Adobe Offline Packager {#package-your-content-with-adobe-offline-packager}

O Adobe Offline Packager assume como entrada conteúdo mp4 não criptografado.

**Chamando o Adobe Offline Packager**

Uma chamada típica do adobe offline packager seria semelhante à chamada abaixo:

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

Nesse caso específico, o empacotador offline está adicionando dados de inicialização de proteção de conteúdo Widevine e PlayReady ao conteúdo DASH de saída. O valor de `-key_file_path` é para uma chave codificada em base64. O valor de `-playready_LA_URL` é para aquisição da licença PlayReady.

O argumento conf_path aponta para o arquivo de configuração que conteria o seguinte:

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

Como certos dispositivos Android — principalmente o Amazon Fire TV — não suportam a descriptografia de áudio, a criptografia de áudio é opcional.
