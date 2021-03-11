---
title: Uso da visão geral da classe DRMManager
description: Uso da visão geral da classe DRMManager
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Uso da classe do DRMManager {#using-the-drmmanager-class}

Use a classe `DRMManager` para gerenciar licenças e sessões do servidor de licenças DRM Primetime em aplicativos.

**Gerenciamento de licenças**

Sempre que um dispositivo reproduz conteúdo protegido, o tempo de execução obtém e armazena em cache a licença necessária para visualizar o conteúdo. Se o aplicativo salvar o conteúdo localmente e a licença permitir reprodução offline, o usuário poderá visualizá-lo no aplicativo sem uma conexão de rede. Usando o `DRMManager`, você pode pré-armazenar a licença em cache. O pedido não tem de obter a licença necessária para visualizar o conteúdo. Por exemplo, seu aplicativo pode baixar o arquivo de mídia e obter a licença enquanto o usuário ainda está online.

Para pré-carregar uma licença, use um objeto `DRMContentData`. O objeto `DRMContentData` contém o URL do servidor de licenças Primetime DRM que pode fornecer a licença e descreve se a autenticação de usuário é necessária. Com essas informações, você pode chamar o método `DRMManager` `loadVoucher()` para obter e armazenar em cache a licença. O workflow para licenças de pré-carregamento é descrito em mais detalhes em *Licenças de pré-carregamento para reprodução offline*.

**Gerenciamento de sessão**

Você também pode usar o `DRMManager` para autenticar o usuário em um servidor de licença do Primetime DRM e gerenciar sessões persistentes. Chame o método `DRMManager` `authenticate()` para estabelecer uma sessão com o servidor de licença do Primetime DRM. Quando a autenticação é concluída com êxito, o `DRMManager` despacha um objeto `DRMAuthenticationCompleteEvent`. Este objeto contém um token de sessão. Você pode salvar esse token para estabelecer sessões futuras, de modo que o usuário não precise fornecer suas credenciais de conta. Passe o token para o método `setAuthenticationToken()` para estabelecer uma nova sessão autenticada. (As configurações do servidor que gerou o token determinam a expiração do token e outros atributos).

## Manipular eventos DRMStatus {#handling-drmstatus-events}

O `DRMManager` despacha um objeto `DRMStatusEvent` após a conclusão bem-sucedida de uma chamada para o método `loadVoucher()`. Se uma licença for obtida, a propriedade detail do objeto de evento terá o valor : `DRM.voucherObtained` e a propriedade voucher contém o objeto `DRMVoucher`. Se uma licença não for obtida, a propriedade detail ainda terá o valor : `DRM.voucherObtained`; no entanto, a propriedade voucher é nula. Não é possível obter uma licença se, por exemplo, você usar `LoadVoucherSetting` de `localOnly` e não houver uma licença em cache local. Se a chamada `loadVoucher()` não for concluída com êxito, talvez por causa de um erro de autenticação ou comunicação, o `DRMManager` despacha um objeto `DRMErrorEvent` ou `DRMAuthenticationErrorEvent`.

## Manipular eventos DRMAuthenticationComplete{#handling-drmauthenticationcomplete-events}

O `DRMManager` despacha um objeto `DRMAuthenticationCompleteEvent` quando um usuário é autenticado com êxito por meio de uma chamada para o método `authenticate()`. O objeto `DRMAuthenticationCompleteEvent` contém um token reutilizável que pode ser usado para persistir a autenticação do usuário em sessões do aplicativo. Passe este token para o método `DRMManager` `setAuthenticationToken()` para restabelecer a sessão. (O criador de token define atributos de token, como expiração. O Adobe não fornece uma API para examinar atributos de token.)

## Manipular eventos DRMAuthenticationError{#handling-drmauthenticationerror-events}

O `DRMManager` despacha um objeto `DRMAuthenticationErrorEvent` quando um usuário não pode ser autenticado com êxito por meio de uma chamada para os métodos `authenticate()` ou `setAuthenticationToken()`.