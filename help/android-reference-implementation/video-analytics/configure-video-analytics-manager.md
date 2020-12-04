---
description: É possível rastrear o uso de vídeo na Implementação de referência do Android Primetime configurando-o para funcionar com sua conta do Adobe Analytics.
seo-description: É possível rastrear o uso de vídeo na Implementação de referência do Android Primetime configurando-o para funcionar com sua conta do Adobe Analytics.
seo-title: Configurar análise de vídeo
title: Configurar análise de vídeo
uuid: ce2ebab3-b3c8-472a-9c54-16ddb1c3cc4e
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# Configurar o Video Analytics {#configure-video-analytics}

É possível rastrear o uso de vídeo na Implementação de referência do Android Primetime configurando-o para funcionar com sua conta do Adobe Analytics. A Implementação de referência do Android foi projetada para enviar dados de uso e pulsação de vídeo para a Adobe Analytics. Para ativar esse recurso, primeiro entre em contato com seu representante da Adobe Primetime e crie uma conta da Adobe Analytics.

Há dois locais na Implementação de referência que você deve configurar para habilitar a integração com o Adobe Analytics. As configurações de tempo de execução do Video Analytics ocorrem assim que um novo vídeo é selecionado para reprodução (ou seja, assim que uma nova PlayerActivity é criada).

1. Configure as opções de tempo de carregamento no arquivo de ativos `ADBMobileConfig.json`.

   Esse arquivo é fornecido pelo representante do Adobe. Por padrão, ele não está incluído no pacote SDK do Primetime. Para obter mais informações sobre as configurações neste arquivo de configuração, consulte o Guia do Programador do Android aqui: Inicialize e configure a análise de vídeo.
1. Configure as opções de tempo de execução no menu de configurações de Implementação de referência

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | Opções de tempo de execução | Descrição |
   |---|---|
   | Servidor de rastreamento do Video Analytics | URL do ponto final da coleção de back-end de análise de vídeo. É aqui que todas as chamadas de rastreamento de pulsação de vídeo são enviadas. |
   | ID do trabalho | O identificador da tarefa de processamento. Isso indica ao endpoint de back-end que tipo de processamento aplicar às chamadas de rastreamento de vídeo. |
   | Canal | O nome do canal no qual o usuário está assistindo ao conteúdo. Para um aplicativo móvel, esse é geralmente o nome do aplicativo. |
   | Editor | O nome do editor de conteúdo |
   | Registro de depuração | Ativa o registro em log extenso. Desativado por padrão, isso pode afetar o desempenho quando ativado, de modo que você desabilite isso para um ambiente de produção. |
   | Modo silencioso | Quando ativado, nenhuma chamada de rede é feita, portanto isso seria útil para a depuração local, mas deve ser desativado para um ambiente de produção. |