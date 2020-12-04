---
description: Os recursos do TVSDK são orientados pela configuração e implementados pelo MediaPlayer.
seo-description: Os recursos do TVSDK são orientados pela configuração e implementados pelo MediaPlayer.
seo-title: Criação de gerenciadores de recursos transmitindo informações de configuração para o MediaPlayer
title: Criação de gerenciadores de recursos transmitindo informações de configuração para o MediaPlayer
uuid: 106ececd-a670-4360-b000-a31fec65233c
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Criação de gerenciadores de recursos transmitindo informações de configuração para o MediaPlayer {#creating-feature-managers-by-passing-configuration-information-to-the-mediaplayer}

Os recursos do TVSDK são orientados pela configuração e implementados pelo MediaPlayer.

* A configuração é a lista de configurações específicas para o recurso, como a taxa de bits inicial do controle ABR e a visibilidade padrão de legenda fechada.

   Os gerentes de recursos precisam obter as configurações para determinar o comportamento do recurso.

   Na implementação da referência Primetime, a configuração é armazenada em preferências compartilhadas, mas você pode armazenar a configuração de qualquer forma que faça sentido para o seu ambiente.

* `MediaPlayer` é o objeto do player de mídia TVSDK que contém o recurso de vídeo.

   Os gerentes de recursos registram ouvintes de evento TVSDK para esse objeto do player, recuperam dados da sessão de reprodução e acionam recursos TVSDK para a sessão de reprodução.

Cada recurso tem uma interface de configuração correspondente. Por exemplo, `CCManager` usa `ICCConfig` para recuperar a configuração. `ICCConfig` contém métodos para obter as informações de configuração relacionadas somente a legendagem fechada.

O exemplo a seguir mostra o arquivo [!DNL ICCConfig.java], configurado para receber informações sobre visibilidade de legenda fechada, estilo de fonte e borda de fonte de `MediaPlayer`:

```java
// Constructor of CCManager 
 
<b>public CCManager(ICCConfig ccConfig, MediaPlayer mediaPlayer) {...}</b> 
  
// ICCConfig methods 
 
<b>public interface ICCConfig {</b> 
  
    /** 
     * Get the closed captioning visibility config 
     * 
     * @return true if visibility is set to true, false otherwise 
     */ 
    
<b> public boolean getCCVisibility();</b> 
  
    /** 
     * Get the closed captioning font style 
     * 
     * @return TextFormat.Font object represents font style 
     */ 
     
<b>public TextFormat.Font getCCFont();</b>

    /** 
     * Get the closed captioning font edge 
     * 
     * @return TextFormat.FontEdge represents of font edge 
     */ 
     
<b>public TextFormat.FontEdge getCCFontEdge();</b> 
... 
}
```

Um aplicativo que usa um recurso TVSDK pode criar seu gerenciador de recursos com um provedor de configuração e um objeto `MediaPlayer`. Por exemplo:

```java
// This application needs to use the advertising workflow feature 
AdsManager adsManager = new AdsManagerOn();
```

Documentos da API de configuração do gerenciador de recursos: [Javadoc](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html)