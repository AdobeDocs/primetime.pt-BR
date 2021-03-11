---
description: Baixar vídeo e áudio em paralelo, em vez de em uma série, reduz os atrasos na inicialização.
title: Downloads paralelos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Downloads paralelos {#parallel-downloads}

Baixar vídeo e áudio em paralelo, em vez de em uma série, reduz os atrasos na inicialização.

Downloads paralelos permitem a reprodução de arquivos de vídeo sob demanda (VOD), otimiza o uso da largura de banda disponível em um servidor, diminui a probabilidade de entrar em situações de buffer sob execução e minimiza o atraso entre o download e a reprodução.

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

Sem downloads paralelos, o TVSDK emite uma solicitação para o segmento de vídeo e, depois que ele é carregado, solicita um ou dois segmentos de áudio. Com downloads paralelos, os segmentos de áudio e vídeo são baixados simultaneamente, não sequencialmente. Além disso, como há duas conexões e duas solicitações HTTP por segmento em paralelo, os dados chegam à tela mais rápido.

>[!NOTE]
>
>Esse recurso aplica-se somente a conteúdo em que o áudio e o vídeo são codificados em arquivos diferentes (conteúdo sem mudo) e não se aplica ao conteúdo MP4, que é sempre mudado. O conteúdo HLS geralmente não é mudado, especialmente com áudio alternativo.

<!-- 

See comment above (DASH use case removed).

  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

A conexão HTTP pode sofrer atrasos nos seguintes estágios:

* Ao estabelecer a conexão TCP/IP com o servidor

   Embora o cliente e o servidor tenham concordado em se comunicar, nenhuma comunicação HTTP ainda ocorreu. Esse tipo de atraso depende da infraestrutura entre o cliente e o servidor. Esse processo requer encontrar um caminho pela Internet entre o cliente e o servidor e garantir que todos os dispositivos, como roteadores e firewalls, na rota concordem com a transferência de dados.
* Ao enviar uma solicitação HTTP para um segmento ou um manifesto sobre a conexão TCP/IP.

   O servidor recebe a solicitação, a processa e começa a enviar os dados de volta ao cliente. O grau de atraso depende da carga e da complexidade do software no servidor e, de certa forma, da velocidade de carregamento da conexão quando o cliente envia a solicitação.