---
description: O Gerenciador de direitos é o gerenciador de recursos que oferece suporte à implementação de autenticação do Primetime.
title: Visão geral do Gerenciador de direitos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# Visão geral do Gerenciador de direitos {#entitlement-manager-overview}

O Gerenciador de direitos é o gerenciador de recursos que oferece suporte à implementação de autenticação do Primetime.

## Visão geral dos recursos

A integração de autenticação do Primetime com a Implementação de referência do SDK do Android Primetime adiciona um novo gerenciador de recursos ao aplicativo. No entanto, diferentemente de muitos dos outros gerentes de recursos, *o EntitlementManager é usado em vários locais no aplicativo*. A seguir, uma visão geral das alterações e adições feitas na Implementação de referência para oferecer suporte à autenticação do Primetime:

### Classe EntitlementManager

A classe `EntitlementManager` lida com toda a comunicação com o SDK de autenticação do Primetime, além de encapsula a lógica do aplicativo necessária para os workflows de direito. A API pública de `EntitlementManager` é usada pelo aplicativo para iniciar workflows de direito, enquanto a interface `EntitlementMangerListener` fornece um mecanismo de retorno de chamada para o aplicativo manipular eventos `EntitlementManger`.

### Retornos de chamada do EntitlementManager

A atividade principal da Implementação de referência, o `CatalogActivity`, cria uma instância de `EntitlementManagerListener` e a registra no `EntitlementManager`. Dessa forma, o `EntitlementManager` pode sinalizar as atualizações necessárias da interface do usuário para o restante do aplicativo. Os retornos de chamada incluem a exibição/ocultação de uma caixa de diálogo de carregamento, a exibição de caixas de diálogo de status, a atualização de ícones de autorização e autenticação e o início da reprodução de vídeo após uma autorização bem-sucedida.

### Caixas de diálogo de direitos

A classe `EntitlementDialogFragment` gera mensagens de diálogo com base no status de direito passado para o construtor de classe. Essa classe é usada para mensagens de sucesso de autenticação, bem como todas as mensagens de erro. O `CatalogActivity` exibe as caixas de diálogo de direito quando recebe eventos específicos do `EntitlementManager`. Além disso, o `CatalogActivity` implementa a interface `EntitlementDialogListener`, que inclui métodos de retorno de chamada para sinalizar quando uma caixa de diálogo é fechada ou quando o usuário faz logoff do serviço de autenticação do Primetime.

### Seleção e logon do provedor de conteúdo

Durante a autenticação com a autenticação do Primetime, duas novas atividades, `MvpdPickerActivity` e `MvpdLoginActivity`, permitem que o usuário selecione o provedor de conteúdo e o logon. Ambas as atividades são iniciadas do `CatalogActivity` por meio do `EntitlementManager`. Além disso, os resultados `MvpdPickerActivity` e `MvpdLoginActivity` retornam para `CatalogActivity` e, portanto, `CatalogActivity` devem substituir o método `Activity.onActivityResult`.

### Botão Fazer logon

A atividade principal da Implementação de referência, o `CatalogActivity`, inclui um novo botão &quot;Fazer logon&quot; em sua barra de ação. O botão Conectar permite que o usuário inicie a autenticação com a autenticação do Primetime. Além disso, o usuário pode iniciar a autenticação selecionando um vídeo protegido para reprodução. O ícone do botão Conectar e o texto mudam, dependendo do status de autenticação do usuário, e o `CatalogActivity` contém código para atualizar o ícone do botão e o texto quando a página é atualizada. Para fazer isso, quando o `CatalogActivity` for iniciado, ele chamará `EntitlementManager.checkAuthentication()` para atualizar o status de autenticação do usuário.

### Direito ao conteúdo

Dentro do `CatalogView`, novos ícones são exibidos na parte superior do ícone do conteúdo para sinalizar o status de autorização do usuário para esse conteúdo. Por exemplo, se o usuário tiver autorização prévia para exibir um vídeo, um ícone de círculo verde será exibido sobre o conteúdo. No entanto, se o usuário não tiver autorização prévia para exibir o vídeo, um ícone de tecla será exibido. A exibição desses ícones é tratada em `ContentTileAdapter`, no entanto, a atualização de seu estado é iniciada a partir de `CatalogActivity` quando um retorno de chamada em `EntitlementManagerListener` é chamado.

### Reprodução de conteúdo

A reprodução de vídeo agora requer uma verificação de autorização pelo `EntitlementManager`. A chamada para `EntitlementManager.getAuthorization()` ocorre dentro de `CatalogView`. Se o vídeo exigir autorização e o usuário estiver autorizado, o `PlayerActivity` será iniciado no `CatalogActivity`.

