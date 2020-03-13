---
seo-title: Configurar e executar as ferramentas de linha de comando
title: Configurar e executar as ferramentas de linha de comando
uuid: b65f8621-54fa-4927-b2f4-d2fd60350fc1
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Configurar e executar as ferramentas de linha de comando {#configure-and-run-the-command-line-tools}

As ferramentas de linha de comando têm propriedades associadas para as quais você deve definir valores definidos [!DNL flashaccesstools.properties] antes ** de executar as ferramentas. Algumas ferramentas de linha de comando também permitem especificar valores de propriedade da linha de comando. Os valores especificados na linha de comando têm prioridade sobre os valores fornecidos por você [!DNL flashaccesstools.properties].

É necessário modificar as configurações nas seguintes seções de [!DNL flashaccesstools.properties] para ativar as ferramentas de linha de comando correspondentes que você pretende usar:

* **Propriedades** do Media Packager - (para [!DNL AdobePackager.jar])

* **Propriedades** do Gerenciador de Lista de Atualização de Política e do Gerenciador de Lista de Revogação - (para [!DNL AdobePolicyUpdateListManager.jar] e [!DNL AdobeRevocationListManager.jar])

* **Propriedades** do Gerenciador de Políticas - (para [!DNL AdobePolicyManager.jar])

* **Propriedades** do gerador de licenças - (para [!DNL AdobeLicenseGenerator.jar])