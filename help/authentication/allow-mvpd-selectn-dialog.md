---
title: Permitir MVPDs na Caixa de Diálogo de Seleção
description: Permitir MVPDs na Caixa de Diálogo de Seleção
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# Permitir MVPDs na Caixa de Diálogo de Seleção {#allow-mvpds-selection-dialog}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Problema {#issue}

O Programador pode testar ou verificar a experiência do usuário de novas integrações MVPD antes de ir ao público para os usuários finais.

## Solução {#solution}

No `displayProviderDialog()` retorno de chamada, a autenticação do Adobe Primetime retorna todos os MVPDs integrados ao Programador selecionado (ID do Solicitante). Mas o Programador pode aplicar um filtro na matriz de retorno de MVPDs e exibir apenas aqueles que estão em ambas as listas.

## Exemplo {#example}

Este exemplo demonstra como exibir somente CableCompany_1 e CableCompany_2 na caixa de diálogo do seletor MVPD e não mostrar CableCompany_NewIntegration.

```C
function displayProviderDialog(mvpdList) {
    var allowlisted = new Array();
    for (var i = 0; i < mvpdList.length; i = i + 1) {
        var currentMvpd = mvpdList[i];
        if ( isAllowListed(currentMvpd.ID) ) {
            allowlisted.push(currentMvpd);
        }
    }
    displayAllowlisted(allowlisted);
}

function isAllowListed(mvpdID) {
    // Implement allowlisting on MVPD IDs.
    return (mvpdID === 'CableCompany_1' || mvpdID === 'CableCompany_2');
}

function displayAllowlisted(list) {
    // TODO: Implement site-specific logic here.
}
```

<!--
**Related Information**
* [Prevent MVPDs from appearing in the Selection Dialog](/help/authentication/prevent-mvpd-selectn-dialog.md)
* **Code Samples**
* [Programmer integration guide](/help/authentication/programmer-integration-guide-overview.md)
-->