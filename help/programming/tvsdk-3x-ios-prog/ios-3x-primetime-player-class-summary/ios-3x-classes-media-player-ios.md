---
description: Você pode usar a API Objetive-C do reprodutor Primetime para personalizar o comportamento do reprodutor.
title: Classes do reprodutor de mídia
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Classes do reprodutor de mídia {#media-player-classes}

Você pode usar a API Objetive-C do reprodutor Primetime para personalizar o comportamento do reprodutor.

Essas classes descrevem o reprodutor de mídia e seus recursos.

| Classe | Descrição |
|---|---|
| PTABRControlParameters | Encapsula todos os parâmetros de controle de taxa de bits adaptáveis. Os parâmetros compatíveis são:<ul><li>minBitRate</li><li>maxBitRate</li><li>taxaDeBitsInicial</li></ul> |
| PTDefaultMediaPlayerClientFactory | Implementação padrão de PTMediaPlayerClientFactoryno TVSDK. Ele fornece as instâncias disponíveis PTOpportunityResolver, PTContentResolver e PTAdPolicySelector. |
| PTMediaPlayer | Define o componente raiz da estrutura do Primetime Player. Os aplicativos criam uma ocorrência dessa classe para reproduzir uma mídia. Esse componente envia notificações para informar ao aplicativo o status do reprodutor a qualquer momento. |
| PTMediaPlayerClientFactory | Protocolo que descreve os métodos que uma fábrica de clientes de reprodutor de mídia personalizado deve implementar para fornecer as instâncias PTOpportunityResolver, PTContentResolver e PTAdPolicySelector disponíveis. |
| PTMediaPlayerItem | Representa uma mídia de áudio e vídeo específica. |
| ExibiçãoDoPlayerDeMídiaPTM | Gerencia o componente de exibição da estrutura do Primetime Player. |
| PTMediaProfile | Representa o perfil de um único fluxo na lista de reprodução de variantes. |
| PTMediaSelectionOption | Representa um recurso de mídia audiovisual para acomodar diferentes preferências de idioma, requisitos de acessibilidade ou configurações de aplicativo personalizadas. Tipos de opção válidos:<ul><li>Legendas (PTMediaSelectionOptionTypeSubtitle)</li><li>Áudio alternativo (PTMediaSelectionOptionTypeAudio)</li><li>Legendas codificadas (PTMediaSelectionOptionTypeCC)</li><li>Indefinido (PTMediaSelectionOptionTypeUndefined)</li></ul> |
| classe PTOpportunityResolver,protocolo PTOpportunityResolver | Classe usada para processar indicações no manifesto que serão usadas como disposições para o processo de decisão de anúncios do Adobe Primetime. |
| PTOpportunityResolverDelegate | Protocolo que descreve os métodos que o resolvedor de oportunidades personalizado ( PTOpportunityResolver ) deve usar para comunicar ao delegado o status da resolução da oportunidade. |
| PTSDK | Descreve a versão do TVSDK e seus recursos. |
| PTSDKConfig | Expõe as configurações globais do TVSDK e permite que um aplicativo assine tags HLS personalizadas. |
| PTTextStyleRule | Define as constantes que representam as chaves de atributo de estilo de texto que formam o dicionário de regras. |
