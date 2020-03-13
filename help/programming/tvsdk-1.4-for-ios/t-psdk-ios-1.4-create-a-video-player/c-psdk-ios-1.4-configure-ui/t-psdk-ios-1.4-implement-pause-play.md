---
description: Você pode configurar botões que chamam métodos TVSDK para pausar e reproduzir a mídia.
seo-description: Você pode configurar botões que chamam métodos TVSDK para pausar e reproduzir a mídia.
seo-title: Implantação de um botão reproduzir/pausar
title: Implantação de um botão reproduzir/pausar
uuid: eccdce4b-0114-4389-b5ee-74fe62d38ed8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Implantação de um botão reproduzir/pausar{#implement-a-play-pause-button}

Você pode configurar botões que chamam métodos TVSDK para pausar e reproduzir a mídia.

Use o seguinte código de amostra para implementar um botão de reprodução ou pausa:

<!--<a id="example_BC2632D673FE451190A30A23145090D0"></a>-->

```
_playPauseButton =  
[[UIButton alloc] initWithFrame:CGRectMake(BUTTON_POS_X, BUTTON_POS_Y, BUTTON_SIZE_W, BUTTON_SIZE_H)]; 
[_playPauseButton setImage:[UIImage imageNamed:@"play.png"] forState:UIControlStateNormal];  
[_playPauseButton setImage:[UIImage imageNamed:@"pause.png"] forState:UIControlStateSelected]; 
[_playPauseButton addTarget:self action:@selector(playTouch:) forControlEvents:UIControlEventTouchUpInside]; 
[self addSubview:_playPauseButton]; 
 
... 
 
- (void)playTouch:(id)sender { 
    if (self.player.status == PTMediaPlayerStatusPlaying) { 
        _playPauseButton.selected = YES;  
        [self.player pause]; 
    } 
    else { 
        _playPauseButton.selected = NO; [self.player play]; 
    } 
} 
```

