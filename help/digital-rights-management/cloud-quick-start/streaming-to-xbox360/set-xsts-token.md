---
description: nulo
seo-description: nulo
seo-title: Defina o token XSTS no player
title: Defina o token XSTS no player
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: b7f52b71bde1d7bf59ef51d4f6f90dfaa07e347b
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---


# Defina o token XSTS no player{#set-the-xsts-token-in-your-player}

No Xbox360, você define o token de forma assíncrona em resposta ao evento `MediaPlayer.RequestKeyAttribute`.

Defina o token XSTS.

O aplicativo de amostra fornecido com seu software mostra como definir o token XSTS no player. Este é o trecho de código relevante do player de amostra:

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

