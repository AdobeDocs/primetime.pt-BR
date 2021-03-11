---
description: Você pode usar a API Objetive-C do Player do Primetime para personalizar o comportamento do reprodutor.
title: Classes do reprodutor de mídia
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Classes do reprodutor de mídia {#media-player-classes}

Você pode usar a API Objetive-C do Player do Primetime para personalizar o comportamento do reprodutor.

Essas classes descrevem o player de mídia e seus recursos.

| Classe | Descrição |
|---|---|
| PTABRControlParameters | Encapsula todos os parâmetros de controle de taxa de bits adaptáveis. Os parâmetros compatíveis são:<ul><li>minBitRate</li><li>maxBitRate</li><li>initialBitRate</li></ul> |
| PTDefaultMediaPlayerClientFactory | Implementação padrão de PTMediaPlayerClientFactoryno TVSDK. Ele fornece as instâncias disponíveis de PTOpportunityResolver, PTContentResolver e PTAdPolicySelector . |
| PTMediaPlayer | Define o componente raiz da estrutura do Primetime Player.Os aplicativos criam uma instância dessa classe para reproduzir uma mídia. Esse componente envia notificações para que o aplicativo saiba o status do reprodutor em um determinado momento. |
| PTMediaPlayerClientFactory | Protocolo que descreve os métodos que uma fábrica cliente do reprodutor de mídia personalizado deve implementar para fornecer as instâncias PTOpportunityResolver , PTContentResolver e PTAdPolicySelector disponíveis. |
| PTMediaPlayerItem | Representa uma mídia específica de áudio e vídeo. |
| PTMediaPlayerView | Gerencia o componente de exibição da estrutura do Player do Primetime. |
| PTMediaProfile | Representa o perfil de um único fluxo na lista de reprodução da variante. |
| PTMediaSelectionOption | Representa um recurso de mídia audiovisual para acomodar diferentes preferências de idioma, requisitos de acessibilidade ou configurações de aplicativo personalizadas. Tipos de opção válidos:<ul><li>Legendas (PTMediaSelectionOptionTypeSubtitle)</li><li>Áudio alternativo (PTMediaSelectionOptionTypeAudio)</li><li>Legendas ocultas (PTMediaSelectionOptionTypeCC)</li><li>Indefinido (PTMediaSelectionOptionTypeUndefined)</li></ul> |
| Classe PTOpportunityResolver,protocolo PTOpportunityResolver | Classe usada para processar dicas de manifesto que serão usadas como disposições para o processo de decisão do anúncio do Adobe Primetime. |
| PTOpportunityResolverDelegate | Protocolo que descreve os métodos que o resolvedor de oportunidade personalizado ( PTOpportunityResolver ) deve usar para comunicar ao delegado o status da resolução da oportunidade. |
| PTSDK | Descreve a versão do TVSDK e seus recursos. |
| PTSDKConfig | Expõe as configurações globais do TVSDK e permite que um aplicativo assine tags HLS personalizadas. |
| PTTextStyleRule | Define constantes que representam chaves de atributo de estilo de texto que formam o dicionário de regras. |
