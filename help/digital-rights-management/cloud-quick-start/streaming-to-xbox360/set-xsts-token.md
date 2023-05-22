---
title: Definir o token XSTS no reprodutor
description: Definir o token XSTS no reprodutor
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# Definir o token XSTS no reprodutor{#set-the-xsts-token-in-your-player}

No Xbox360, você define o token de forma assíncrona em resposta ao `MediaPlayer.RequestKeyAttribute` evento.

Defina o token XSTS.

O aplicativo de amostra fornecido com seu software mostra como definir o token XSTS no reprodutor. Este é o trecho de código relevante do reprodutor de amostra:

```
   MediaPlayer mMediaPlayer;  
 
mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
 
private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
    string token = "";  
    // XBOX XSTS Token...  
    KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
    mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
} 
```

