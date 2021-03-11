---
description: Você pode salvar a posição atual da reprodução em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.
title: Salve a posição do vídeo e retome mais tarde
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---


# Salve a posição do vídeo e retome mais tarde{#save-the-video-position-and-resume-later}

Você pode salvar a posição atual da reprodução em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.

As publicidades inseridas dinamicamente diferem entre sessões de usuário, portanto, salvar a posição **com** publicidades em spliced refere-se a uma posição diferente em uma sessão futura. O TVSDK fornece métodos para recuperar a posição da reprodução ao ignorar anúncios em spliced.

1. Quando o usuário sai de um vídeo, seu aplicativo recupera e salva a posição no vídeo.

   >[!TIP]
   >
   >As durações dos anúncios não são incluídas.

   As quebras de anúncios podem variar em cada sessão devido aos padrões de anúncios, limite de frequência e assim por diante. O horário atual do vídeo em uma sessão pode ser diferente em uma sessão futura. Ao salvar uma posição no vídeo, o aplicativo recupera a hora local . Use a propriedade `localTime` para ler essa posição , que pode ser salva no dispositivo ou em um banco de dados no servidor.

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   Por exemplo, se o usuário estiver no 20º minuto do vídeo e essa posição incluir cinco minutos de anúncios, `currentTime` terá `be` 1200 segundos, enquanto `localTime` nessa posição terá `be` 900 segundos.

1. Restaure a sessão do usuário quando a atividade do reprodutor for retomada.

   O TVSDK não reinicia a reprodução entre as inicializações do TVSDK porque não salva nenhuma informação localmente. O aplicativo deve implementar essa lógica.

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. Para retomar o vídeo na mesma posição:

   * Para retomar a reprodução do vídeo da posição que foi salva de uma sessão anterior, use `seekToLocal`.

      >[!TIP]
      >
      >Esse método é chamado somente com valores de hora locais. Se o método for chamado com os resultados de tempo atuais, ocorrerá um comportamento incorreto.

   * Para procurar no horário atual, use `seek`.

1. Quando o aplicativo recebe o evento de alteração de status `onStatusChanged`, procure no horário local salvo.
1. Forneça os ad breaks conforme especificado na interface da política de anúncios.
1. Implemente um seletor de política de anúncio personalizado estendendo o seletor de política de anúncio padrão.
1. Forneça os ad breaks que devem ser apresentados ao usuário implementando `selectAdBreaksToPlay`.

   Quando o reprodutor entra no status PREPARED , todos os anúncios já são resolvidos, portanto, a propriedade `AdPolicyInfo.adBreakTimelineItem` contém todas as quebras de anúncio antes da posição de hora local. Seu aplicativo pode decidir reproduzir um ad break precedente e retomar para o horário local especificado, reproduzir um ad break intermediário e retomar para o horário local especificado, ou não reproduzir ad breaks.
