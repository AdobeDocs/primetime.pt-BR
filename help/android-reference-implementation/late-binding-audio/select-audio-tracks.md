---
title: Selecionar as faixas de áudio
description: Selecionar as faixas de áudio
copied-description: true
exl-id: d4a7260a-82dd-4b57-8037-b91815d9b954
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# Selecionar as faixas de áudio{#select-the-audio-tracks}

Para selecionar faixas de áudio para áudio de associação tardia, implemente [IAAConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IAAConfig.html).

| Para... | Chamar... |
|---|---|
| Obter uma lista de faixas do AA disponíveis | [getAudioTracks()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/AAManager.html#getAudioTracks()) |
| Obter a faixa selecionada no momento | [getSelectedAudioTrack()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/AAManager.html#getSelectedAudioTrack()) |
| Selecionar uma faixa do AA | [selectAlternateAudioTrack()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/AAManager.html#selectAlternateAudioTrack(int)) |

O código de amostra a seguir ilustra como a implementação de referência obtém as faixas de áudio do TVSDK e atribui a faixa selecionada ao item de mídia associado:

```java
/** 
 * Displays a chooser dialog, allowing the user to select the desired 
 * alternate audio track. 
 */ 
private void displayAlternateAudioDialog() { 
    PrimetimeReference.logger.i(LOG_TAG + "#selectAlternateAudio", 
      "Displaying alternate audio chooser dialog."); 
    final int selectedAlternateAudio = aaManager.getSelectedAudioTrackIndex(); 
    if (selectedAlternateAudio != AAManagerOn.INVALID_AUDIO_TRACK) { 
        final String items[] = aaManager.getAudioTracks(); 
        new AlertDialog.Builder(getActivity()) 
          .setTitle(R.string.PlayerControlAADialogTitle) 
          .setSingleChoiceItems(items, selectedAlternateAudio, 
          new DialogInterface.OnClickListener() { 
              public void onClick(DialogInterface dialog, int whichButton) { 
                  boolean result =  
                    aaManager.selectAlternateAudioTrack(whichButton); 
                  if (result) { 
                      PrimetimeReference.logger.i(LOG_TAG 
                                                  + "#selectAlternateAudio", 
                                                  "Audio track selection successful"); 
                  } else { 
                      PrimetimeReference.logger.i(LOG_TAG 
                                            + "#selectAlternateAudio", 
                                            "Audio track selection failed"); 
                  } 
                  // Dismiss dialog. 
                  dialog.cancel(); 
              } 
          }).setNegativeButton(R.string.PlayerControlCCDialogCancel, 
                               new DialogInterface.OnClickListener() { 
              public void onClick(DialogInterface dialog, 
                                    int whichButton) { 
                                // Just cancel the dialog. 
              } 
          }).show(); 
 
    } else { 
        PrimetimeReference.logger.i(LOG_TAG + "#selectAlternateAudioFailed", 
                "Unable to detect the currently selected audio track."); 
        Toast.makeText(getActivity(), 
                "Unable to detect the currently selected audio track", 
                Toast.LENGTH_SHORT).show(); 
    } 
} 
```
