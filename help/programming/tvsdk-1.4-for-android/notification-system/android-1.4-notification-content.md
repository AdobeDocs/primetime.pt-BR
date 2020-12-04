---
description: Os objetos MediaPlayerNotification fornecem informações sobre alterações no estado do player, avisos e erros. Erros que param a reprodução do vídeo também causam uma alteração no estado do player.
seo-description: Os objetos MediaPlayerNotification fornecem informações sobre alterações no estado do player, avisos e erros. Erros que param a reprodução do vídeo também causam uma alteração no estado do player.
seo-title: Conteúdo da notificação
title: Conteúdo da notificação
uuid: 89fb8f63-b0d5-45cd-bdad-348529fd07d0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---


# Conteúdo de notificação {#notification-content}

Os objetos MediaPlayerNotification fornecem informações sobre alterações no estado do player, avisos e erros. Erros que param a reprodução do vídeo também causam uma alteração no estado do player.

Seu aplicativo pode recuperar a notificação e as informações de estado. Você também pode criar um sistema de registro para diagnóstico e validação usando as informações de notificação.

Você implementa ouvintes de eventos para capturar e responder a eventos. Muitos eventos fornecem notificações de status `MediaPlayerNotification`.

`MediaPlayerNotification` fornece informações relacionadas ao status do player.

O TVSDK fornece uma lista cronológica de `MediaPlayerNotification` notificações. Cada notificação contém as seguintes informações:

* Carimbo de data e hora
* Metadados de diagnóstico que consistem nos seguintes elementos:

   * `type`: INFO, AVISO ou ERRO.
   * `code`: Uma representação numérica da notificação.
   * `name`: Uma descrição legível pela pessoa da notificação, como SEEK_ERROR
   * `metadata`: Pares chave/valor que contêm informações relevantes sobre a notificação. Por exemplo, uma chave chamada `URL` fornece um valor que é um URL relacionado à notificação.

   * `innerNotification`: Uma referência a outro  `MediaPlayerNotification` objeto que afeta diretamente essa notificação.

Você pode armazenar essas informações localmente para análise posterior ou enviá-las para um servidor remoto para registro e representação gráfica.

## Configure seu sistema de notificação {#set-up-your-notification-system}

Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações.

O núcleo do sistema de notificação do Primetime Player é a classe `Notification`, que representa uma notificação independente.

A classe `NotificationHistory` fornece um mecanismo para acumular notificações. Ele armazena um log de objetos de notificação (NotificationHistoryItem) que representa uma coleção de Notificações.

Para receber notificações:

* Escutar notificações
* Adicionar notificações ao histórico de notificações

1. Analise as mudanças de estado.
1. Implemente o retorno de chamada `MediaPlayer.PlaybackEventListener.onStateChanged`.
1. O TVSDK passa dois parâmetros para o retorno de chamada:

   * O novo estado ( `MediaPlayer.PlayerState`)
   * Um objeto `MediaPlayerNotification`

## Adicionar registro e depuração em tempo real {#add-real-time-logging-and-debugging}

Você pode usar notificações para implementar o logon em tempo real no aplicativo de vídeo.

O sistema de notificação permite coletar informações de registro e depuração para diagnóstico e validação sem estressar excessivamente o sistema.

>[!IMPORTANT]
>
>O back-end de logon não faz parte de uma configuração de produção e não é esperado que trate de tráfego de alta carga. Se sua implementação não precisar ser totalmente concluída, considere a eficiência da transmissão de dados para evitar sobrecarregar seu sistema.

Este é um exemplo de como recuperar notificações.

1. Crie um thread de execução com base em temporizador para seu aplicativo de vídeo que query periodicamente os dados coletados pelo sistema de notificação TVSDK.

1. Se o intervalo do temporizador for muito grande e o tamanho da lista do evento for muito pequeno, a lista do evento de notificação estourará. Para evitar esse sobrefluxo, execute um dos procedimentos a seguir:

   * Diminua o intervalo de tempo que direciona o thread que pesquisa novos eventos.
   * Aumente o tamanho da lista de notificação.

1. Serialize as entradas mais recentes do evento de notificação no formato JSON e envie as entradas para um servidor remoto para pós-processamento.

   O servidor remoto poderia então exibir graficamente os dados fornecidos em tempo real.
1. Para detectar a perda de eventos de notificação, procure por lacunas na sequência de valores de índice de evento.

   Cada evento de notificação tem um valor de índice que é incrementado automaticamente pela classe `session.NotificationHistory`.

## Tags ID3 {#id-tags}

As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O TVSDK detecta tags ID3 no nível do segmento de fluxo de transporte (TS) nos fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag .

>[!IMPORTANT]
>
>O TVSDK reconhece os metadados ID3 (versão 2.3.0 ou 2.4.0) nos fluxos de áudio (AAC) e vídeo (H.264), em qualquer uma de suas possíveis codificações (ASCII, UTF8, UTF16-BE ou UTF16-LE). Ele ignora as tags ID3 que não estão em nenhuma das versões ou formatos reconhecidos. A codificação não especificada é tratada como UTF8.

Quando o TVSDK detecta os metadados ID3, ele emite uma notificação com os seguintes dados:

* InfoCode = 303007
* TYPE = ID3
* NAME = não presente
* ID = 0

1. Implemente um ouvinte de evento para `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` e registre-o com o objeto `MediaPlayer`.

   O TVSDK chama esse ouvinte quando detecta metadados ID3.

   >[!NOTE]
   >
   >As dicas de anúncio personalizadas usam o mesmo evento `onTimedMetadata` para indicar a detecção de uma nova tag. Isso não deve causar confusão, pois as dicas de anúncio personalizadas são detectadas no nível do manifesto e as tags ID3 são incorporadas no fluxo. Para obter mais informações, consulte custom-tags-configure .

1. Recupere os metadados.

   ```java
   @Override 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               String value = metadata.getValue(key); 
           } 
       } 
   }
   ```
