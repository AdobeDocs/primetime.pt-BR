---
description: O TVSDK pode reproduzir vídeos com vários perfis com taxas de bits diferentes, alternando entre eles para fornecer mais de um nível de qualidade com base na largura de banda disponível.
title: Várias taxas de bits
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# Várias taxas de bits {#multiple-bit-rates}

O TVSDK pode reproduzir vídeos com vários perfis com taxas de bits diferentes, alternando entre eles para fornecer mais de um nível de qualidade com base na largura de banda disponível.

Você pode definir taxas de bits iniciais, mínimas e máximas, bem como a política de switch ABR (adaptive bit-rate) para um fluxo MBR (multiple bit rate). O TVSDK alterna automaticamente para a taxa de bits que fornece a melhor experiência de reprodução na configuração especificada.

A implementação de referência configura os seguintes parâmetros ABR no [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html).

| Parâmetro | Descrição |
|--- |--- |
| Taxa de bits inicial: getABRInitialBitRate | A taxa de bits de reprodução desejada (em bits por segundo) para o primeiro segmento. Quando a reprodução começa, o perfil mais próximo (igual ou maior que a taxa de bits inicial) é usado para o primeiro segmento.  Se uma taxa de bits mínima for definida e a taxa de bits inicial for menor que o mínimo, o TVSDK selecionará o perfil com a taxa de bits mais baixa acima da taxa de bits mínima. Da mesma forma, se a taxa inicial estiver acima da taxa máxima, o TVSDK selecionará a taxa mais alta abaixo do máximo. Se a taxa de bits inicial for zero ou indefinida, a taxa de bits inicial será determinada pela política ABR.  Retorna um valor inteiro que representa o perfil de byte por segundo. |
| Taxa de bits mínima: getABRMinBitRate | A taxa de bits mais baixa permitida para a qual o ABR pode alternar. A switching ABR ignora perfis com uma taxa de bits inferior a esta. Retorna um valor inteiro que representa o perfil de bits por segundo. |
| Taxa de bits máxima: getABRMaxBitRate | A taxa de bits mais alta permitida para a qual o ABR pode alternar. A switching ABR ignora perfis com uma taxa de bits superior a esta. Retorna um valor inteiro que representa o perfil de bits por segundo. |
| Política de switching ABR: getABRPolicy | A reprodução alterna gradualmente para o perfil de taxa de bits mais alta quando possível. Você pode definir a política de switching ABR, que determina a rapidez com que o TVSDK alterna entre perfis. O padrão é Moderado. <ul><li>*Conservador*: Alterna para o perfil com a próxima taxa de bits mais alta quando a largura de banda for 50% mais alta do que a taxa de bits atual. </li><li>*Moderado*: Alterna para o próximo perfil de taxa de bits mais alta quando a largura de banda for 20% mais alta do que a taxa de bits atual.</li><li>*Agressivo*: Alterna imediatamente para o perfil de taxa de bits mais alta quando a largura de banda for maior que a taxa de bits atual</li></ul><br/>Se a taxa de bits inicial for zero ou não for especificada e uma política for especificada, a reprodução começará com o perfil de taxa de bits mais baixo para Conservador, o perfil mais próximo da taxa de bits mediana dos perfis disponíveis para Moderado e o perfil de taxa de bits mais alto para Agressivo.<br/><br/>A política funciona dentro das restrições das taxas de bits mínima e máxima, se elas forem especificadas.  Retorna a configuração atual do enum ABRControlParameters: <ul><li>ABR_CONSERVATIVE</li><li>ABR_MODERATE </li><li>ABR_AGRESSIVO</li></ul><br>Consulte também [ABRPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html). |

>[!NOTE]
>
>* O mecanismo de failover do TVSDK pode substituir essas configurações, pois o TVSDK favorece uma experiência de reprodução contínua em vez de respeitar estritamente os parâmetros de controle.
>* Quando a taxa de bits muda, o TVSDK envia `onProfileChanged` eventos em `PlaybackEventListener`.

## Habilitação do controle ABR personalizado na implementação de referência {#section_72A6E7263E1441DD8D7E0690285515E6}

Por padrão, a taxa de bits adaptável (ABR) está ativada no TVSDK. Você pode usar a interface do usuário de Configurações do Primetime para substituir o comportamento padrão do TVSDK na implementação de referência, configurando o controle ABR personalizado.

Para habilitar o ABR personalizado por meio da interface do usuário de Configurações:

* Abra a caixa de diálogo Configurações do Primetime.
* Selecionar **[!UICONTROL ABR controls]**.

  ![](assets/abr-configuration.jpg)

* Toque no [!UICONTROL Enable ON] para que seja exibido `OFF`.

A variável `PlaybackManager` define os parâmetros ABR somente se [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) retorna verdadeiro (ON). Se retornar false (OFF), a variável `PlaybackManager` O usa o controle ABR padrão de modo que as taxas de bits inicial, mínima e máxima sejam 0 e a política ABR seja `ABR_MODERATE`.

## Configurar para taxas de bits baixas {#section_5451691CBBD24542AD54A474D222CD39}

Para algumas taxas de reprodução de baixa taxa de bits, o TVSDK, por padrão, alterna para o fluxo somente de áudio e a reprodução parece congelada. Você pode configurar o reprodutor para que ele nunca encontre uma situação em que ele alterne para somente áudio.

* Implementar o [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) interface:

* Assegure que [getABRMinBitRate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate()) é maior que a taxa de bits somente de áudio (maior que 64000).
* Assegure que [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled()) está ativado.
