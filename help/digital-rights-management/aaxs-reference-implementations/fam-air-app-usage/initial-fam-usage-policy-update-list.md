---
title: Lista de atualização de política
description: Lista de atualização de política
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Lista de atualização de política {#policy-update-list}

Você pode usar Listas de Atualização de Política para comunicar alterações de política a um Servidor de Licenças. Se uma política for modificada depois de ser usada para empacotar conteúdo, é desejável que o License Server esteja ciente da versão mais recente da política, para que essa versão possa ser usada para emitir uma licença.

Para criar uma Lista de Atualização de Política pela primeira vez, clique em **[!UICONTROL Add policies]** para exibir todas as políticas disponíveis no servidor. Para qualquer política que tenha sido atualizada desde que foi usada para empacotar conteúdo, selecione o botão de opção **[!UICONTROL update]**.

Se você não quiser mais usar uma política para emitir licenças e a política já tiver sido usada para empacotar conteúdo, poderá revogar a política. Para fazer isso, selecione o botão de opção **[!UICONTROL revoke]**. Quando as políticas desejadas tiverem sido selecionadas, escolha **[!UICONTROL Create Policy Update List]**. Um arquivo chamado [!DNL PolicyUpdateList.dat] será salvo no Diretório [!DNL Resources].

Para modificar uma Lista de Atualização de Política existente, clique em **[!UICONTROL Add policies]** para ver todas as políticas disponíveis no servidor. Escolha as políticas adicionais a serem adicionadas ou revogadas. As entradas existentes na Lista de Atualização de Políticas podem ser alteradas na seção superior da tela. As políticas marcadas **[!UICONTROL updated]** podem ser alteradas para **[!UICONTROL revoked]**, mas uma vez que a política seja **[!UICONTROL revoked]**, não poderá ser alterada de volta para **[!UICONTROL updated]**.

Quando as alterações desejadas forem feitas, escolha **[!UICONTROL Create Policy Update List]** e o arquivo [!DNL PolicyUpdateList.dat] será gerado novamente. Se uma política já estiver na lista de atualização de política e tiver sido atualizada desde a última vez que a lista foi gerada, a versão mais recente da política será usada quando a Lista de atualização de política for gerada novamente.
