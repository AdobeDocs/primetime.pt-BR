---
description: Você pode implementar uma barra de controle com suporte a DVR para transmissão ao vivo e VOD. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.
seo-description: Você pode implementar uma barra de controle com suporte a DVR para transmissão ao vivo e VOD. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.
seo-title: Construa uma barra de controle aprimorada para DVR
title: Construa uma barra de controle aprimorada para DVR
uuid: 83c56def-a454-4f26-bdfc-2ef2497ef9bd
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Construa uma barra de controle aprimorada para DVR{#construct-a-control-bar-enhanced-for-dvr}

Você pode implementar uma barra de controle com suporte a DVR para transmissão ao vivo e VOD. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.

* Para VOD, o comprimento da janela pesquisável é a duração do ativo inteiro.
* Para transmissão ao vivo, o comprimento da janela DVR (pesquisável) é definido como o intervalo de tempo que começa na janela de reprodução ao vivo e termina no ponto ativo do cliente.

   O ponto ativo do cliente é calculado subtraindo o comprimento do buffer do final da janela ativa. A duração do destino é um valor maior ou igual à duração máxima de um fragmento no manifesto.

   A barra de controle para reprodução ao vivo suporta DVR ao posicionar primeiro a miniatura no ponto ativo do cliente ao iniciar a reprodução e ao exibir uma região que marca a área na qual a busca não é permitida.

Para uma barra de controle:

1. Adicione uma sobreposição à barra de controle que representa o intervalo de reprodução.

1. Quando o usuário começar a buscar, verifique se a posição de busca desejada está dentro do intervalo pesquisável.
