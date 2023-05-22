---
title: Usando a visão geral de classe do DRMManager
description: Usando a visão geral de classe do DRMManager
copied-description: true
exl-id: 941a69fb-3085-45d6-9176-08ebb93cada4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Uso da classe DRMManager {#using-the-drmmanager-class}

Use o `DRMManager` classe para gerenciar licenças e sessões de servidor de licenças do Primetime DRM em aplicativos.

**Gerenciamento de licenças**

Sempre que um dispositivo reproduz um conteúdo protegido, o tempo de execução obtém e armazena em cache a licença necessária para visualizar o conteúdo. Se o aplicativo salvar o conteúdo localmente e a licença permitir a reprodução offline, o usuário poderá visualizar o conteúdo no aplicativo sem uma conexão de rede. Usar o `DRMManager`, você pode pré-armazenar a licença em cache. O aplicativo não precisa obter a licença necessária para visualizar o conteúdo. Por exemplo, seu aplicativo pode baixar o arquivo de mídia e obter a licença enquanto o usuário ainda está online.

Para pré-carregar uma licença, use um `DRMContentData` objeto. A variável `DRMContentData` O objeto contém o URL do servidor de licença do Primetime DRM que pode fornecer a licença e descreve se a autenticação de usuário é necessária. Com essas informações, você pode chamar o `DRMManager` `loadVoucher()` para obter e armazenar a licença em cache. O fluxo de trabalho para licenças de pré-carregamento é descrito com mais detalhes em *Licenças de pré-carregamento para reprodução offline*.

**Gerenciamento de sessão**

Você também pode usar a variável `DRMManager` para autenticar o usuário em um servidor de licença do Primetime DRM e gerenciar sessões persistentes. Chame o `DRMManager` `authenticate()` para estabelecer uma sessão com o servidor de licenças do Primetime DRM. Quando a autenticação é concluída com sucesso, a variável `DRMManager` despacha um `DRMAuthenticationCompleteEvent` objeto. Este objeto contém um token de sessão. Você pode salvar esse token para estabelecer sessões futuras para que o usuário não precise fornecer suas credenciais de conta. Passe o token para o `setAuthenticationToken()` para estabelecer uma nova sessão autenticada. (As configurações do servidor que gerou o token determinam a expiração do token e outros atributos).

## Manipular eventos DRMStatus {#handling-drmstatus-events}

A variável `DRMManager` despacha um `DRMStatusEvent` após uma chamada para o `loadVoucher()` O método é concluído com sucesso. Se uma licença for obtida, a propriedade detail do objeto de evento terá o valor: `DRM.voucherObtained`, e a propriedade voucher contém o `DRMVoucher` objeto. Se uma licença não for obtida, a propriedade detail ainda terá o valor: `DRM.voucherObtained`; no entanto, a propriedade voucher é nula. Uma licença não pode ser obtida se, por exemplo, você usar o `LoadVoucherSetting` de `localOnly` e não há licença armazenada em cache localmente. Se a variável `loadVoucher()` chamada não for concluída com êxito, talvez devido a um erro de autenticação ou comunicação, a variável `DRMManager` despacha um `DRMErrorEvent` ou `DRMAuthenticationErrorEvent` objeto.

## Manipulação de eventos DRMAuthenticationComplete{#handling-drmauthenticationcomplete-events}

A variável `DRMManager` despacha um `DRMAuthenticationCompleteEvent` objeto quando um usuário é autenticado com êxito por meio de uma chamada para o `authenticate()` método. A variável `DRMAuthenticationCompleteEvent` o objeto contém um token reutilizável que pode ser usado para manter a autenticação do usuário nas sessões do aplicativo. Passe este token para `DRMManager` `setAuthenticationToken()` para restabelecer a sessão. (O criador do token define atributos de token, como expiração. O Adobe não fornece uma API para examinar atributos de token.)

## Manipulação de eventos DRMAuthenticationError{#handling-drmauthenticationerror-events}

A variável `DRMManager` despacha um `DRMAuthenticationErrorEvent` objeto quando um usuário não puder ser autenticado com êxito por meio de uma chamada para o `authenticate()` ou `setAuthenticationToken()` métodos.
