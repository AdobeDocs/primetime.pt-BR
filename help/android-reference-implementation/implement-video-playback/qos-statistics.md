---
description: Você pode configurar seu reprodutor para ler estatísticas de reprodução e do dispositivo do QoSProvider sempre que necessário.
title: Exibir estatísticas de dispositivo e reprodução de QoS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Exibir estatísticas de dispositivo e reprodução de QoS {#display-qos-playback-and-device-statistics}

Você pode configurar seu reprodutor para ler estatísticas de reprodução e do dispositivo do QoSProvider sempre que necessário.

A variável `QoSProvider` A classe fornece várias estatísticas, incluindo a taxa de quadros, a taxa de bits do perfil, o tempo total gasto no buffering, o número de tentativas de buffering, o tempo necessário para obter o primeiro byte do primeiro fragmento de vídeo, o tempo necessário para renderizar o primeiro quadro, o tamanho do buffer no momento e o tempo de buffer.

A implementação de referência fornece uma `QoSManager` onde você pode habilitar a exibição da sobreposição de QoS. Você também pode ativar a visibilidade de QoS na interface do usuário de Configurações:

![](assets/qos-configuration.jpg)

A variável `QoSManager` O rastreia estatísticas de QoS obtendo informações do dispositivo, anexando ao reprodutor de mídia e atualizando com as informações de QoS mais recentes.

**Ativar ou desativar o relatório de estatísticas de QoS**

1. Crie um QosManager ou ative o relatório de QoS usando o ManagerFactory.

   * Para criar um QosManager:
      * Este aplicativo precisa usar o recurso de fluxo de trabalho de publicidade

   QoSManager qosManager = new QosManagerOn();

   * Para usar um ManagerFactory para habilitar a exibição de estatísticas de QoS:

   qosManager = ManagerFactory.getQosManager(
   <b>true</b>, config, mediaPlayer);

   >[!NOTE]
   >
   >Alteração de booleano para `false` desativa o relatório de QoS.

2. Adicionar ouvintes de eventos:

   `qosManager.addEventListener(qosManagerEventListener);`

3. Crie o provedor de QoS e anexe-o ao contexto de atividade do player:

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >Quando a atividade do reprodutor for destruída, chame [qosManager.destroyQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) para limpar o provedor de QOS desanexando-o do reprodutor de mídia.

**Documentação da API relacionada**

* [Classe QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [Classe QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
