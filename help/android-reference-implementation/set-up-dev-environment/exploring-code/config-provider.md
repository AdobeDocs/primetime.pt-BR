---
description: A classe ConfigProvider obtém a configuração do player de mídia. Você deve implementar a interface de configuração para que os gerentes de recursos possam ler as informações de configuração.
seo-description: A classe ConfigProvider obtém a configuração do player de mídia. Você deve implementar a interface de configuração para que os gerentes de recursos possam ler as informações de configuração.
seo-title: ConfigProvider
title: ConfigProvider
uuid: 2467a617-6413-4b5d-9710-894cdc751b26
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# ConfigProvider {#configprovider}

A classe ConfigProvider obtém a configuração do player de mídia. Você deve implementar a interface de configuração para que os gerentes de recursos possam ler as informações de configuração.

Use a classe [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) para implementar as interfaces de configuração `ICCConfig`, `IAAConfig`, `IPlaybackConfig`e `IAdConfig``IQosConfig` , para que os gerentes de recursos possam ler as configurações. Por exemplo, a interface `ICCConfig` é a interface da `CCManager` configuração. Os arquivos de configuração recebem os parâmetros de configuração do arquivo de configuração JSON.

O `ConfigProvider.java` arquivo é um exemplo da implementação da Adobe das interfaces de configuração. Ele lê as configurações de `SharedPreferences`, onde a configuração é armazenada. Você pode armazenar sua configuração de qualquer maneira que funcione para sua organização. A implementação da configuração fornece um invólucro para a sua fonte de configuração.