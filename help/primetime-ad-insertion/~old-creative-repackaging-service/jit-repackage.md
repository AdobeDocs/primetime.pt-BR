---
description: Um player de vídeo cliente ou o servidor de manifesto podem interagir com o CRS para obter o reempacotamento da JIT. Ambos usam a mesma lógica de seleção de anúncios.
title: Fluxos de trabalho detalhados para reempacotamento de JIT
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Fluxos de trabalho detalhados para reempacotamento de JIT {#detailed-workflows-for-jit-repackaging}

Um player de vídeo cliente ou o servidor de manifesto podem interagir com o CRS para obter o reempacotamento da JIT. Ambos usam a mesma lógica de seleção de anúncios.

## Reempacotamento de JIT iniciado pelo Servidor Manifest {#section_1F1C1B7DD146403890C2B43E24FEF0EB}

![](assets/ssai_JIT-workflow_web.png)

O fluxo de trabalho para o reempacotamento de JIT no lado do servidor de manifesto é o seguinte:

1. O servidor de manifesto faz uma solicitação ao servidor de anúncios.
1. O servidor de manifesto recebe um anúncio criativo que não está no formato HLS.
1. O servidor de manifesto envia uma solicitação ao servidor CDN para uma versão HLS transcodificada anteriormente do criativo do anúncio.

   >[!NOTE]
   >
   >Em uma configuração de vários CDNs, o servidor de manifesto usa o `ptcdn` no URL de inicialização para identificar o servidor CDN.

1. O servidor de manifesto verifica a resposta:

   1. Se a solicitação for bem-sucedida, o servidor de manifesto inserirá a versão HLS transcodificada anteriormente da campanha criativa no fluxo de conteúdo.
   1. Se a solicitação falhar, o servidor de manifesto gera uma entrada de log e solicita uma versão transcodificada do CRS.

1. O CRS transcodifica o criativo do anúncio e carrega a versão do HLS no servidor CDN para uso futuro.

Para todas as solicitações subsequentes desse criativo, o servidor de manifesto recupera a versão HLS do CDN e a insere no fluxo de conteúdo.

## Reempacotamento de JIT iniciado pelo cliente {#section_FBC97D40043F4FDD98247A08BB6195B0}

<!--<a id="fig_hkn_ndt_3z"></a>-->

![](assets/ssai_JIT-workflow_client_web.png)

Um cliente com base no TVSDK ou com recursos semelhantes pode interagir com o CRS para obter o reempacotamento da JIT, da seguinte maneira:

1. O cliente solicita um anúncio do servidor de anúncios.
1. O servidor de anúncios retorna o anúncio ao cliente.
1. O cliente verifica o formato do anúncio no servidor de anúncios:

   1. Se o criativo do anúncio estiver no formato HLS, o cliente o inserirá (costuma) no conteúdo e será concluído.
   1. Se o criativo do anúncio não estiver no formato HLS, o cliente solicitará um do servidor CDN.

      >[!NOTE]
      >
      >Em uma configuração de vários CDNs, o servidor de manifesto usa o `ptcdn` no URL de inicialização para identificar o servidor CDN.

1. O cliente verifica a resposta do servidor CDN.

   1. Se a CDN forneceu uma versão do HLS, o cliente a insere (compila) no conteúdo e está concluído.
   1. Se o servidor CDN não fornecer uma versão HLS, o cliente solicitará ao servidor de anúncios que solicite uma do CRS. O cliente não insere o anúncio no conteúdo.

1. O servidor de anúncios solicita que os não-HLS sejam transcodificados para HLS.
1. O CRS cria uma versão do HLS e a carrega no servidor CDN para uso futuro.

## Prioridades de Formato de Anúncio e Linha do Tempo {#section_A74DE37A57BF45D7B6D09E3DE40F8E61}

O servidor de manifesto e o cliente usam a mesma lógica de seleção para determinar as prioridades para reproduzir os anúncios disponíveis. Anúncios formatados em HLS são de primeira prioridade, seguidos por MP4, FLV e, por fim, WebM.

O CRS geralmente leva de 2 a 4 minutos para processar um anúncio não HLS e criativo, geralmente menos de 3 minutos.

O CRS produz diferentes taxas de bits HLS, de modo que o anúncio pode ser reproduzido em uma velocidade adequada à velocidade de conexão e largura de banda disponíveis. Se houver várias taxas de bits disponíveis, o CRS escolherá a taxa de bits mais alta disponível. Se o CRS receber um anúncio não HLS criativo, ele produzirá uma versão HLS na maior resolução disponível.