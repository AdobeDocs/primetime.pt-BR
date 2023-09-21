---
title: Lista de atualização de política
description: Lista de atualização de política
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Lista de atualização de política {#policy-update-list}

Você pode usar Listas de Atualização de Políticas para comunicar alterações de políticas a um Servidor de Licenças. Se uma política for modificada depois de ser usada para empacotar conteúdo, é desejável que o Servidor de Licenças esteja ciente da versão mais recente da política, para que a versão possa ser usada para emitir uma licença.

Para criar uma Lista de Atualização de Política pela primeira vez, clique em **[!UICONTROL Add policies]** para exibir todas as políticas disponíveis no servidor. Para quaisquer políticas que foram atualizadas desde que foram usadas para criar o pacote de conteúdo, selecione a **[!UICONTROL update]** botão de opção.

Se você não quiser mais usar uma política para emitir licenças e a política já tiver sido usada para empacotar conteúdo, talvez você queira revogar a política. Para fazer isso, selecione o **[!UICONTROL revoke]** botão de opção. Quando as políticas desejadas tiverem sido selecionadas, escolha **[!UICONTROL Create Policy Update List]**. Um arquivo chamado [!DNL PolicyUpdateList.dat] será salvo na variável [!DNL Resources] Diretório.

Para modificar uma Lista de Atualização de Política existente, clique em **[!UICONTROL Add policies]** para exibir todas as políticas disponíveis no servidor. Escolha as políticas adicionais para adicionar ou revogar. As entradas existentes na Lista de atualização de política podem ser alteradas na seção superior da tela. Políticas marcadas **[!UICONTROL updated]** pode ser alterado para **[!UICONTROL revoked]**, mas quando uma política é **[!UICONTROL revoked]**, não pode ser alterado novamente para **[!UICONTROL updated]**.

Quando as alterações desejadas tiverem sido feitas, escolha **[!UICONTROL Create Policy Update List]**, e o [!DNL PolicyUpdateList.dat] arquivo é gerado novamente. Se uma política já estiver na lista de atualização de política e tiver sido atualizada desde a última vez que a lista foi gerada, a versão mais recente da política será usada quando a Lista de Atualização de Política for gerada novamente.
