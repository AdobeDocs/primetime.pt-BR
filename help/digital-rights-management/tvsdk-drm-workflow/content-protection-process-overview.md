---
title: Visão geral do processo de aquisição de licença
description: Visão geral do processo de aquisição de licença
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Visão geral do processo de aquisição de licença{#license-acquisition-process-overview}

A habilitação do aplicativo para reproduzir conteúdo sob a proteção do Primetime DRM está descrita nas seções a seguir, usando amostras de código do ActionScript 3 (AS3). As saídas matizadas deste fluxo de trabalho para aplicativos nativos em plataformas móveis são apresentadas quando apropriado. Os workflows DRM do Primetime são muito semelhantes em todas as plataformas, no entanto, sua compreensão do código AS3 tornará a extrapolação para outras plataformas bastante simples.

**Processo de aquisição de licença:**

1. Obtenha os metadados DRM do conteúdo protegido.
1. Verifique se há uma licença disponível localmente:

   * Se a licença estiver disponível localmente, carregue-a e vá para a Etapa 6.
   * Se a licença não estiver disponível localmente, vá para a Etapa 3.

1. Verifique se a autenticação é necessária:

   * Se a autenticação for necessária, obtenha as credenciais de autenticação do usuário e transmita-as para o servidor de licenças.
   * Se a autenticação não for necessária, vá para a Etapa 6.

1. Se o registro do domínio do dispositivo for necessário, ingresse no domínio do dispositivo.
1. Se a autenticação foi necessária e está concluída, baixe a licença do servidor de licenças.
1. Reproduzir o conteúdo.

Se nenhum erro ocorrer e o usuário tiver sido autorizado com êxito a visualizar o conteúdo, o Primetime enviará um `DRMStatusEvent` e o aplicativo inicia a reprodução. A variável `DRMStatusEvent` O objeto contém as informações de licença relacionadas, que identificam a política e as permissões do usuário. Por exemplo, `DRMStatusEvent` pode conter informações sobre se o conteúdo pode ser disponibilizado offline, quando a licença expira e assim por diante.

O aplicativo pode usar as informações de licença para informar ao usuário o status de sua política. Por exemplo, o aplicativo pode exibir o número de dias restantes que o usuário tem para visualizar o conteúdo em uma barra de status. Se o usuário tiver acesso offline, a licença será armazenada em cache e o conteúdo criptografado será baixado no computador do usuário. O conteúdo é disponibilizado pela duração definida na duração do armazenamento em cache da licença. A propriedade detail no evento contém `DRM.voucherObtained`. O aplicativo decide onde armazenar o conteúdo localmente para que ele fique disponível offline. Também é possível pré-carregar licenças usando o `DRMManager` classe.
