---
description: Você pode implementar uma barra de controle com suporte a DVR para VOD e transmissão ao vivo. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.
title: Construir uma barra de controle aprimorada para DVR
exl-id: e4846f1e-bc57-452b-b393-8f8f55434e7a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Construir uma barra de controle aprimorada para DVR{#construct-a-control-bar-enhanced-for-dvr}

Você pode implementar uma barra de controle com suporte a DVR para VOD e transmissão ao vivo. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.

* Para VOD, o comprimento da janela pesquisável é a duração do ativo inteiro.
* Para transmissão ao vivo, o comprimento da janela DVR (pesquisável) é definido como o intervalo de tempo que começa na janela de reprodução ao vivo e termina no ponto de vida do cliente.

   O ponto ativo do cliente é calculado subtraindo o comprimento do buffer do final da janela ativa. A duração alvo é um valor maior ou igual à duração máxima de um fragmento no manifesto.

   A barra de controle para reprodução ao vivo suporta DVR, posicionando primeiro o polegar no ponto ao vivo do cliente ao iniciar a reprodução e exibindo uma região que marca a área onde a busca não é permitida.

Para uma barra de controle:

1. Adicione uma sobreposição à barra de controle que representa o intervalo de reprodução.

1. Quando o usuário começar a busca, verifique se a posição de busca desejada está dentro do intervalo pesquisável.
