---
description: Você pode configurar botões que chamam métodos TVSDK para pausar e reproduzir a mídia.
seo-description: Você pode configurar botões que chamam métodos TVSDK para pausar e reproduzir a mídia.
seo-title: Implantação de um botão reproduzir/pausar
title: Implantação de um botão reproduzir/pausar
uuid: b0ce4103-819e-4a1c-8238-1d7728ec8770
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d

---


# Implantação de um botão reproduzir/pausar {#implement-a-play-pause-button}

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
