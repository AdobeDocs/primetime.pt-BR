---
seo-title: Lista de atualização de política
title: Lista de atualização de política
uuid: ecc74b66-5b53-4ec3-9641-8b78929e2932
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lista de atualização de política {#policy-update-list}

Você pode usar Listas de Atualização de Política para comunicar alterações de política a um Servidor de Licenças. Se uma política for modificada depois de usada para empacotar conteúdo, é desejável que o License Server esteja ciente da versão mais recente da política, para que essa versão possa ser usada para emitir uma licença.

Para criar uma Lista de atualizações de políticas pela primeira vez, clique em **[!UICONTROL Add policies]** para exibir todas as políticas disponíveis no servidor. Para quaisquer políticas que foram atualizadas desde que foram usadas para empacotar conteúdo, selecione o botão de opção **[!UICONTROL update]** .

Se você não quiser mais usar uma política para emitir licenças e a política já tiver sido usada para disponibilizar conteúdo, revogue a política. Para fazer isso, selecione o botão de **[!UICONTROL revoke]** opção. Quando as políticas desejadas forem selecionadas, escolha **[!UICONTROL Create Policy Update List]**. Um arquivo chamado [!DNL PolicyUpdateList.dat] será salvo no [!DNL Resources] Diretório.

Para modificar uma Lista de Atualização de Política existente, clique em **[!UICONTROL Add policies]** para exibir todas as políticas disponíveis no servidor. Escolha as políticas adicionais a serem adicionadas ou revogadas. As entradas existentes na Lista de atualizações de políticas podem ser alteradas na seção superior da tela. As políticas marcadas **[!UICONTROL updated]** podem ser alteradas para **[!UICONTROL revoked]**, mas uma vez que uma política é **[!UICONTROL revoked]**, ela não pode ser alterada de volta para **[!UICONTROL updated]**.

Quando as alterações desejadas forem feitas, escolha **[!UICONTROL Create Policy Update List]** e o [!DNL PolicyUpdateList.dat] arquivo será gerado novamente. Se uma política já estiver na lista de atualização de política e tiver sido atualizada desde a última vez que a lista foi gerada, a versão mais recente da política será usada quando a Lista de atualizações de política for gerada novamente.
