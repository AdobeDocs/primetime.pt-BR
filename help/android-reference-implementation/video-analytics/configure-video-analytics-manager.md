---
description: Você pode rastrear o uso do vídeo na Implementação de referência do Android Primetime, configurando-o para funcionar com sua conta do Adobe Analytics.
title: Configurar o Video Analytics
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Configurar o Video Analytics {#configure-video-analytics}

Você pode rastrear o uso do vídeo na Implementação de referência do Android Primetime, configurando-o para funcionar com sua conta do Adobe Analytics. A implementação de referência do Android foi projetada para enviar dados de uso de vídeo e pulsação para o Adobe Analytics. Para ativar esse recurso, primeiro entre em contato com o representante da Adobe Primetime e crie uma conta da Adobe Analytics.

Há dois locais na Implementação de referência que você deve configurar para habilitar a integração com o Adobe Analytics. As configurações de tempo de execução do Video Analytics ocorrem depois que um novo vídeo é selecionado para reprodução (ou seja, depois que uma nova Atividade do Player é criada).

1. Configure as opções de tempo de carregamento no arquivo de ativos `ADBMobileConfig.json`.

   Esse arquivo é fornecido pelo representante de Adobe. Por padrão, ele não está incluído no pacote SDK do Primetime. Para obter mais informações sobre as configurações neste arquivo de configuração, consulte o Guia do Programador do Android aqui: Inicialize e configure a análise de vídeo.
1. Configure as opções de tempo de execução no menu Configurações de implementação de referência

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | Opções de tempo de execução | Descrição |
   |---|---|
   | Servidor de rastreamento do Video Analytics | URL do ponto final da coleção de back-end da análise de vídeo. É aqui que todas as chamadas de rastreamento de pulsação de vídeo são enviadas. |
   | ID da tarefa | O identificador de trabalho de processamento. Isso indica ao endpoint de back-end qual tipo de processamento aplicar para as chamadas de rastreamento de vídeo. |
   | Canal | O nome do canal no qual o usuário está assistindo ao conteúdo. Para um aplicativo móvel, esse é normalmente o nome do aplicativo. |
   | Editor | O nome do publicador de conteúdo |
   | Registro de depuração | Ativa o logon extenso. Desabilitado por padrão, isso pode afetar o desempenho quando ativado, de modo que você desabilita isso para um ambiente de produção. |
   | Modo silencioso | Quando ativado, nenhuma chamada de rede é feita, portanto, isso seria útil para depuração local, mas deve ser desativado para um ambiente de produção. |