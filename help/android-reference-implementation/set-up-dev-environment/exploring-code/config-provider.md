---
description: A classe ConfigProvider obtém a configuração do reprodutor de mídia. Você deve implementar a interface de configuração para que os gerentes de recursos possam ler as informações de configuração.
title: ConfigProvider
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# ConfigProvider {#configprovider}

A classe ConfigProvider obtém a configuração do reprodutor de mídia. Você deve implementar a interface de configuração para que os gerentes de recursos possam ler as informações de configuração.

Você usa a classe [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) para implementar as interfaces de configuração `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig` e `IQosConfig` para que os gerentes de recursos possam ler as configurações. Por exemplo, `ICCConfig` é a interface da configuração `CCManager`. Os arquivos de configuração recebem os parâmetros de configuração do arquivo de configuração JSON.

O arquivo &lt;a0/ é um exemplo de implementação Adobe das interfaces de configuração. `ConfigProvider.java` Ele lê as configurações de `SharedPreferences`, onde a configuração é armazenada. Você pode armazenar sua configuração de qualquer maneira que funcione para sua organização. A implementação da configuração fornece um wrapper para sua fonte de configuração.