---
description: O Gerenciador de direitos é o gerenciador de recursos que suporta a implementação da autenticação Primetime.
seo-description: O Gerenciador de direitos é o gerenciador de recursos que suporta a implementação da autenticação Primetime.
seo-title: Visão geral do Gerenciador de direitos
title: Visão geral do Gerenciador de direitos
uuid: b33dfae3-a132-4215-9992-80cbf4c87a61
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Visão Geral do Gerenciador de Direitos {#entitlement-manager-overview}

O Gerenciador de direitos é o gerenciador de recursos que suporta a implementação da autenticação Primetime.

## Visão geral do recurso

A integração de autenticação Primetime com a Implementação de referência do SDK do Android Primetime adiciona um novo gerenciador de recursos ao aplicativo. No entanto, diferentemente de muitos dos outros gerenciadores de recursos, *o EntitlementManager é usado em vários locais em todo o aplicativo*. A seguir, é apresentada uma visão geral das alterações e adições feitas à Implementação de referência para suportar a autenticação do Primetime:

### Classe EntitlementManager

A classe `EntitlementManager` lida com toda a comunicação com o SDK de autenticação Primetime, além de encapsular a lógica do aplicativo necessária para os workflows de direito. A API pública do `EntitlementManager` é usada pelo aplicativo para iniciar workflows de direito, enquanto a interface `EntitlementMangerListener` fornece um mecanismo de retorno de chamada para o aplicativo manipular eventos `EntitlementManger`.

### Retornos de chamada do EntitlementManger

A atividade principal da Implementação de referência, `CatalogActivity`, cria uma instância de `EntitlementManagerListener` e a registra com o `EntitlementManager`. Dessa forma, o `EntitlementManager` pode sinalizar as atualizações necessárias da interface do usuário para o restante do aplicativo. Os retornos de chamada incluem a exibição/ocultação de uma caixa de diálogo de carregamento, a exibição de caixas de diálogo de status, a atualização de ícones de autorização e autenticação e o início da reprodução do vídeo após uma autorização bem-sucedida.

### Caixas de diálogo de direito

A classe `EntitlementDialogFragment` gera mensagens de diálogo com base no status de direito passado para o construtor de classe. Essa classe é usada para mensagens de sucesso de autenticação, bem como para todas as mensagens de erro. O `CatalogActivity` exibe as caixas de diálogo de direito quando recebe eventos específicos do `EntitlementManager`. Além disso, o `CatalogActivity` implementa a interface `EntitlementDialogListener`, que inclui métodos de retorno de chamada para sinalizar quando uma caixa de diálogo é fechada ou quando o usuário faz logout do serviço de autenticação Primetime.

### Seleção e logon do provedor de conteúdo

Durante a autenticação com autenticação Primetime, duas novas atividades, `MvpdPickerActivity` e `MvpdLoginActivity`, permitem que o usuário selecione seu provedor de conteúdo e login. Ambas as atividades são iniciadas de `CatalogActivity` por meio de `EntitlementManager`. Além disso, os resultados de `MvpdPickerActivity` e `MvpdLoginActivity` retornam para `CatalogActivity` e, portanto, `CatalogActivity` devem substituir o método `Activity.onActivityResult`.

### Botão Entrar

A atividade principal da Implementação de referência, o `CatalogActivity`, inclui um novo botão &quot;Entrar&quot; em sua barra de ações. O botão Entrar permite que o usuário inicie a autenticação com a autenticação Primetime. Além disso, o usuário pode iniciar a autenticação selecionando um vídeo protegido para reprodução. O ícone e o texto do botão Entrar são alterados dependendo do status de autenticação do usuário e o `CatalogActivity` contém o código para atualizar o ícone e o texto do botão quando a página é atualizada. Para fazer isso, quando o `CatalogActivity` start, ele chama `EntitlementManager.checkAuthentication()` para atualizar o status de autenticação do usuário.

### Direito ao conteúdo

Dentro de `CatalogView`, novos ícones são exibidos na parte superior do ícone do conteúdo para sinalizar o status de autorização do usuário para esse conteúdo. Por exemplo, se o usuário estiver autorizado previamente a visualização de um vídeo, um ícone de círculo verde será exibido sobre o conteúdo. No entanto, se o usuário não estiver pré-autorizado a visualização do vídeo, um ícone de tecla será exibido. A exibição desses ícones é feita em `ContentTileAdapter`, no entanto, a atualização de seu estado é iniciada a partir de `CatalogActivity` quando um retorno de chamada em `EntitlementManagerListener` é chamado.

### Reprodução de conteúdo

A reprodução de vídeo agora requer uma verificação de autorização pelo `EntitlementManager`. A chamada para `EntitlementManager.getAuthorization()` ocorre dentro de `CatalogView`. Se o vídeo exigir autorização e o usuário estiver autorizado, `PlayerActivity` será iniciado a partir de `CatalogActivity`.

