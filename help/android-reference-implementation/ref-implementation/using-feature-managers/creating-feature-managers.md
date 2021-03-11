---
description: Os recursos TVSDK são orientados pela configuração e implementados por meio do MediaPlayer.
title: Criação de gerenciadores de recursos ao passar informações de configuração para o MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Criação de gerenciadores de recursos ao transmitir informações de configuração para o MediaPlayer {#creating-feature-managers-by-passing-configuration-information-to-the-mediaplayer}

Os recursos TVSDK são orientados pela configuração e implementados por meio do MediaPlayer.

* Configuração é a lista de configurações específicas para o recurso, como a taxa de bits inicial do controle ABR e a visibilidade de legendas ocultas padrão.

   Os gerentes de recursos precisam obter as configurações para determinar o comportamento do recurso.

   Na implementação de referência do Primetime, a configuração é armazenada em preferências compartilhadas, mas você pode armazenar a configuração de qualquer maneira que faça sentido para o seu ambiente.

* `MediaPlayer` é o objeto do reprodutor de mídia TVSDK que contém o recurso de vídeo.

   Os gerentes de recursos registram ouvintes de eventos TVSDK para esse objeto do reprodutor, recuperam dados da sessão de reprodução e acionam recursos TVSDK para a sessão de reprodução.

Cada recurso tem uma interface de configuração correspondente. Por exemplo, `CCManager` usa `ICCConfig` para recuperar a configuração. `ICCConfig` contém métodos para obter as informações de configuração relacionadas somente às legendas ocultas.

O exemplo a seguir mostra o arquivo [!DNL ICCConfig.java], configurado para receber informações sobre visibilidade de legenda fechada, estilo de fonte e borda de fonte do `MediaPlayer`:

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

Um aplicativo que usa um recurso TVSDK pode criar seu gerenciador de recursos com um provedor de configuração e um objeto `MediaPlayer` . Por exemplo:

```java
// This application needs to use the advertising workflow feature 
AdsManager adsManager = new AdsManagerOn();
```

Documentos da API de configuração do gerenciador de recursos: [Javadoc](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html)