---
description: Você pode criar facilmente uma interface de usuário personalizada com base na estrutura de implementação de referência.
title: Criar uma interface de usuário personalizada
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Criar uma interface de usuário personalizada {#build-a-custom-user-interface}

Você pode criar uma interface de usuário personalizada com base na estrutura de implementação de referência.

Os componentes da interface do usuário dos seguintes recursos já estão integrados:

* Anúncios clicáveis
* Sobreposições de anúncios
* Áudio de associação tardia
* Legendas ocultas
* Ouvintes de todos os componentes acima

1. Edite o [!DNL PlayerFragment.java] arquivo para inicializar os componentes da interface do usuário que você deseja usar no player.

1. Edite o [!DNL res/player/player_fragment.xml] arquivo para personalizar a interface do usuário.
1. Crie o projeto.

>[!NOTE]
>
>Para fazer alterações na interface do usuário na barra de busca, você pode editar a classe MarkableSeekBar. A variável [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) A classe manipula o controle deslizante, a miniatura do controle deslizante, o suporte do marcador de anúncio, os marcadores de sinalização, o intervalo de buffer e os planos de fundo do intervalo de busca.
