---
description: O TVSDK pode reproduzir vídeos que têm vários perfis com diferentes taxas de bits, alternando entre eles para fornecer mais de um nível de qualidade com base na largura de banda disponível.
seo-description: O TVSDK pode reproduzir vídeos que têm vários perfis com diferentes taxas de bits, alternando entre eles para fornecer mais de um nível de qualidade com base na largura de banda disponível.
seo-title: Taxas de vários bits
title: Taxas de vários bits
uuid: 46eac41e-0b2a-42e3-8a88-54ad9fe34212
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---


# Taxas de bits múltiplas {#multiple-bit-rates}

O TVSDK pode reproduzir vídeos que têm vários perfis com diferentes taxas de bits, alternando entre eles para fornecer mais de um nível de qualidade com base na largura de banda disponível.

Você pode definir taxas de bits iniciais, mínimas e máximas, bem como a política de switch de taxa de bits adaptável (ABR) para um fluxo de taxa de bits múltipla (MBR). O TVSDK muda automaticamente para a taxa de bits que fornece a melhor experiência de reprodução dentro da configuração especificada.

A implementação de referência configura os seguintes parâmetros ABR em [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html).

| Parâmetro | Descrição |
|--- |--- |
| Taxa de bits inicial:  getABRInitialBitRate | A taxa de bits de reprodução desejada (em bits por segundo) para o primeiro segmento. Quando os start de reprodução, o perfil mais próximo (igual ou maior à taxa de bits inicial) é usado para o primeiro segmento.  Se uma taxa de bits mínima for definida e a taxa de bits inicial for inferior à mínima, o TVSDK selecionará o perfil com a taxa de bits mais baixa acima da taxa de bits mínima. Da mesma forma, se a taxa inicial estiver acima da taxa máxima, o TVSDK selecionará a taxa mais alta abaixo do máximo. Se a taxa de bits inicial for zero ou indefinida, a taxa de bits inicial será determinada pela política ABR.  Retorna um valor inteiro que representa o perfil byte por segundo. |
| Taxa mínima de bits:  getABRMinBitRate | A menor taxa de bits permitida para a qual o ABR pode alternar. A alternância ABR ignora perfis com uma taxa de bits inferior a essa. Retorna um valor inteiro que representa o perfil bits por segundo. |
| Taxa máxima de bits:  getABRMaxBitRate | A maior taxa de bits permitida para a qual o ABR pode alternar. A comutação ABR ignora perfis com uma taxa de bits superior a essa. Retorna um valor inteiro que representa o perfil bits por segundo. |
| Política de comutação ABR:  getABRPolicy | A reprodução alterna gradualmente para o perfil da taxa de bits mais alta quando possível. Você pode definir a política para a alternância ABR, que determina a velocidade de alternância do TVSDK entre perfis. O padrão é Moderado. <ul><li>*Conservador*: Alterna para o perfil com a próxima taxa de bits mais alta quando a largura de banda for 50% mais alta do que a taxa de bits atual. </li><li>*Moderado*: Alterna para o próximo perfil de taxa de bits mais alta quando a largura de banda for 20% mais alta do que a taxa de bits atual.</li><li>*Agressivo*: Alterna imediatamente para o perfil de taxa de bits mais alta quando a largura de banda for maior que a taxa de bits atual</li></ul><br/>Se a taxa de bits inicial for zero ou não especificada e uma política for especificada, start de reprodução com o perfil de taxa de bits mais baixo para Conservador, o perfil mais próximo da taxa de bits mediana dos perfis disponíveis para Moderado e o perfil de taxa de bits mais alto para Agressivo.<br/><br/>A política funciona dentro das restrições das taxas de bits mínimas e máximas, se elas forem especificadas.  Retorna a configuração atual da enumeração ABRControlParameters: <ul><li>ABR_CONSERVATIVE</li><li>ABR_MODERATE </li><li>ABR_AGRESSIVE</li></ul><br>Consulte também  [ABRPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html). |

>[!NOTE]
>
>* O mecanismo de failover TVSDK pode substituir essas configurações, pois o TVSDK favorece uma experiência de reprodução contínua em vez de respeitar rigorosamente os parâmetros de controle.
>* Quando a taxa de bits muda, o TVSDK despacha os eventos `onProfileChanged` em `PlaybackEventListener`.


## Habilitar controle ABR personalizado na implementação de referência {#section_72A6E7263E1441DD8D7E0690285515E6}

A taxa de bits adaptável (ABR) é ativada no TVSDK por padrão. Você pode usar a interface do usuário Configurações do Primetime para substituir o comportamento padrão do TVSDK na implementação de referência, configurando o controle ABR personalizado.

Para ativar o ABR personalizado por meio da interface do usuário de Configurações:

* Abra a caixa de diálogo Configurações do Primetime.
* Selecione **[!UICONTROL ABR controls]**.

   ![](assets/abr-configuration.jpg)

* Toque no controle [!UICONTROL Enable ON] para exibir `OFF`.

O `PlaybackManager` só define os parâmetros ABR se [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) retornar true (ON). Se retornar false (OFF), `PlaybackManager` usará o controle ABR padrão, de modo que as taxas de bits inicial, mínima e máxima serão todas 0 e a política ABR será `ABR_MODERATE`.

## Configurar para taxas de bits baixas {#section_5451691CBBD24542AD54A474D222CD39}

Para algumas taxas de reprodução de baixa taxa de bits, o TVSDK, por padrão, alterna para o fluxo somente de áudio e a reprodução parece congelada. Você pode configurar o player para que ele nunca encontre uma situação em que ele alterne para somente áudio.

* Implemente a interface [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html):

* Certifique-se de que [getABRMinBitRate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate()) seja superior à taxa de bits somente de áudio (superior a 64000).
* Verifique se [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled()) está ativado.