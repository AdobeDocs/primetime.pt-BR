---
description: Você pode configurar seu player para ler as estatísticas de reprodução e dispositivo do QoSProvider sempre que necessário.
seo-description: Você pode configurar seu player para ler as estatísticas de reprodução e dispositivo do QoSProvider sempre que necessário.
seo-title: Exibir estatísticas de reprodução e dispositivo de QoS
title: Exibir estatísticas de reprodução e dispositivo de QoS
uuid: 8fc45a2f-03d4-4fa0-979b-eb816419c4f7
translation-type: tm+mt
source-git-commit: e1c6ab1d50f9262aaf70aef34854cf293fb4f30d
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Exibir estatísticas de reprodução e dispositivo de QoS {#display-qos-playback-and-device-statistics}

Você pode configurar seu player para ler as estatísticas de reprodução e dispositivo do QoSProvider sempre que necessário.

A `QoSProvider` classe fornece várias estatísticas, incluindo a taxa de quadros, a taxa de bits do perfil, o tempo total gasto no buffering, o número de tentativas de buffering, o tempo necessário para obter o primeiro byte do primeiro fragmento de vídeo, o tempo necessário para renderizar o primeiro quadro, a duração do buffer no momento e o tempo do buffer.

A implementação de referência fornece uma `QoSManager` classe na qual você pode ativar a exibição da sobreposição de QoS. Você também pode ativar a visibilidade de QoS na interface do usuário de Configurações:

![](assets/qos-configuration.jpg)

O `QoSManager` rastreia as estatísticas de QoS obtendo informações do dispositivo, anexando-as ao player de mídia e atualizando-as com as últimas informações de QoS.

**Ativar ou desativar o relatórios de estatísticas de QoS**

1. Crie um QosManager ou ative o relatórios QoS usando o ManagerFactory.

   * Para criar um QosManager:
      * Este aplicativo precisa usar o recurso de fluxo de trabalho de publicidade

   QoSManager qosManager = new QosManagerOn();

   * Para usar um ManagerFactory para ativar a exibição de estatísticas de QoS:

   qosManager = ManagerFactory.getQosManager(
   <b>true</b>, config, mediaPlayer);

   >[!NOTE]
   >
   >Alterar o booliano para `false` desativa o relatórios QoS.

2. Adicionar ouvintes de evento:

   `qosManager.addEventListener(qosManagerEventListener);`

3. Crie o provedor QoS e anexe-o ao contexto de atividade do player:

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >Quando a atividade do player for destruída, certifique-se de chamar [qosManager.structQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) para limpar o provedor QOS, desconectando-o do player de mídia.

**Documentação da API relacionada**

* [Classe QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [Classe QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
