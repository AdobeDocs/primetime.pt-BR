---
product: primetime
audience: end-user
user-guide-title: Ajuda de implementação de referência do Primetime
user-guide-description: Ajuda a entender o TVSDK e modificar os gerentes de recursos para personalizar seu reprodutor pessoal.
source-git-commit: 95626ebde981d1996652a67bc9e0cea05f24aa6d
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# PSDK 1.4 para implementação de referência do Android {#reference-implementation}

+ [Visão geral da implementação de referência do Android](home.md)
+ Implementação de referência do Primetime {#reference}
   + [Como usar a implementação de referência do Primetime](ref-implementation/how-to-use-ref-player.md)
   + [Estrutura de implementação de referência](ref-implementation/ref-player-structure.md)
   + Como usar gerenciadores de recursos {#feature-managers}
      + [Como usar gerenciadores de recursos](ref-implementation/using-feature-managers/how-to-use-feature-managers.md)
      + [Criando gerenciadores de recursos transmitindo informações de configuração ao MediaPlayer...](ref-implementation/using-feature-managers/creating-feature-managers.md)
      + [Ativando ou desativando recursos usando o ManagerFactory](ref-implementation/using-feature-managers/turning-features-on-off.md)
      + [Manipulação de eventos](ref-implementation/using-feature-managers/handling-events.md)
   + Configurar o ambiente de desenvolvimento {#setup-dev}
      + [Configurar o ambiente de desenvolvimento](set-up-dev-environment/set-up-dev-environment-overview.md)
      + [Faça o download e configure os softwares de pré-requisito](set-up-dev-environment/download-prereqs-android.md)
      + [Criar a implementação de referência do Primetime](set-up-dev-environment/install-the-ref-player-project.md)
   + Explorar o código {#explore-code}
      + [PlayerFragment](set-up-dev-environment/exploring-code/player-fragment.md)
      + [Gerenciadores de recursos](set-up-dev-environment/exploring-code/about-psdk-feature-managers.md)
      + [ConfigProvider](set-up-dev-environment/exploring-code/config-provider.md)
      + [SettingsActivity](set-up-dev-environment/exploring-code/settings-activity.md)
      + [Formato do catálogo](set-up-dev-environment/exploring-code/catalog-format.md)
      + [Objeto JSON para anúncios do Primetime](set-up-dev-environment/exploring-code/json-pt-ads.md)
      + [Objeto JSON para ad breaks diretos](set-up-dev-environment/exploring-code/json-direct-ad-breaks.md)
      + [Objeto JSON para marcadores de anúncios personalizados](set-up-dev-environment/exploring-code/json-custom-ad-markers.md)
      + [Objeto JSON para ID de recurso de direito](set-up-dev-environment/exploring-code/json-entitlement-resource-id.md)
      + [Exemplo de formato de feed JSON](set-up-dev-environment/exploring-code/example-json-feed-format.md)
   + Implementar reprodução de vídeo {#implement-video}
      + [Operações essenciais de reprodução de vídeo](implement-video-playback/video-playback.md)
      + [Ativar reprodução de vídeo](implement-video-playback/enable-video-playback.md)
      + [Proteção de conteúdo DRM](implement-video-playback/content-protection.md)
   + [Várias taxas de bits](implement-video-playback/mbr.md)
   + Configurar um reprodutor para reprodução de DVR com anúncios {#dvr}
      + [DVR sem inserção de anúncio](implement-video-playback/dvr/dvr-without-ad-insertion.md)
      + [DVR com inserção de anúncio](implement-video-playback/dvr/dvr-with-ad-insertion.md)
      + [Escolhendo um ponto de partida personalizado para DVR](implement-video-playback/dvr/dvr-custom-start-point.md)
      + [Definir uma hora de início personalizada na implementação de referência](implement-video-playback/dvr/set-custom-start-time-dvr.md)
   + [Exibir estatísticas de dispositivo e reprodução de QoS](implement-video-playback/qos-statistics.md)
   + Inserir anúncios {#insert-ads}
      + [Inserção de anúncio](insert-ads/ad-insertion.md)
      + [Tipos de inserção de anúncio](insert-ads/ad-insertion-types.md)
      + [Adicionar publicidade](insert-ads/add-advertising.md)
      + [Documentação da API relacionada](insert-ads/aps-callbacks-ad-insertion.md)
   + Áudio de associação tardia {#late-binding-audio}
      + [Visão geral](late-binding-audio/late-binding-audio-overview.md)
      + [Integrar áudio de ligação tardia](late-binding-audio/aa-enable.md)
      + [Selecionar as faixas de áudio](late-binding-audio/select-audio-tracks.md)
      + [Documentação da API relacionada](late-binding-audio/aa-api-callbacks.md)
   + Fluxos de direito de autenticação do Primetime {#primetime-authentications}
      + [Visão geral](paytvpass-entitlement/paytvpass-entitlement-overview.md)
      + [Visão geral do Gerenciador de direitos](paytvpass-entitlement/entitlement-overvivew.md)
      + [Integrar autenticação do Primetime](paytvpass-entitlement/integrate-pass.md)
      + [Configurar relatórios do Adobe Analytics](paytvpass-entitlement/pass-analytics-setup.md)
      + [Documentação da API relacionada](paytvpass-entitlement/pass-apis-callbacks.md)
   + Análise de vídeo {#video-analytics}
      + [Análise de vídeo](video-analytics/video-analytics-overview.md)
      + [Criar o Gerenciador de análise de vídeo](video-analytics/create-video-analytics-manager.md)
      + [Configurar análise de vídeo](video-analytics/configure-video-analytics-manager.md)
      + [Documentação da API relacionada](video-analytics/va-apis-callbacks.md)
   + [Criar uma interface de usuário personalizada](build-custom-ui.md)
   + [Solução de problemas](troubleshooting.md)
