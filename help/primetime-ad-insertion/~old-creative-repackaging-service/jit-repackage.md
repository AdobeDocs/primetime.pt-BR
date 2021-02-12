---
description: Um player de vídeo cliente ou o servidor manifest pode interagir com o CRS para obter o reempacotamento JIT. Ambos usam a mesma lógica de seleção de anúncio.
seo-description: Um player de vídeo cliente ou o servidor manifest pode interagir com o CRS para obter o reempacotamento JIT. Ambos usam a mesma lógica de seleção de anúncio.
seo-title: Workflows detalhados para reempacotamento JIT
title: Workflows detalhados para reempacotamento JIT
uuid: 11b6eb3c-f6aa-4018-9b20-ab6f5910508b
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---


# Workflows detalhados para o reempacotamento JIT {#detailed-workflows-for-jit-repackaging}

Um player de vídeo cliente ou o servidor manifest pode interagir com o CRS para obter o reempacotamento JIT. Ambos usam a mesma lógica de seleção de anúncio.

## Reempacotamento JIT iniciado pelo servidor de manifesto {#section_1F1C1B7DD146403890C2B43E24FEF0EB}

![](assets/ssai_JIT-workflow_web.png)

O fluxo de trabalho para reempacotamento JIT no lado do servidor manifest é o seguinte:

1. O servidor manifest faz uma solicitação para o servidor de publicidade.
1. O servidor manifest recebe um anúncio criativo que não está no formato HLS.
1. O servidor manifest envia uma solicitação ao servidor CDN para uma versão HLS previamente transcodificada do anúncio.

   >[!NOTE]
   >
   >Em uma configuração de vários CDN, o servidor manifest usa o parâmetro `ptcdn` no URL de inicialização para identificar o servidor CDN.

1. O servidor manifest verifica a resposta:

   1. Se a solicitação for bem-sucedida, o servidor de manifesto inserirá a versão HLS transcodificada anteriormente do anúncio no fluxo de conteúdo.
   1. Se a solicitação falhar, o servidor manifest gera uma entrada de log e solicita uma versão transcodificada do CRS.

1. O CRS transcodifica o anúncio e faz upload da versão HLS para o servidor CDN para uso futuro.

Para todas as solicitações subsequentes desse anúncio, o servidor manifest recupera a versão HLS do CDN e a insere no fluxo de conteúdo.

## Reempacotamento JIT iniciado pelo cliente {#section_FBC97D40043F4FDD98247A08BB6195B0}

<!--<a id="fig_hkn_ndt_3z"></a>-->

![](assets/ssai_JIT-workflow_client_web.png)

Um cliente com base no TVSDK ou com recursos semelhantes pode interagir com o CRS para obter o reempacotamento JIT, da seguinte forma:

1. O cliente solicita um anúncio do servidor de publicidade.
1. O servidor de publicidade retorna o anúncio para o cliente.
1. O cliente verifica o formato do anúncio no servidor de publicidade:

   1. Se o anúncio estiver no formato HLS, o cliente o inserirá (pontos) no conteúdo e será feito.
   1. Se o anúncio não estiver no formato HLS, o cliente solicitará um do servidor CDN.

      >[!NOTE]
      >
      >Em uma configuração de vários CDN, o servidor manifest usa o parâmetro `ptcdn` no URL de inicialização para identificar o servidor CDN.

1. O cliente verifica a resposta do servidor CDN.

   1. Se o CDN forneceu uma versão HLS, o cliente a insere (pontos) no conteúdo e é feito.
   1. Se o servidor CDN não fornecer uma versão HLS, o cliente solicitará que o servidor de publicidade solicite uma do CRS. O cliente não insere o anúncio no conteúdo.

1. O servidor de anúncios solicita que a publicidade não HLS seja transcodificada para HLS.
1. O CRS cria uma versão HLS e a carrega no servidor CDN para uso futuro.

## Prioridades e Linha do tempo do formato de anúncio {#section_A74DE37A57BF45D7B6D09E3DE40F8E61}

O servidor manifest e o cliente usam a mesma lógica de seleção para determinar as prioridades para a reprodução de anúncios disponíveis. Anúncios formatados em HLS são a primeira prioridade, seguidos por MP4, FLV e, finalmente, WebM.

O CRS normalmente requer de 2 a 4 minutos para processar um anúncio não HLS criativo e, geralmente, menos de 3 minutos.

O CRS produz diferentes taxas de bits HLS, de modo que o anúncio pode ser reproduzido a uma velocidade adequada à velocidade e largura de banda da conexão disponível. Se houver várias taxas de bits disponíveis, o CRS escolherá a maior taxa de bits disponível. Se o CRS receber um anúncio não HLS criativo, ele produzirá uma versão HLS na resolução mais alta disponível.