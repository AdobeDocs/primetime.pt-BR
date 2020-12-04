---
seo-title: Uso da visão geral da classe do DRMManager
title: Uso da visão geral da classe do DRMManager
uuid: 71ce061b-75b6-4ab5-8bbd-cafe7c3e4592
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Uso da classe DRMManager {#using-the-drmmanager-class}

Use a classe `DRMManager` para gerenciar licenças e sessões do servidor de licenças Primetime DRM nos aplicativos.

**Gerenciamento de licenças**

Sempre que um dispositivo reproduz conteúdo protegido, o tempo de execução obtém e armazena em cache a licença necessária para visualização do conteúdo. Se o aplicativo salvar o conteúdo localmente e a licença permitir a reprodução offline, o usuário poderá visualização o conteúdo no aplicativo sem uma conexão de rede. Usando o `DRMManager`, você pode pré-armazenar a licença em cache. O aplicativo não precisa obter a licença necessária para visualização do conteúdo. Por exemplo, seu aplicativo pode baixar o arquivo de mídia e obter a licença enquanto o usuário ainda está online.

Para pré-carregar uma licença, use um objeto `DRMContentData`. O objeto `DRMContentData` contém o URL do servidor de licenças Primetime DRM que pode fornecer a licença e descreve se a autenticação do usuário é necessária. Com essas informações, você pode chamar o método `DRMManager` `loadVoucher()` para obter e armazenar a licença em cache. O fluxo de trabalho das licenças de pré-carregamento é descrito com mais detalhes em *licenças de Pré-carregamento para reprodução offline*.

**Gerenciamento de sessões**

Você também pode usar o `DRMManager` para autenticar o usuário em um servidor de licenças Primetime DRM e gerenciar sessões persistentes. Chame o método `DRMManager` `authenticate()` para estabelecer uma sessão com o servidor de licenças Primetime DRM. Quando a autenticação é concluída com êxito, `DRMManager` despacha um objeto `DRMAuthenticationCompleteEvent`. Este objeto contém um token de sessão. Você pode salvar esse token para estabelecer sessões futuras, de modo que o usuário não precise fornecer suas credenciais de conta. Passe o token para o método `setAuthenticationToken()` para estabelecer uma nova sessão autenticada. (As configurações do servidor que gerou o token determinam a expiração do token e outros atributos).

## Tratamento de Eventos DRMStatus {#handling-drmstatus-events}

O `DRMManager` despacha um objeto `DRMStatusEvent` depois que uma chamada para o método `loadVoucher()` é concluída com êxito. Se uma licença for obtida, a propriedade detail do objeto de evento terá o valor: `DRM.voucherObtained` e a propriedade de comprovante contém o objeto `DRMVoucher`. Se uma licença não for obtida, a propriedade detail ainda terá o valor: `DRM.voucherObtained`; no entanto, a propriedade do comprovante é nula. Uma licença não pode ser obtida se, por exemplo, você usar `LoadVoucherSetting` de `localOnly` e não houver uma licença em cache local. Se a chamada `loadVoucher()` não for concluída com êxito, talvez devido a um erro de autenticação ou comunicação, o `DRMManager` despacha um objeto `DRMErrorEvent` ou `DRMAuthenticationErrorEvent` em vez disso.

## Tratamento de Eventos DRMAuthenticationComplete{#handling-drmauthenticationcomplete-events}

O `DRMManager` despacha um objeto `DRMAuthenticationCompleteEvent` quando um usuário é autenticado com êxito por meio de uma chamada para o método `authenticate()`. O objeto `DRMAuthenticationCompleteEvent` contém um token reutilizável que pode ser usado para persistir a autenticação do usuário nas sessões do aplicativo. Passe esse token para o método `DRMManager` `setAuthenticationToken()` para restabelecer a sessão. (O criador de token define atributos de token como expiração. Adobe não fornece uma API para examinar atributos de token.)

## Tratamento de eventos DRMAuthenticationError{#handling-drmauthenticationerror-events}

O `DRMManager` despacha um objeto `DRMAuthenticationErrorEvent` quando um usuário não pode ser autenticado com êxito por meio de uma chamada para os métodos `authenticate()` ou `setAuthenticationToken()`.