---
title: Impedir que os MVPDs apareçam na Caixa de Diálogo de Seleção
description: Impedir que os MVPDs apareçam na Caixa de Diálogo de Seleção
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Impedir que os MVPDs apareçam na Caixa de Diálogo de Seleção

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

## Problema {#issue-prevent-mvpd-sel-dialog}

Você precisa impedir que MVPDs específicos (&quot;lista de bloqueios&quot;) sejam exibidos no seletor de MVPD.


## Solução {#solution-prevent-mvpd-sel-dialog}

A solução é incluir uma lista de bloqueios quando `displayProviderDialog()` é chamado.

Por exemplo, se você desejar que CableCompany_1 e CableCompany_2 não sejam exibidos dentro do seletor de MVPD, você faria algo semelhante ao que é mostrado no exemplo a seguir.

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
