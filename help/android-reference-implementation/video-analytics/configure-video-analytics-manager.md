---
description: Você pode rastrear o uso do vídeo na Implementação de referência do Android do Primetime configurando-a para funcionar com sua conta da Adobe Analytics.
title: Configurar análise de vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Configurar análise de vídeo {#configure-video-analytics}

Você pode rastrear o uso do vídeo na Implementação de referência do Android do Primetime configurando-a para funcionar com sua conta da Adobe Analytics. A implementação de referência do Android foi projetada para enviar dados de uso e heartbeat de vídeo para o Adobe Analytics. Para ativar esse recurso, primeiro entre em contato com o representante da Adobe Primetime e crie uma conta do Adobe Analytics.

Há dois lugares na Implementação de referência que você deve configurar para habilitar a integração com o Adobe Analytics. As configurações de tempo de execução da Análise de vídeo entram em vigor assim que um novo vídeo é selecionado para reprodução (ou seja, assim que uma nova Atividade de player é criada).

1. Configurar as opções de tempo de carregamento no `ADBMobileConfig.json` arquivo de ativos.

   Esse arquivo é fornecido pelo representante da Adobe. Por padrão, ele não está incluído no pacote de SDK do Primetime. Para obter mais informações sobre as configurações neste arquivo de configuração, consulte o Guia do programador do Android aqui: Inicializar e configurar a análise de vídeo.
1. Configurar opções de tempo de execução no menu Configurações de implementação de referência

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | Opções de tempo de execução | Descrição |
   |---|---|
   | Servidor de rastreamento do Video Analytics | URL do ponto de extremidade da coleção de back-end da análise de vídeo. Aqui, todas as chamadas de rastreamento de heartbeat de vídeo são enviadas. |
   | ID da tarefa | O identificador do trabalho de processamento. Isso indica ao endpoint de back-end que tipo de processamento deve ser aplicado às chamadas de rastreamento de vídeo. |
   | Canal | O nome do canal no qual o usuário está assistindo ao conteúdo. Para um aplicativo móvel, geralmente esse é o nome do aplicativo. |
   | Editor | O nome do publicador do conteúdo |
   | Registro de depuração | Ativa o registro extensivo. Desativado por padrão, isso pode afetar o desempenho quando ativado, de modo que você desativa isso para um ambiente de produção. |
   | Modo Silencioso | Quando habilitado, nenhuma chamada de rede é feita, portanto, isso seria útil para a depuração local, mas deve ser desabilitado para um ambiente de produção. |
