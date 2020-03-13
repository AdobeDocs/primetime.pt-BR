---
description: Baixar vídeo e áudio em paralelo, em vez de em uma série, reduz os atrasos na inicialização.
seo-description: Baixar vídeo e áudio em paralelo, em vez de em uma série, reduz os atrasos na inicialização.
seo-title: Downloads paralelos
title: Downloads paralelos
uuid: 11d37a39-391d-4127-9aa7-c94eb8a6a6a8
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Downloads paralelos {#parallel-downloads}

Baixar vídeo e áudio em paralelo, em vez de em uma série, reduz os atrasos na inicialização.

Downloads paralelos permitem que arquivos VOD (Video-on-demand) sejam reproduzidos, otimizam o uso da largura de banda disponível em um servidor, diminuem a probabilidade de entrar em situações de buffer sem execução e minimizam o atraso entre o download e a reprodução.

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

Sem downloads paralelos, o TVSDK emite uma solicitação para o segmento de vídeo e, depois que o segmento de vídeo é carregado, solicita um ou dois segmentos de áudio. Com downloads paralelos, os segmentos de áudio e vídeo são baixados simultaneamente, e não sequencialmente. Além disso, como há duas conexões e duas solicitações HTTP por segmento em paralelo, os dados chegam à tela mais rápido.

>[!NOTE]
>
>Este recurso se aplica somente ao conteúdo em que o áudio e o vídeo são codificados em arquivos diferentes (conteúdo sem mudo) e não se aplica ao conteúdo MP4, que é sempre mudo. O conteúdo HLS geralmente não é mudo, especialmente com áudio alternativo.

<!-- 

See comment above (DASH use case removed).
<note type="restriction">
  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
</note>

 -->

A conexão HTTP pode sofrer atrasos nos seguintes estágios:

* Ao estabelecer a conexão TCP/IP com o servidor

   Embora o cliente e o servidor tenham concordado em se comunicar, ainda não ocorreu nenhuma comunicação HTTP. Esse tipo de atraso depende da infraestrutura entre o cliente e o servidor. Esse processo requer encontrar um caminho pela Internet entre o cliente e o servidor e garantir que todos os dispositivos, como roteadores e firewalls, na rota concordem com a transferência de dados.
* Ao enviar uma solicitação HTTP para um segmento ou um manifesto pela conexão TCP/IP.

   O servidor recebe a solicitação, processa-a e começa a enviar os dados de volta ao cliente. O grau de atraso depende da carga e da complexidade do software no servidor e, de alguma forma, da velocidade de carregamento da conexão quando o cliente envia a solicitação.