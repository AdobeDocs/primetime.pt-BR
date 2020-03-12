---
description: Você pode salvar a posição de reprodução atual em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.
seo-description: Você pode salvar a posição de reprodução atual em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.
seo-title: Salve a posição do vídeo e retome mais tarde
title: Salve a posição do vídeo e retome mais tarde
uuid: 03ed5c63-008d-4dd1-9a31-baefa73b56e2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Salve a posição do vídeo e retome mais tarde{#save-the-video-position-and-resume-later}

Você pode salvar a posição de reprodução atual em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.

As publicidades inseridas dinamicamente diferem entre as sessões do usuário, portanto, salvar a posição **com** publicidades em spliced refere-se a uma posição diferente em uma sessão futura. O TVSDK fornece métodos para recuperar a posição de reprodução ao ignorar anúncios segmentados.

1. Quando o usuário sai de um vídeo, seu aplicativo recupera e salva a posição no vídeo.

   >[!TIP]
   >
   >A duração do anúncio não está incluída.

   As quebras de anúncios podem variar em cada sessão devido aos padrões de anúncios, limitação de frequência e assim por diante. A hora atual do vídeo em uma sessão pode ser diferente em uma sessão futura. Ao salvar uma posição no vídeo, o aplicativo recupera a hora local. Use a `localTime` propriedade para ler essa posição, que pode ser salva no dispositivo ou em um banco de dados no servidor.

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   Por exemplo, se o usuário estiver no 20º minuto do vídeo, e essa posição incluir cinco minutos de anúncios, `currentTime` fará `be` 1200 segundos, enquanto `localTime` nessa posição serão `be` 900 segundos.

1. Restaure a sessão do usuário quando a atividade do player for retomada.

   O TVSDK não reinicia a reprodução entre inicializações do TVSDK porque não salva nenhuma informação localmente. Seu aplicativo deve implementar essa lógica.

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. Para retomar o vídeo na mesma posição:

   * Para retomar a reprodução do vídeo da posição que foi salva de uma sessão anterior, use `seekToLocal`.

      >[!TIP]
      >
      >Esse método é chamado somente com valores de hora locais. Se o método for chamado com os resultados de tempo atuais, ocorrerá comportamento incorreto.

   * Para buscar o horário atual, use `seek`.

1. Quando o aplicativo receber o evento de alteração de `onStatusChanged` status, procure a hora local salva.
1. Forneça os intervalos de anúncio conforme especificado na interface da política de anúncios.
1. Implemente um seletor de política de publicidade personalizado estendendo o seletor de política de publicidade padrão.
1. Forneça as pausas de anúncio que devem ser apresentadas ao usuário por meio da implementação `selectAdBreaksToPlay`.

   Quando o player entra no status PREPARADO, todos os anúncios já são resolvidos, portanto, a `AdPolicyInfo.adBreakTimelineItem` propriedade contém todas as quebras de anúncio antes da posição da hora local. Seu aplicativo pode decidir reproduzir um intervalo de anúncios precedente e retomar para o horário local especificado, reproduzir um intervalo de anúncios intermediário e retomar para o horário local especificado, ou não reproduzir nenhum intervalo de anúncios.
