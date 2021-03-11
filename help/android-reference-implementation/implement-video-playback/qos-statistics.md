---
description: Você pode configurar seu reprodutor para ler as estatísticas de reprodução e dispositivo do QoSProvider sempre que necessário.
title: Exibir estatísticas de reprodução e dispositivo de QoS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# Exibir a reprodução de QoS e as estatísticas do dispositivo {#display-qos-playback-and-device-statistics}

Você pode configurar seu reprodutor para ler as estatísticas de reprodução e dispositivo do QoSProvider sempre que necessário.

A classe `QoSProvider` fornece várias estatísticas, incluindo a taxa de quadros, a taxa de bits do perfil, o tempo total gasto no buffering, o número de tentativas de buffering, o tempo necessário para obter o primeiro byte do primeiro fragmento de vídeo, o tempo necessário para renderizar o primeiro quadro, a duração do buffer no momento e o tempo do buffer.

A implementação de referência fornece uma classe `QoSManager` onde você pode ativar a exibição da sobreposição de QoS. Você também pode ativar a visibilidade do QoS na interface do usuário das Configurações:

![](assets/qos-configuration.jpg)

O `QoSManager` rastreia as estatísticas de QoS obtendo informações do dispositivo, anexando ao reprodutor de mídia e atualizando com as informações de QoS mais recentes.

**Ativar ou desativar o relatório de estatísticas de QoS**

1. Crie um QosManager ou ative o relatório de QoS usando o ManagerFactory.

   * Para criar um QosManager:
      * Este aplicativo precisa usar o recurso de fluxo de trabalho de publicidade

   QoSManager qosManager = new QosManagerOn();

   * Para usar um ManagerFactory para ativar a exibição das estatísticas de QoS:

   qosManager = ManagerFactory.getQosManager(
   <b>true</b>, config, mediaPlayer);

   >[!NOTE]
   >
   >Alterar o booleano para `false` desativa os relatórios de QoS.

2. Adicionar ouvintes de eventos:

   `qosManager.addEventListener(qosManagerEventListener);`

3. Crie o provedor QoS e o anexe ao contexto da atividade do reprodutor:

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >Quando a atividade do reprodutor for destruída, certifique-se de chamar [qosManager.destroyQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) para limpar o provedor QOS desconectando-o do reprodutor de mídia.

**Documentação da API relacionada**

* [Classe QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [Classe QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
