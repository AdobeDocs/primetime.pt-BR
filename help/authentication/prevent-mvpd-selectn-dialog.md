---
title: Impedir que MVPDs apareçam na caixa de diálogo de seleção
description: Impedir que MVPDs apareçam na caixa de diálogo de seleção
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Impedir que MVPDs apareçam na caixa de diálogo de seleção

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Problema {#issue-prevent-mvpd-sel-dialog}

Você precisa impedir que MVPDs específicos (&quot;lista de bloqueios&quot;) apareçam no seletor MVPD.


## Solução {#solution-prevent-mvpd-sel-dialog}

A solução é fazer uma lista de bloqueios quando `displayProviderDialog()` é chamado.

Por exemplo, se você quiser que CableCompany_1 e CableCompany_2 não sejam mostradas dentro do seletor MVPD, você faria algo como o mostrado no exemplo a seguir.

```C
function displayProviderDialog(mvpdList) {
    var allowlisted = new Array();
    for (var i = 0; i < mvpdList.length; i = i + 1) {
        var currentMvpd = mvpdList[i];
        if (!isBlocklisted(currentMvpd.ID)) {
            allowlisted.push(currentMvpd);
        }
    }
    displayAllowlisted(allowlisted);
}

function isBlocklisted(mvpdID) {
    // Implement block-listing on MVPD IDs.
    return (mvpdID === 'CableCompany_1' || mvpdID === 'CableCompany_2');
}

function displayAllowlisted(list) {
    // TODO: Implement site-specific logic here.
} 
```

<!--
**Related Information**

* [Allow MVPDs in the Selection Dialog](/help/authentication/allow-mvpd-selectn-dialog.md)
* **Code samples**
* [Programmer integration guide](/help/authentication/programmer-integration-guide-overview.md)
-->