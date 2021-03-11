---
title: Configurar e executar as ferramentas de linha de comando
description: Configurar e executar as ferramentas de linha de comando
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# Configure e execute as ferramentas de linha de comando {#configure-and-run-the-command-line-tools}

As ferramentas de linha de comando têm propriedades associadas para as quais você deve definir valores em [!DNL flashaccesstools.properties] *antes de* executar as ferramentas. Algumas das ferramentas de linha de comando também permitem especificar valores de propriedade a partir da linha de comando. Os valores especificados na linha de comando têm prioridade sobre os valores fornecidos a partir de [!DNL flashaccesstools.properties].

Você deve modificar as configurações nas seguintes seções de [!DNL flashaccesstools.properties] para ativar as ferramentas de linha de comando correspondentes que pretende usar:

* **Propriedades**  do Media Packager - (para  [!DNL AdobePackager.jar])

* **Propriedades**  do Gerenciador de Lista de Atualizações de Política e do Gerenciador de Lista de Revogação - (para  [!DNL AdobePolicyUpdateListManager.jar] e  [!DNL AdobeRevocationListManager.jar])

* **Propriedades**  do Gerenciador de Políticas - (para  [!DNL AdobePolicyManager.jar])

* **Propriedades**  do Gerador de Licenças - (para  [!DNL AdobeLicenseGenerator.jar])