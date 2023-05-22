---
description: O download de vídeo e áudio em paralelo, em vez de em série, reduz os atrasos de inicialização.
title: Downloads paralelos
exl-id: 7cc9afbf-e495-40b0-a8ff-86d4939d1b15
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Downloads paralelos {#parallel-downloads}

O download de vídeo e áudio em paralelo, em vez de em série, reduz os atrasos de inicialização.

Os downloads paralelos permitem a reprodução de arquivos de vídeo sob demanda (VOD), otimizam o uso da largura de banda disponível de um servidor, reduzem a probabilidade de entrar em situações de buffer sem execução e minimizam o atraso entre o download e a reprodução.

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

Sem downloads paralelos, o TVSDK emite uma solicitação para o segmento de vídeo e, após o segmento de vídeo ser carregado, solicita um ou dois segmentos de áudio. Com downloads paralelos, os segmentos de áudio e vídeo são baixados simultaneamente, não sequencialmente. Além disso, como há duas conexões e duas solicitações HTTP por segmento em paralelo, os dados chegam à tela mais rapidamente.

>[!NOTE]
>
>Esse recurso se aplica somente ao conteúdo em que o áudio e o vídeo são codificados em arquivos diferentes (conteúdo não-muxed) e não se aplica ao conteúdo MP4, que é sempre muxed. O conteúdo HLS geralmente é desmarcado, especialmente com áudio alternativo.

<!-- 

See comment above (DASH use case removed).

  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

A conexão HTTP pode enfrentar atrasos nos seguintes estágios:

* Ao estabelecer a conexão TCP/IP com o servidor

   Embora o cliente e o servidor tenham concordado em se comunicar, nenhuma comunicação HTTP ocorreu ainda. Esse tipo de atraso depende da infraestrutura entre o cliente e o servidor. Esse processo requer encontrar um caminho pela Internet entre o cliente e o servidor e garantir que todos os dispositivos, como roteadores e firewalls, na rota estejam de acordo com a transferência de dados.
* Ao enviar uma solicitação HTTP para um segmento ou um manifesto pela conexão TCP/IP.

   O servidor recebe a solicitação, processa e começa a enviar os dados de volta para o cliente. O grau de atraso depende da carga e da complexidade do software no servidor e, de certa forma, da velocidade da conexão de upload quando o cliente envia a solicitação.
