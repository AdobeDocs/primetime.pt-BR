---
title: Aprovar um certificado (Administrador de Conta ou Secundário)
description: Aprovar um certificado (Administrador de Conta ou Secundário)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Aprovar um certificado (Administrador de Conta ou Secundário){#approve-a-certificate-account-or-secondary-administrator}

1. Faça logon no site de Registro de Certificado.
1. Selecione o **[!UICONTROL Certificates]** guia.
1. Revise a solicitação para verificar se ela é válida.
1. Se a solicitação for válida, clique em **[!UICONTROL Approve]**.

   Você também pode adicionar um comentário. Um e-mail é enviado ao Solicitante informando que a solicitação foi aprovada por um dos administradores da empresa. Uma cópia desse e-mail é enviada à empresa e aos administradores do Adobe.

1. Se a solicitação não for válida, clique em **[!UICONTROL Reject]** e insira um comentário na caixa de diálogo de confirmação.

   Um e-mail é enviado ao Solicitante informando que a solicitação foi rejeitada por um dos administradores da empresa. Uma cópia deste email é enviada aos administradores da empresa.

Quando um administrador aprova uma solicitação de certificado, o Adobe verifica a identidade do Solicitante. Adobe entra em contato com o Solicitante no número de telefone listado em seu perfil.

O administrador de Adobe tenta entrar em contato com o Solicitante duas vezes dentro de um período de três dias. Se o administrador do Adobe não conseguir entrar em contato com o Solicitante, ele deixará uma mensagem solicitando um retorno de chamada ou fornecerá um horário para fazer uma nova chamada. Se o administrador de Adobe não conseguir acessar o Solicitante, um e-mail será enviado aos administradores.

>[!NOTE]
>
>Somente os administradores de Conta e Secundário podem alterar o número de telefone da empresa e a frase desafiadora do Solicitante.

Se a identidade do Solicitante for verificada, ele receberá um e-mail contendo o arquivo PKCS#7 ( [!DNL p7b]).

O Solicitante pode copiar o conteúdo PKCS#7 do corpo do email e salvá-lo em um arquivo ou usar o arquivo anexado ao email. A Adobe recomenda que, ao salvar o arquivo PKSC#7, você use o nome base usado para gerar a chave privada e o arquivo CSR.

>[!NOTE]
>
>O arquivo enviado ao Solicitante contém somente o certificado. O arquivo não contém informações de chave privada.
