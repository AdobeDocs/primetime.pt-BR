---
description: O Adobe Offline Packager assume como entrada conteúdo mp4 não criptografado.
title: Compacte seu conteúdo com o Adobe Offline Packager
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Compacte seu conteúdo com o Adobe Offline Packager{#package-your-content-with-adobe-offline-packager}

O Adobe Offline Packager assume como entrada conteúdo mp4 não criptografado.

**Chamando o Adobe Offline Packager**

Uma chamada típica do adobe offline packager seria semelhante à chamada abaixo:

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dc7ecf3 1a8ebf1b7dda5
    -widevine_provider intertrust
    -playready_LA_
    URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7dda5
    -content_id c595f21 4d84dc7ecf31a8ebf1b7dda5

Nesse caso específico, o empacotador offline está adicionando dados de inicialização de proteção de conteúdo Widevine e PlayReady ao conteúdo DASH de saída. O valor de `-key_file_path` é para uma chave codificada em base64. O valor de `-playready_LA_URL` é para aquisição da licença PlayReady.

O argumento conf_path aponta para o arquivo de configuração que conteria o seguinte:

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>falso&lt;/encrypt_audio>
    &lt;/config>

Como certos dispositivos Android — principalmente o Amazon Fire TV — não suportam a descriptografia de áudio, a criptografia de áudio é opcional.
