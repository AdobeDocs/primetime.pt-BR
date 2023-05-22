---
description: Os objetos MediaPlayerNotification fornecem informações sobre alterações no estado do player, avisos e erros. Erros que interrompem a reprodução do vídeo também causam uma alteração no estado do reprodutor.
title: Conteúdo da notificação
exl-id: b8298865-0389-4610-b495-b8735ef9cd56
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Conteúdo da notificação {#notification-content}

Os objetos MediaPlayerNotification fornecem informações sobre alterações no estado do player, avisos e erros. Erros que interrompem a reprodução do vídeo também causam uma alteração no estado do reprodutor.

Seu aplicativo pode recuperar as informações de notificação e estado. Você também pode criar um sistema de registro para diagnóstico e validação usando as informações de notificação.

Você implementa ouvintes de eventos para capturar e responder a eventos. Muitos eventos fornecem `MediaPlayerNotification` notificações de status.

`MediaPlayerNotification` O fornece informações relacionadas ao status do reprodutor.

O TVSDK fornece uma lista cronológica de `MediaPlayerNotification` notificações. Cada notificação contém as seguintes informações:

* Carimbo de data/hora
* Metadados de diagnóstico que consistem nos seguintes elementos:

   * `type`: INFORMAÇÕES, AVISO ou ERRO.
   * `code`: uma representação numérica da notificação.
   * `name`: uma descrição legível da notificação, como SEEK_ERROR
   * `metadata`: Pares de chave/valor que contêm informações relevantes sobre a notificação. Por exemplo, uma chave chamada `URL` O fornece um valor que é um URL relacionado à notificação.

   * `innerNotification`: Uma referência a outra `MediaPlayerNotification` objeto que afeta diretamente esta notificação.

Você pode armazenar essas informações localmente para análise posterior ou enviá-las a um servidor remoto para registro e representação gráfica.

## Configurar seu sistema de notificação {#set-up-your-notification-system}

Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações.

O núcleo do sistema de notificação do Primetime Player é o `Notification` classe, que representa uma notificação independente.

A variável `NotificationHistory` A classe fornece um mecanismo para acumular notificações. Ele armazena um log de objetos de notificação (NotificationHistoryItem) que representa uma coleção de Notificações.

Para receber notificações:

* Acompanhar notificações
* Adicionar notificações ao histórico de notificações

1. Analise as alterações de estado.
1. Implementar o `MediaPlayer.PlaybackEventListener.onStateChanged` retorno de chamada.
1. O TVSDK passa dois parâmetros para o retorno de chamada:

   * O novo estado ( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` objeto

## Adicionar depuração e registro em tempo real {#add-real-time-logging-and-debugging}

Você pode usar as notificações para implementar o registro em tempo real no aplicativo de vídeo.

O sistema de notificação permite coletar informações de registro e depuração para diagnóstico e validação sem sobrecarregar o sistema.

>[!IMPORTANT]
>
>O back-end de registro não faz parte de uma configuração de produção e não é esperado que manipule o tráfego de carga alta. Se a implementação não precisar estar totalmente completa, considere a eficiência da transmissão de dados para evitar sobrecarga do sistema.

Este é um exemplo de como recuperar notificações.

1. Crie um thread de execução baseado em cronômetro para seu aplicativo de vídeo que consulte periodicamente os dados coletados pelo sistema de notificação TVSDK.

1. Se o intervalo do cronômetro for muito grande e o tamanho da lista de eventos for muito pequeno, a lista de eventos de notificação estourará. Para evitar esse excesso, siga um destes procedimentos:

   * Diminuir o intervalo de tempo que orienta o thread que pesquisa novos eventos.
   * Aumente o tamanho da lista de notificações.

1. Serialize as entradas de evento de notificação mais recentes no formato JSON e envie as entradas para um servidor remoto para pós-processamento.

   O servidor remoto poderia exibir graficamente os dados fornecidos em tempo real.
1. Para detectar a perda de eventos de notificação, procure por lacunas na sequência de valores de índice de evento.

   Cada evento de notificação tem um valor de índice que é incrementado automaticamente pelo `session.NotificationHistory` classe.

## Tags ID3 {#id-tags}

As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O TVSDK detecta tags ID3 no nível de segmento de fluxo de transporte (TS) em fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag.

>[!IMPORTANT]
>
>O TVSDK reconhece metadados ID3 (versão 2.3.0 ou 2.4.0) em fluxos de áudio (AAC) e vídeo (H.264), em qualquer uma de suas possíveis codificações (ASCII, UTF8, UTF16-BE ou UTF16-LE). Ele ignora tags ID3 que não estão em uma das versões ou formatos reconhecidos. A codificação não especificada é tratada como UTF8.

Quando o TVSDK detecta metadados de ID3, ele emite uma notificação com os seguintes dados:

* InfoCode = 303007
* TIPO = ID3
* NAME = ausente
* ID = 0

1. Implementar um ouvinte de eventos para `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` e registre-o com o `MediaPlayer` objeto.

   O TVSDK chama esse ouvinte quando detecta metadados de ID3.

   >[!NOTE]
   >
   >As dicas de anúncios personalizados usam o mesmo `onTimedMetadata` para indicar a detecção de uma nova tag. Isso não deve causar confusão, pois dicas de anúncios personalizados são detectadas no nível do manifesto e tags ID3 são incorporadas no fluxo. Para obter mais informações, consulte custom-tags-configure.

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
