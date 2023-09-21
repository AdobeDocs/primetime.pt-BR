---
description: O Adobe Offline Packager assume como entrada o conteúdo mp4 não criptografado.
title: Empacotar o conteúdo com o Adobe Offline Packager
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Empacotar o conteúdo com o Adobe Offline Packager{#package-your-content-with-adobe-offline-packager}

O Adobe Offline Packager assume como entrada o conteúdo mp4 não criptografado.

**Chamando o Adobe Offline Packager**

Uma invocação típica do empacotador offline da Adobe seria semelhante à chamada abaixo:

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jigo.mp4&quot;
    -out_path &quot;Jigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
    -widevine_provider interconfiança
    -playready_LA_URL
    http://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
    -content_id c595f214d84dc7ecf31a8ebf1b7ddda5

Nesse caso específico, o empacotador offline está adicionando dados de inicialização da proteção de conteúdo Widevine e da proteção de conteúdo PlayReady ao conteúdo DASH de saída. O valor de `-key_file_path` é para uma chave codificada em base64. O valor de `-playready_LA_URL` é para aquisição de licença do PlayReady.

O argumento conf_path aponta para o arquivo de configuração que conteria o seguinte:

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

Como alguns dispositivos Android — principalmente o Amazon Fire TV — não oferecem suporte à descriptografia de áudio, a criptografia de áudio é opcional.
