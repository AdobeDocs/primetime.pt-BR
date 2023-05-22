---
description: O Gerenciador de direitos é o gerenciador de recursos que oferece suporte à implementação de autenticação do Primetime.
title: Visão geral do Gerenciador de direitos
exl-id: a66e131e-283f-4378-b834-7cfa887b3ec9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# Visão geral do Gerenciador de direitos {#entitlement-manager-overview}

O Gerenciador de direitos é o gerenciador de recursos que oferece suporte à implementação de autenticação do Primetime.

## Visão geral do recurso

A integração de autenticação do Primetime com a Implementação de referência do SDK do Android Primetime adiciona um novo gerenciador de recursos ao aplicativo. No entanto, ao contrário de muitos outros gerentes de recursos, *o EntitlementManager é usado em vários locais no aplicativo*. A seguir há uma visão geral das alterações e adições feitas na implementação de referência para oferecer suporte à autenticação do Primetime:

### Classe do EntitlementManager

A variável `EntitlementManager` A classe lida com toda a comunicação com o SDK de autenticação do Primetime, além de encapsular a lógica do aplicativo necessária para os workflows de direito. A variável `EntitlementManager`A API pública do é usada pelo aplicativo para iniciar workflows de direito, enquanto a `EntitlementMangerListener` fornece um mecanismo de retorno de chamada para o aplicativo manipular `EntitlementManger` eventos.

### Retornos de chamada do EntitlementManager

A atividade principal da implementação de referência, a `CatalogActivity`, cria uma instância de `EntitlementManagerListener` e registra-o com o `EntitlementManager`. Deste modo, a Comissão `EntitlementManager` pode sinalizar as atualizações de interface do usuário necessárias para o restante do aplicativo. Os retornos de chamada incluem exibir/ocultar uma caixa de diálogo de carregamento, exibir caixas de diálogo de status, atualizar ícones de autorização e autenticação e iniciar a reprodução de vídeo após a autorização bem-sucedida.

### Caixas de diálogo de direitos

A variável `EntitlementDialogFragment` A classe gera mensagens de caixa de diálogo com base no status de direito passado para o construtor de classe. Essa classe é usada para mensagens de sucesso de autenticação, bem como para todas as mensagens de erro. A variável `CatalogActivity` exibe as caixas de diálogo de direito quando recebe eventos específicos do `EntitlementManager`. Além disso, a `CatalogActivity` implementa o `EntitlementDialogListener` interface, que inclui métodos de retorno de chamada para sinalizar quando uma caixa de diálogo é fechada ou quando o usuário faz logoff do serviço de autenticação Primetime.

### Seleção e logon do provedor de conteúdo

Durante a autenticação com a autenticação do Primetime, duas novas atividades, `MvpdPickerActivity` e `MvpdLoginActivity`, permitem que o usuário selecione o provedor de conteúdo e faça logon. Ambas as atividades são iniciadas a partir do `CatalogActivity` por meio da `EntitlementManager`. Além disso, tanto o `MvpdPickerActivity` e `MvpdLoginActivity` retornar os resultados para o `CatalogActivity` e, por conseguinte, a `CatalogActivity` deve substituir o `Activity.onActivityResult` método.

### Botão Entrar

A atividade principal da implementação de referência, a `CatalogActivity`, inclui um novo botão &quot;Fazer logon&quot; em sua barra de ações. O botão Fazer logon permite que o usuário inicie a autenticação com a autenticação do Primetime. Além disso, o usuário pode iniciar a autenticação selecionando um vídeo protegido para reprodução. O ícone e o texto do botão Fazer logon serão alterados dependendo do status de autenticação do usuário e da `CatalogActivity` contém o código para atualizar o ícone e o texto do botão quando a página é atualizada. Para fazer isso, ao `CatalogActivity` inicia, chama `EntitlementManager.checkAuthentication()` para atualizar o status de autenticação do usuário.

### Direito de conteúdo

No prazo de `CatalogView`, novos ícones são exibidos na parte superior do ícone do conteúdo para sinalizar o status de autorização do usuário para esse conteúdo. Por exemplo, se o usuário estiver pré-autorizado a visualizar um vídeo, um ícone de círculo verde será exibido sobre o conteúdo. No entanto, se o usuário não estiver pré-autorizado a exibir o vídeo, um ícone de chave será exibido. A exibição desses ícones é tratada em `ContentTileAdapter`No entanto, a atualização do seu estado é iniciada a partir da `CatalogActivity` quando um retorno de chamada na `EntitlementManagerListener` é chamado.

### Reprodução de conteúdo

A reprodução de vídeo agora requer uma verificação de autorização pelo `EntitlementManager`. A chamada para `EntitlementManager.getAuthorization()` ocorre dentro de `CatalogView`. Se o vídeo exigir autorização e o usuário estiver autorizado, a variável `PlayerActivity` é iniciado a partir do `CatalogActivity`.
