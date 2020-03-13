---
description: Você pode criar facilmente uma interface de usuário personalizada com base na estrutura de implementação de referência.
seo-description: Você pode criar facilmente uma interface de usuário personalizada com base na estrutura de implementação de referência.
seo-title: Criar uma interface de usuário personalizada
title: Criar uma interface de usuário personalizada
uuid: b785f6a4-3ef8-4f7a-a087-0d6551da9750
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Criar uma interface de usuário personalizada {#build-a-custom-user-interface}

Você pode criar uma interface de usuário personalizada com base na estrutura de implementação de referência.

Os componentes da interface do usuário dos seguintes recursos já estão integrados:

* Anúncios clicáveis
* Sobreposições de anúncio
* Áudio de ligação tardia
* Legendas ocultas
* Ouvintes para todos os componentes acima

1. Edite o [!DNL PlayerFragment.java] arquivo para inicializar os componentes da interface que você deseja usar no player.

1. Edite o [!DNL res/player/player_fragment.xml] arquivo para personalizar a interface do usuário.
1. Construa o projeto.

>[!NOTE]
>
>Para fazer alterações na interface da barra de busca, edite a classe MarkableSeekBar. A classe [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) lida com o controle deslizante, o polegar do controle deslizante, o marcador do anúncio, os marcadores de sinalização, o intervalo de buffer e os planos de fundo do intervalo de busca.