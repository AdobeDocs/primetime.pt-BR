---
description: É possível implementar uma barra de controle com suporte a DVR para VOD e transmissão ao vivo. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.
title: Construa uma barra de controle aprimorada para DVR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# Construa uma barra de controle aprimorada para DVR{#construct-a-control-bar-enhanced-for-dvr}

É possível implementar uma barra de controle com suporte a DVR para VOD e transmissão ao vivo. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.

* Para VOD, o comprimento da janela que pode ser buscada é a duração do ativo inteiro.
* Para transmissão ao vivo, o comprimento da janela DVR (pesquisável) é definido como o intervalo de tempo que começa na janela de reprodução ao vivo e termina no ponto ativo do cliente.

   O ponto ativo do cliente é calculado subtraindo o comprimento do buffer do final da janela ativa. A duração do target é um valor maior ou igual à duração máxima de um fragmento no manifesto.

   A barra de controle da reprodução ao vivo oferece suporte a DVR, posicionando primeiro o polegar no ponto de entrada do cliente ao iniciar a reprodução e exibindo uma região que marca a área onde a busca não é permitida.

Para uma barra de controle:

1. Adicione uma sobreposição à barra de controle que representa o intervalo de reprodução.

1. Quando o usuário começar a procurar, verifique se a posição de busca desejada está dentro do intervalo pesquisável.
