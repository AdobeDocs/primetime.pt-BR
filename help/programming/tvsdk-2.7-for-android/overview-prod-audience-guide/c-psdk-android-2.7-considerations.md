---
description: Para usar o TVSDK de forma mais eficiente, considere alguns detalhes de sua operação e siga certas práticas recomendadas.
seo-description: Para usar o TVSDK de forma mais eficiente, considere alguns detalhes de sua operação e siga certas práticas recomendadas.
seo-title: Considerações e práticas recomendadas
title: Considerações e práticas recomendadas
uuid: 049da1f4-028b-49d2-9ebd-e5d9edcbaf8a
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Considerações e práticas recomendadas{#considerations-and-best-practices}

Para usar o TVSDK de forma mais eficiente, considere alguns detalhes de sua operação e siga certas práticas recomendadas.

## Considerações {#section_tvsdk_considerations}

Lembre-se das seguintes informações ao usar o TVSDK:

* A API TVSDK é implementada em Java.
* A Adobe Primetime não funciona atualmente em emuladores Android.

   Você deve usar dispositivos reais para teste.
* A reprodução é compatível somente com conteúdo HTTP Live Streaming (HLS).
* O conteúdo de vídeo principal pode ser multiplexado (fluxos de vídeo e áudio na mesma execução) ou não multiplexado (fluxos de vídeo e áudio em representações separadas).
* Atualmente, você precisa executar a maioria das operações da API TVSDK no thread da interface do usuário, que é o thread principal do Android.

   As operações executadas corretamente no thread principal podem gerar um erro e sair quando executadas em um thread em segundo plano.
* A reprodução de vídeo requer o Adobe Video Engine (AVE). Isso afeta como e quando os recursos de mídia podem ser acessados:

   * As legendas ocultas são suportadas na medida fornecida pelo AVE.
   * Dependendo da precisão do codificador, a duração real da mídia codificada pode diferir das durações que são registradas no manifesto do recurso de fluxo.

      Não há uma maneira confiável de ressincronizar entre a linha do tempo virtual ideal e a linha do tempo de reprodução real. O rastreamento de andamento da reprodução de fluxo para o gerenciamento de anúncios e o Video Analytics deve usar o tempo de reprodução real, de modo que o comportamento do relatórios e da interface do usuário pode não rastrear com precisão o conteúdo de mídia e anúncio.
   * O nome do agente de usuário recebido para todas as solicitações de mídia do TVSDK nesta plataforma recebe o seguinte padrão de string:

   ```
   "Adobe Primetime/" + 
   <varname>
   originalUserAgent
   </varname> 
   ```

   Todas as chamadas relacionadas a anúncios usam o agente de usuário padrão do Android ou o agente de usuário personalizado se você o definir ao configurar metadados de inserção de anúncios.

## Práticas recomendadas {#section_tvsdk_best_practices}

Estas são as práticas recomendadas para o TVSDK:

* Use a versão 3.0 ou superior do HLS para conteúdo de programas.
* Execute a maioria das operações TVSDK no thread principal (UI), não nos threads em segundo plano.
* Por padrão, para TVSDK 2.5 para Android, a resolução de anúncios ociosos está ativada.

   Para conteúdo sem precedente ou intermediário, você pode usar `AdvertisingMetadata.setPreroll(false)` para acelerar o carregamento do conteúdo.
