---
seo-title: Configurar e executar as ferramentas de linha de comando
title: Configurar e executar as ferramentas de linha de comando
uuid: b65f8621-54fa-4927-b2f4-d2fd60350fc1
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# Configure e execute as ferramentas de linha de comando {#configure-and-run-the-command-line-tools}

As ferramentas de linha de comando têm propriedades associadas para as quais você deve definir valores definidos em [!DNL flashaccesstools.properties] *antes de* executar as ferramentas. Algumas ferramentas de linha de comando também permitem especificar valores de propriedade da linha de comando. Os valores especificados na linha de comando têm prioridade sobre os valores fornecidos de [!DNL flashaccesstools.properties].

É necessário modificar as configurações nas seguintes seções de [!DNL flashaccesstools.properties] para ativar as ferramentas de linha de comando correspondentes que você pretende usar:

* **Propriedades**  do Media Packager - (para  [!DNL AdobePackager.jar])

* **Propriedades**  do Gerenciador de Listas e do Gerenciador de Listas de Revogação de Atualização de Política - (para  [!DNL AdobePolicyUpdateListManager.jar] e  [!DNL AdobeRevocationListManager.jar])

* **Propriedades**  do Gerenciador de Políticas - (para  [!DNL AdobePolicyManager.jar])

* **Propriedades**  do gerador de licenças - (para  [!DNL AdobeLicenseGenerator.jar])