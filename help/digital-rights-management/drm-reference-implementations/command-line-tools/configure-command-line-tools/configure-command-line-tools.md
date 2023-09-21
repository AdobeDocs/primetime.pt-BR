---
title: Configurar e executar as ferramentas de linha de comando
description: Configurar e executar as ferramentas de linha de comando
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Configurar e executar as ferramentas de linha de comando {#configure-and-run-the-command-line-tools}

As ferramentas de linha de comando têm propriedades associadas para as quais você deve definir valores em [!DNL flashaccesstools.properties] *antes* você executa as ferramentas. Algumas das ferramentas de linha de comando também permitem especificar valores de propriedade a partir da linha de comando. Os valores especificados na linha de comando têm prioridade sobre os valores fornecidos pelo [!DNL flashaccesstools.properties].

Você deve modificar as configurações nas seguintes seções de [!DNL flashaccesstools.properties] para ativar as ferramentas de linha de comando correspondentes que você pretende usar:

* **Propriedades do Media Packager** - (para [!DNL AdobePackager.jar])

* **Propriedades do Gerenciador de Listas de Atualização de Políticas e do Gerenciador de Listas de Revogação** - (para [!DNL AdobePolicyUpdateListManager.jar] e [!DNL AdobeRevocationListManager.jar])

* **Propriedades do Policy Manager** - (para [!DNL AdobePolicyManager.jar])

* **Propriedades do Gerador de Licenças** - (para [!DNL AdobeLicenseGenerator.jar])
