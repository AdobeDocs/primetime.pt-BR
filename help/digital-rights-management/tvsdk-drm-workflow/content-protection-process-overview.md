---
seo-title: Visão geral do processo de aquisição de licença
title: Visão geral do processo de aquisição de licença
uuid: c2eedd0a-3e3a-4c2f-a781-855f0ba65b15
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Visão geral do processo de aquisição de licença{#license-acquisition-process-overview}

A habilitação do aplicativo para reproduzir conteúdo sob a proteção do Primetime DRM está descrita nas seções a seguir, usando amostras de código do ActionScript 3 (AS3). Os desvios diferenciados desse fluxo de trabalho para aplicativos nativos em plataformas móveis são apresentados quando apropriado. No entanto, os fluxos de trabalho do DRM do Primetime são muito semelhantes em todas as plataformas, de modo que sua compreensão do código AS3 tornará a extrapolação para outras plataformas bastante simples.

**Processo de aquisição de licença:**

1. Obtenha os metadados DRM do conteúdo protegido.
1. Verifique se uma licença está disponível localmente:

   * Se a licença estiver disponível localmente, carregue a licença e vá para a Etapa 6.
   * Se a licença não estiver disponível localmente, vá para a Etapa 3.

1. Verifique se a autenticação é necessária:

   * Se a autenticação for necessária, obtenha as credenciais de autenticação do usuário e passe-as para o servidor de licenças.
   * Se a autenticação não for obrigatória, vá para a Etapa 6.

1. Se o registro de domínio do dispositivo for necessário, ingresse no domínio do dispositivo.
1. Se a autenticação for necessária e agora estiver concluída, baixe a licença do servidor de licenças.
1. Reproduzir o conteúdo.

Se não ocorrerem erros e o usuário tiver sido autorizado com êxito a exibir o conteúdo, o Primetime despachará um `DRMStatusEvent` objeto e o aplicativo começará a reprodução. O `DRMStatusEvent` objeto contém as informações de licença relacionadas, que identificam a política e as permissões do usuário. Por exemplo, `DRMStatusEvent` pode conter informações sobre se o conteúdo pode ser disponibilizado offline, quando a licença expira e assim por diante.

O aplicativo pode usar as informações de licença para informar o usuário sobre o status de sua política. Por exemplo, o aplicativo pode exibir o número de dias restantes que o usuário tem para exibir o conteúdo em uma barra de status. Se o usuário tiver acesso offline permitido, a licença será armazenada em cache e o conteúdo criptografado será baixado no computador do usuário. O conteúdo é disponibilizado pela duração definida na duração do armazenamento em cache da licença. A propriedade detail no evento contém `DRM.voucherObtained`. O aplicativo decide onde armazenar o conteúdo localmente para que ele esteja disponível offline. Você também pode pré-carregar licenças usando a `DRMManager` classe.
