---
seo-title: Uso da visão geral da classe do DRMManager
title: Uso da visão geral da classe do DRMManager
uuid: 71ce061b-75b6-4ab5-8bbd-cafe7c3e4592
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Uso da classe DRMManager {#using-the-drmmanager-class}

Use a `DRMManager` classe para gerenciar licenças e sessões do servidor de licenças Primetime DRM nos aplicativos.

**Gerenciamento de licenças**

Sempre que um dispositivo reproduz conteúdo protegido, o tempo de execução obtém e armazena em cache a licença necessária para exibir o conteúdo. Se o aplicativo salvar o conteúdo localmente e a licença permitir a reprodução offline, o usuário poderá visualizá-lo no aplicativo sem uma conexão de rede. Usando o `DRMManager`, você pode pré-armazenar a licença em cache. O aplicativo não precisa obter a licença necessária para exibir o conteúdo. Por exemplo, seu aplicativo pode baixar o arquivo de mídia e obter a licença enquanto o usuário ainda está online.

Para pré-carregar uma licença, use um `DRMContentData` objeto. O `DRMContentData` objeto contém o URL do servidor de licenças Primetime DRM que pode fornecer a licença e descreve se a autenticação do usuário é necessária. Com essas informações, você pode chamar o `DRMManager` `loadVoucher()` método para obter e armazenar a licença em cache. O fluxo de trabalho das licenças de pré-carregamento é descrito com mais detalhes em *Pré-carregar licenças para reprodução* offline.

**Gerenciamento de sessões**

Você também pode usar o para autenticar o usuário em um servidor de licenças Primetime DRM e gerenciar sessões persistentes. `DRMManager` Chame o `DRMManager` `authenticate()` método para estabelecer uma sessão com o servidor de licenças Primetime DRM. Quando a autenticação é concluída com êxito, o `DRMManager` envia um `DRMAuthenticationCompleteEvent` objeto. Este objeto contém um token de sessão. Você pode salvar esse token para estabelecer sessões futuras, de modo que o usuário não precise fornecer suas credenciais de conta. Passe o token para o `setAuthenticationToken()` método para estabelecer uma nova sessão autenticada. (As configurações do servidor que gerou o token determinam a expiração do token e outros atributos).

## Tratamento de eventos DRMStatus {#handling-drmstatus-events}

O `DRMManager` envia um `DRMStatusEvent` objeto depois que uma chamada para o `loadVoucher()` método é concluída com êxito. Se uma licença for obtida, a propriedade detail do objeto event terá o valor: `DRM.voucherObtained`e a propriedade do comprovante contém o `DRMVoucher` objeto. Se uma licença não for obtida, a propriedade detail ainda terá o valor: `DRM.voucherObtained`; no entanto, a propriedade do comprovante é nula. Uma licença não pode ser obtida se, por exemplo, você usar o `LoadVoucherSetting` de `localOnly` e não houver uma licença em cache local. Se a `loadVoucher()` chamada não for concluída com êxito, talvez devido a um erro de autenticação ou comunicação, o `DRMManager` envia um objeto `DRMErrorEvent` ou `DRMAuthenticationErrorEvent` .

## Tratamento de eventos DRMAuthenticationComplete{#handling-drmauthenticationcomplete-events}

O `DRMManager` envia um `DRMAuthenticationCompleteEvent` objeto quando um usuário é autenticado com êxito por meio de uma chamada para o `authenticate()` método. O `DRMAuthenticationCompleteEvent` objeto contém um token reutilizável que pode ser usado para persistir a autenticação do usuário nas sessões do aplicativo. Passe este token para `DRMManager` `setAuthenticationToken()` o método para restabelecer a sessão. (O criador de token define atributos de token como expiração. A Adobe não fornece uma API para examinar atributos de token.)

## Tratamento de eventos DRMAuthenticationError{#handling-drmauthenticationerror-events}

O `DRMManager` envia um `DRMAuthenticationErrorEvent` objeto quando um usuário não pode ser autenticado com êxito por meio de uma chamada para os métodos `authenticate()` ou `setAuthenticationToken()` .