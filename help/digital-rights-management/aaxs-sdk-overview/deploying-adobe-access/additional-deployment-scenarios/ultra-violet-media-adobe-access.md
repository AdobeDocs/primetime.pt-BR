---
description: O Adobe Access pode ser usado com outras soluções de transmissão de conteúdo de terceiros para configurar um ecossistema de distribuição de mídia completo e seguro, baseado em DRM.
title: Mídia UltraViolet e Acesso Adobe
exl-id: cca476a4-1961-46d8-aad4-bc7c996d7b02
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Mídia UltraViolet e Acesso Adobe {#ultraviolet-media-and-adobe-access}

O Adobe Access pode ser usado com outras soluções de transmissão de conteúdo de terceiros para configurar um ecossistema de distribuição de mídia completo e seguro, baseado em DRM.

UltraVioleta ( [](https://www.uvvu.com/)) é um sistema de autenticação de direitos digitais e distribuição baseada em nuvem que permite aos consumidores de conteúdo de entretenimento da casa digital transmitir e baixar conteúdo adquirido por meio de várias plataformas e dispositivos. O conteúdo UltraViolet será baixado (ou transmitido) em um formato de arquivo comum (CFF) usando a Criptografia comum (CENC).

É fácil configurar um sistema UltraViolet juntamente com o Adobe Access. O caso de uso a seguir descreve o comportamento do fluxo de conteúdo:

<!--<a id="fig_cxy_dc2_44"></a>-->

![](assets/AdobeUV_web.png)

1. O proprietário do conteúdo codifica e compacta o conteúdo em CFF. O conteúdo empacotado é licenciado para distribuição a um varejista.
1. O varejista faz upload do conteúdo para um provedor de serviços digitais, como o CDN. O conteúdo agora está disponível para download. Observe que algumas dessas funções podem ser desempenhadas por uma ou mais empresas.

   O usuário final tem um dispositivo compatível com o Adobe AIR. Além disso, o usuário precisa instalar uma aplicação compatível com UltraViolet. O aplicativo inclui o código necessário para analisar o CFF e apresentá-lo para consumo pelo tempo de execução. Todas as operações criptográficas confidenciais são tratadas no tempo de execução seguro.
1. O aplicativo pode acionar uma associação de domínio para o dispositivo, que interage com o coordenador. O coordenador mantém um registrador de direitos, um banco de dados de usuários e domínios. O gerenciador de domínio do coordenador é construído usando o SDK de acesso do Adobe para implementar operações de ingresso/saída de domínio específicas do acesso do Adobe.
1. O usuário pode usar o aplicativo para selecionar um vídeo que deseja adquirir do varejista. O varejista normalmente fornece um portal da Web e lida com toda a lógica de negócios.
1. O varejista interage com o coordenador para adicionar um token de direitos. O varejista então redireciona a solicitação para o provedor de serviços para o download do conteúdo real.
1. Se o dispositivo ainda não tiver uma licença para o conteúdo, ele acionará uma solicitação de licença usando o CFF. A solicitação normalmente inclui um certificado de domínio, credenciais de usuário e informações sobre o aplicativo. O provedor de serviços opera um Adobe Access License Server (desenvolvido com o SDK de acesso ao Adobe) que segue as especificações do UltraViolet.
1. A lógica de negócios UltraViolet do provedor de serviços interage com o coordenador conforme necessário para recuperar o token de direitos apropriado para determinar se uma licença de conteúdo deve ser emitida.

   A licença de conteúdo está vinculada ao domínio. O aplicativo cliente pode inserir a licença no arquivo CFF. O conteúdo agora pode ser reproduzido de volta no aplicativo, com toda a proteção e aplicação de regras de uso tratadas pelo componente de Acesso ao Adobe no tempo de execução.
1. Outros dispositivos e aplicativos pertencentes ao mesmo usuário final podem ser registrados com o coordenador. O conteúdo agora pode ser carregado em outros dispositivos de acesso Adobe sem exigir nenhuma transação externa.
