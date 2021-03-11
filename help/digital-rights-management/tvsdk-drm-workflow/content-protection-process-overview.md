---
title: Visão geral do processo de aquisição de licença
description: Visão geral do processo de aquisição de licença
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# Visão geral do processo de aquisição de licença{#license-acquisition-process-overview}

Habilitar seu aplicativo para reproduzir conteúdo sob a proteção do DRM do Primetime é descrito nas seções a seguir, usando amostras de código do ActionScript 3 (AS3). As saídas com nuance desse fluxo de trabalho para aplicativos nativos em plataformas móveis são apresentadas quando apropriado. Os workflows de DRM do Primetime são muito semelhantes em todas as plataformas, no entanto, sua compreensão do código AS3 tornará a extrapolação para outras plataformas bastante simples.

**Processo de aquisição de licença:**

1. Obtenha os metadados DRM do conteúdo protegido.
1. Verifique se uma licença está disponível no local:

   * Se a licença estiver disponível localmente, carregue a licença e vá para a Etapa 6.
   * Se a licença não estiver disponível localmente, vá para a Etapa 3.

1. Verifique se a autenticação é necessária:

   * Se a autenticação for necessária, obtenha as credenciais de autenticação do usuário e as transmita ao servidor de licenças.
   * Se a autenticação não for necessária, vá para a Etapa 6.

1. Se o registro de domínio do dispositivo for necessário, participe do domínio do dispositivo.
1. Se a autenticação for necessária e agora estiver concluída, baixe a licença do servidor de licenças.
1. Reproduzir o conteúdo.

Se nenhum erro ocorrer e o usuário tiver sido autorizado com êxito a visualizar o conteúdo, o Primetime enviará um objeto `DRMStatusEvent` e o aplicativo iniciará a reprodução. O objeto `DRMStatusEvent` contém as informações de licença relacionadas, que identificam a política e as permissões do usuário. Por exemplo, `DRMStatusEvent` pode conter informações sobre se o conteúdo pode ser disponibilizado offline, quando a licença expira e assim por diante.

O aplicativo pode usar as informações da licença para informar o usuário sobre o status de sua política. Por exemplo, o aplicativo pode exibir o número de dias restantes que o usuário tem para visualizar o conteúdo em uma barra de status. Se o usuário tiver acesso offline, a licença será armazenada em cache e o conteúdo criptografado será baixado no computador do usuário. O conteúdo é disponibilizado pela duração definida no armazenamento em cache da licença. A propriedade detail no evento contém `DRM.voucherObtained`. O aplicativo decide onde armazenar o conteúdo localmente para que ele fique disponível offline. Você também pode pré-carregar licenças usando a classe `DRMManager`.
