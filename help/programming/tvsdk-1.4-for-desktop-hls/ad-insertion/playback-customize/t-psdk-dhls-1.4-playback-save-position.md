---
description: Você pode salvar a posição de reprodução atual em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.
title: Salvar a posição do vídeo e retomar mais tarde
exl-id: a06897a6-bf57-4902-b1b4-e931419b56ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Salvar a posição do vídeo e retomar mais tarde{#save-the-video-position-and-resume-later}

Você pode salvar a posição de reprodução atual em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.

Os anúncios inseridos dinamicamente diferem entre as sessões do usuário, portanto, salvar a posição **com** anúncios em spliced refere-se a uma posição diferente em uma sessão futura. O TVSDK fornece métodos para recuperar a posição de reprodução, ignorando anúncios empacotados.

1. Quando o usuário sai de um vídeo, o aplicativo recupera e salva a posição no vídeo.

   >[!TIP]
   >
   >A duração do anúncio não está incluída.

   Os ad breaks podem variar em cada sessão devido a padrões de anúncios, limite de frequência e assim por diante. A hora atual do vídeo em uma sessão pode ser diferente em uma sessão futura. Ao salvar uma posição no vídeo, o aplicativo recupera a hora local . Use o `localTime` para ler esta posição, que pode ser salva no dispositivo ou em um banco de dados no servidor.

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   Por exemplo, se o usuário estiver no 20º minuto do vídeo e essa posição incluir cinco minutos de anúncios, `currentTime` irá `be` 1200 segundos, enquanto `localTime` nesta posição `be` 900 segundos.

1. Restaure a sessão do usuário quando a atividade do player for retomada.

   O TVSDK não retoma a reprodução entre inicializações do TVSDK porque não salva informações localmente. Seu aplicativo deve implementar essa lógica.

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. Para retomar o vídeo na mesma posição:

   * Para retomar a reprodução do vídeo a partir da posição salva em uma sessão anterior, use `seekToLocal`.

      >[!TIP]
      >
      >Esse método é chamado somente com valores de hora locais. Se o método for chamado com os resultados da hora atual, ocorrerá um comportamento incorreto.

   * Para buscar o horário atual, use `seek`.

1. Quando o aplicativo recebe a variável `onStatusChanged` evento de alteração de status, procure a hora local salva.
1. Forneça os ad breaks de acordo com as especificações da interface de política de anúncios.
1. Implemente um seletor de política de anúncios personalizado estendendo o seletor de política de anúncios padrão.
1. Fornecer os ad breaks que devem ser apresentados ao usuário implementando `selectAdBreaksToPlay`.

   Quando o reprodutor entrar no status PREPARADO, todos os anúncios já estarão resolvidos, portanto, o `AdPolicyInfo.adBreakTimelineItem` A propriedade contém todos os ad breaks antes da posição da hora local. Seu aplicativo pode decidir reproduzir um ad break precedente e retomar o horário local especificado, reproduzir um ad break intermediário e retomar o horário local especificado ou não reproduzir ad breaks.
