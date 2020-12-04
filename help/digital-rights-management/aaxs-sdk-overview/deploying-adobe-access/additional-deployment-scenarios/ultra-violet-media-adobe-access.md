---
description: O Acesso ao Adobe pode ser usado com outras soluções de streaming de conteúdo de terceiros para configurar um ecossistema de distribuição de mídia baseado em DRM completo e seguro.
seo-description: O Acesso ao Adobe pode ser usado com outras soluções de streaming de conteúdo de terceiros para configurar um ecossistema de distribuição de mídia baseado em DRM completo e seguro.
seo-title: Mídia UltraViolet e acesso a Adobe
title: Mídia UltraViolet e acesso a Adobe
uuid: d287680f-02de-4cca-aeea-22b7fd8e67d2
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# Mídia UltraViolet e acesso a Adobe {#ultraviolet-media-and-adobe-access}

O Acesso ao Adobe pode ser usado com outras soluções de streaming de conteúdo de terceiros para configurar um ecossistema de distribuição de mídia baseado em DRM completo e seguro.

O UltraViolet ( [](https://www.uvvu.com/)) é um sistema de autenticação de direitos digitais e distribuição baseado em nuvem que permite que os consumidores de conteúdo de entretenimento da casa digital façam stream e baixem conteúdo adquirido por meio de várias plataformas e dispositivos. O conteúdo UltraViolet será baixado (ou transmitido) em um Formato de arquivo comum (CFF) usando Criptografia comum (CENC).

É fácil configurar um sistema UltraViolet junto com o Adobe Access. O caso de uso a seguir descreve o comportamento do fluxo de conteúdo:

<!--<a id="fig_cxy_dc2_44"></a>-->

![](assets/AdobeUV_web.png)

1. O proprietário do conteúdo codifica e agrupa o conteúdo no CFF. O conteúdo empacotado é licenciado para distribuição a um varejista.
1. O varejista faz upload do conteúdo para um provedor de serviço digital, como CDN. O conteúdo agora está disponível para download. Observe que algumas dessas funções podem ser executadas por uma ou mais empresas.

   O usuário final tem um dispositivo compatível com o Adobe AIR. Além disso, o usuário precisa instalar um aplicativo compatível com UltraViolet. O aplicativo inclui o código necessário para analisar o CFF e apresentá-lo para consumo pelo tempo de execução. Todas as operações criptográficas confidenciais são manipuladas no tempo de execução seguro.
1. O aplicativo pode acionar um ingresso de domínio para o dispositivo, que interage com o coordenador. O coordenador mantém um bloqueador de direitos, um banco de dados de usuários e domínios. O gerenciador de domínio do coordenador é criado usando o SDK de acesso ao Adobe para implementar operações de entrada/saída de domínio específicas do acesso ao Adobe.
1. O usuário pode usar o aplicativo para selecionar um vídeo que deseja adquirir do varejista. O varejista normalmente fornece um portal da Web e lida com toda a lógica comercial.
1. Em seguida, o retalhista interage com o coordenador para adicionar um token de direitos. O varejista redireciona a solicitação para o provedor de serviço para o download do conteúdo real.
1. Se o dispositivo ainda não tiver uma licença para o conteúdo, ele acionará uma solicitação de licença usando o CFF. Normalmente, a solicitação inclui um certificado de domínio, credenciais de usuário e informações sobre o aplicativo. O provedor de serviço opera um servidor de licença de acesso a Adobe (desenvolvido com o SDK de acesso a Adobe) que segue as especificações UltraViolet.
1. A lógica comercial UltraViolet do provedor de serviço interage com o coordenador conforme necessário para recuperar o token de direitos apropriado para determinar se uma licença de conteúdo deve ser emitida.

   A licença de conteúdo está vinculada ao domínio. O aplicativo cliente pode inserir a licença no arquivo CFF. O conteúdo agora pode ser reproduzido no aplicativo, com toda a aplicação de regras de proteção e uso manipulada pelo componente de Acesso ao Adobe no tempo de execução.
1. Outros dispositivos e aplicações pertencentes ao mesmo utilizador final podem ser registrados no coordenador. O conteúdo agora pode ser carregado em outros dispositivos de acesso a Adobe sem exigir nenhuma transação externa.

