---
description: Você pode usar a API Objetive-C do Player Primetime para personalizar o comportamento do player.
seo-description: Você pode usar a API Objetive-C do Player Primetime para personalizar o comportamento do player.
seo-title: Classes do Media Player
title: Classes do Media Player
uuid: 705c71b6-4e5e-46b5-a59d-13df977b04f2
translation-type: tm+mt
source-git-commit: b13f2d3f083a6ca333a4edba1c8d7261f7d448ad

---


# Classes do Media Player {#media-player-classes}

Você pode usar a API Objetive-C do Player Primetime para personalizar o comportamento do player.

Essas classes descrevem seu media player e seus recursos.

| Classe | Descrição |
|---|---|
| PTABRControlParameters | Encapsula todos os parâmetros adaptáveis de controle de taxa de bits. Os parâmetros suportados são:<ul><li>minBitRate</li><li>maxBitRate</li><li>initialBitRate</li></ul> |
| PTDefaultMediaPlayerClientFactory | Implementação padrão de PTMediaPlayerClientFactoryno TVSDK. Fornece as instâncias disponíveisPTOpportunityResolver, PTContentResolver e PTAdPolicySelector. |
| PTMediaPlayer | Define o componente raiz da estrutura do Primetime Player.Os aplicativos criam uma instância dessa classe para reproduzir uma mídia. Este componente envia notificações para permitir que seu aplicativo saiba o status do player a qualquer momento. |
| PTMediaPlayerClientFactory | Protocolo que descreve os métodos que uma fábrica cliente de player de mídia personalizada deve implementar para fornecer as instâncias PTOpportunityResolver, PTContentResolver e PTAdPolicySelector disponíveis. |
| PTMediaPlayerItem | Representa uma mídia de áudio e vídeo específica. |
| PTMediaPlayerView | Gerencia o componente de visualização da estrutura do Primetime Player. |
| PTMediaProfile | Representa o perfil de um único fluxo na lista de reprodução variante. |
| PTMediaSelectionOption | Representa um recurso de mídia audiovisual para acomodar diferentes preferências de idioma, requisitos de acessibilidade ou configurações de aplicativo personalizadas. Tipos de opção válidos:<ul><li>Legendas (PTMediaSelectionOptionTypeSubtitle)</li><li>Áudio alternativo (PTMediaSelectionOptionTypeAudio)</li><li>Legendas ocultas (PTMediaSelectionOptionTypeCC)</li><li>Indefinido (PTMediaSelectionOptionTypeUndefined)</li></ul> |
| classe PTOpportunityResolver,protocolo PTOpportunityResolver | Classe usada para processar dicas no manifesto que serão usadas como disposições para o processo de decisão do anúncio do Adobe Primetime. |
| PTOpportunityResolverDelegate | Protocolo que descreve os métodos que o resolvedor de oportunidade personalizado ( PTOpportunityResolver ) deve usar para comunicar ao delegado o status da resolução da oportunidade. |
| PTSDK | Descreve a versão do TVSDK e seus recursos. |
| PTSDKConfig | Expõe as configurações globais do TVSDK e permite que um aplicativo assine tags HLS personalizadas. |
| PTTextStyleRule | Define constantes que representam chaves de atributo de estilo de texto que formam o dicionário de regras. |
