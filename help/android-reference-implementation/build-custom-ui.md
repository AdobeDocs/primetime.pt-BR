---
description: Você pode criar facilmente uma interface de usuário personalizada com base na estrutura de implementação de referência.
title: Criar uma interface de usuário personalizada
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Criar uma interface de usuário personalizada {#build-a-custom-user-interface}

Você pode criar uma interface de usuário personalizada com base na estrutura de implementação de referência.

Os componentes da interface do usuário dos seguintes recursos já estão integrados:

* Anúncios clicáveis
* Sobreposições de anúncio
* Áudio de ligação tardia
* Legendas ocultas
* Ouvintes de todos os componentes acima

1. Edite o arquivo [!DNL PlayerFragment.java] para inicializar os componentes da interface do usuário que deseja usar no player.

1. Edite o arquivo [!DNL res/player/player_fragment.xml] para personalizar a interface do usuário.
1. Crie o projeto.

>[!NOTE]
>
>Para fazer alterações na interface do usuário na barra de busca, você pode editar a classe MarkableSeekBar . A classe [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) manipula o controle deslizante, o polegar do controle deslizante, o marcador de anúncio, os marcadores de sinalização, o intervalo de buffer e os planos de fundo do intervalo de busca.