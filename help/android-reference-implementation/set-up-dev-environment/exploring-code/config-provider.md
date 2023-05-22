---
description: A classe ConfigProvider obtém a configuração do reprodutor de mídia. Você deve implementar a interface de configuração para que os gerenciadores de recursos possam ler as informações de configuração.
title: ConfigProvider
exl-id: 75613bfb-3c2b-4b53-b365-adc98f7e1164
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# ConfigProvider {#configprovider}

A classe ConfigProvider obtém a configuração do reprodutor de mídia. Você deve implementar a interface de configuração para que os gerenciadores de recursos possam ler as informações de configuração.

Você usa o [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) classe para implementar o `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig`, e `IQosConfig` para que os gerenciadores de recursos possam ler as configurações. Por exemplo, a variável `ICCConfig` é a interface para o `CCManager` configuração. Os arquivos de configuração recebem os parâmetros de configuração do arquivo de configuração JSON.

A variável `ConfigProvider.java` file é um exemplo de implementação Adobe das interfaces de configuração. Ele lê as configurações de `SharedPreferences`, onde a configuração é armazenada. Você pode armazenar a configuração de qualquer maneira que funcione para sua organização. A implementação da configuração fornece um wrapper para sua fonte de configuração.
