---
description: Um reprodutor de vídeo cliente ou o servidor de manifesto pode interagir com o CRS para obter o reempacotamento do JIT. Ambos usam a mesma lógica de seleção de publicidade.
title: Fluxos de trabalho detalhados para reempacotamento JIT
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Fluxos de trabalho detalhados para reempacotamento JIT {#detailed-workflows-for-jit-repackaging}

Um reprodutor de vídeo cliente ou o servidor de manifesto pode interagir com o CRS para obter o reempacotamento do JIT. Ambos usam a mesma lógica de seleção de publicidade.

## Reempacotamento JIT Iniciado pelo Servidor de Manifesto {#section_1F1C1B7DD146403890C2B43E24FEF0EB}

![](assets/ssai_JIT-workflow_web.png)

O fluxo de trabalho para reempacotamento de JIT no lado do servidor de manifesto é o seguinte:

1. O servidor de manifesto faz uma solicitação para o servidor de publicidade.
1. O servidor de manifesto recebe um anúncio criativo que não está no formato HLS.
1. O servidor de manifesto envia uma solicitação ao servidor CDN para uma versão HLS previamente transcodificada da criação para anúncios.

   >[!NOTE]
   >
   >Em uma configuração de várias CDN, o servidor de manifesto usa o parâmetro `ptcdn` no URL de inicialização para identificar o servidor CDN.

1. O servidor manifest verifica a resposta:

   1. Se a solicitação for bem-sucedida, o servidor de manifesto insere a versão HLS previamente transcodificada do anúncio criativo no fluxo de conteúdo.
   1. Se a solicitação falhar, o servidor de manifesto gera uma entrada de log e solicita uma versão transcodificada do CRS.

1. O CRS transcodifica o anúncio e faz upload da versão do HLS para o servidor CDN para uso futuro.

Para todas as solicitações subsequentes desse anúncio, o servidor de manifesto recupera a versão do HLS do CDN e a insere no fluxo de conteúdo.

## Reempacotamento JIT Iniciado pelo Cliente {#section_FBC97D40043F4FDD98247A08BB6195B0}

<!--<a id="fig_hkn_ndt_3z"></a>-->

![](assets/ssai_JIT-workflow_client_web.png)

Um cliente com base em TVSDK ou com recursos semelhantes pode interagir com o CRS para obter reempacotamento de JIT, da seguinte maneira:

1. O cliente solicita um anúncio do servidor de anúncios.
1. O servidor de publicidade retorna o anúncio ao cliente.
1. O cliente verifica o formato do anúncio no servidor de anúncios:

   1. Se o anúncio estiver no formato HLS, o cliente o insere (une pontos) no conteúdo e é feito.
   1. Se o anúncio não estiver no formato HLS, o cliente solicitará um ao servidor CDN.

      >[!NOTE]
      >
      >Em uma configuração de várias CDN, o servidor de manifesto usa o parâmetro `ptcdn` no URL de inicialização para identificar o servidor CDN.

1. O cliente verifica a resposta do servidor CDN.

   1. Se a CDN forneceu uma versão HLS, o cliente a insere (une pontos) no conteúdo e é feita.
   1. Se o servidor CDN não fornecer uma versão HLS, o cliente solicita ao servidor de anúncios que solicite uma do CRS. O cliente não insere o anúncio no conteúdo.

1. O servidor de anúncios solicita que a publicidade não HLS seja transcodificada para HLS.
1. O CRS cria uma versão do HLS e a carrega no servidor CDN para uso futuro.

## Prioridades e linha do tempo do formato de anúncio {#section_A74DE37A57BF45D7B6D09E3DE40F8E61}

O servidor de manifesto e o cliente usam a mesma lógica de seleção para determinar as prioridades para a reprodução de anúncios disponíveis. Os anúncios formatados com HLS são a primeira prioridade, seguidos por MP4, FLV e finalmente WebM.

O CRS normalmente requer de 2 a 4 minutos para processar um anúncio não-HLS criativo e geralmente menos de 3 minutos.

O CRS produz diferentes taxas de bits de HLS, de modo que o anúncio pode ser reproduzido a uma velocidade adequada à velocidade de conexão e largura de banda disponíveis. Se houver várias taxas de bits disponíveis, o CRS escolhe a maior taxa de bits disponível. Se o CRS receber um anúncio não HLS criativo, ele produzirá uma versão HLS na resolução mais alta disponível.