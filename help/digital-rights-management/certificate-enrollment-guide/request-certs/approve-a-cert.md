---
title: Aprovar um certificado (Administrador de conta ou secundário)
description: Aprovar um certificado (Administrador de conta ou secundário)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---


# Aprovar um certificado (Administrador de Conta ou Secundário){#approve-a-certificate-account-or-secondary-administrator}

1. Efetue logon no site Inscrição de certificados.
1. Selecione a guia **[!UICONTROL Certificates]**.
1. Revise a solicitação para verificar se ela é válida.
1. Se a solicitação for válida, clique em **[!UICONTROL Approve]**.

   Você também pode adicionar um comentário. Um e-mail é enviado ao Solicitante declarando que a solicitação foi aprovada por um dos administradores da empresa. Uma cópia deste e-mail é enviada para a empresa e os administradores do Adobe.

1. Se a solicitação não for válida, clique em **[!UICONTROL Reject]** e insira um comentário na caixa de diálogo de confirmação.

   Um e-mail é enviado ao Solicitante declarando que a solicitação foi rejeitada por um dos administradores da empresa. Uma cópia deste e-mail é enviada aos administradores da empresa.

Quando um administrador aprova uma solicitação de certificado, o Adobe verifica a identidade do solicitante. O Adobe entra em contato com o Solicitante no número de telefone listado em seu perfil.

O administrador do Adobe tenta entrar em contato com o Requester duas vezes em um período de três dias. Se o administrador do Adobe não conseguir entrar em contato com o Requerente, ele deixará uma mensagem solicitando uma chamada de retorno ou fornecerá um horário em que ele fará uma chamada novamente. Se o administrador do Adobe não conseguir acessar o Solicitante, um email será enviado para os administradores do .

>[!NOTE]
>
>Somente os administradores Conta e Secundário podem alterar o número de telefone da empresa e a frase de desafio do Requerente.

Se a identidade do solicitante for verificada, o solicitante receberá um email contendo o arquivo PKCS#7 ( [!DNL p7b]).

O Requerente pode copiar o conteúdo PKCS#7 do corpo do email e salvá-lo em um arquivo ou usar o arquivo anexado ao email. O Adobe recomenda que, ao salvar o arquivo PKSC#7, você use o nome básico usado para gerar a chave privada e o arquivo CSR.

>[!NOTE]
>
>O arquivo enviado para o solicitante contém somente o certificado. O arquivo não contém informações de chave privada.

