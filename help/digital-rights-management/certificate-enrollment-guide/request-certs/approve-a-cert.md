---
description: nulo
seo-description: nulo
seo-title: Aprovar um certificado (Administrador da conta ou secundário)
title: Aprovar um certificado (Administrador da conta ou secundário)
uuid: 5b95e2e8-abe9-4aef-bcb4-9b98ba6604d1
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Aprovar um certificado (Administrador de conta ou secundário){#approve-a-certificate-account-or-secondary-administrator}

1. Efetue logon no site de Inscrição de Certificado.
1. Selecione a guia **[!UICONTROL Certificates]**.
1. Revise a solicitação para verificar se ela é válida.
1. Se a solicitação for válida, clique em **[!UICONTROL Approve]**.

   Você também pode adicionar um comentário. Um e-mail é enviado para o Solicitante declarando que a solicitação foi aprovada por um dos administradores da empresa. Uma cópia desse email é enviada aos administradores de empresa e Adobe.

1. Se a solicitação não for válida, clique em **[!UICONTROL Reject]** e insira um comentário na caixa de diálogo de confirmação.

   Um e-mail é enviado ao Requester informando que a solicitação foi rejeitada por um dos administradores da empresa. Uma cópia desse email é enviada aos administradores da empresa.

Quando um administrador aprova uma solicitação de certificado, o Adobe verifica a identidade do solicitante. Adobe entre em contato com o solicitante no número de telefone listado no perfil.

O administrador do Adobe tenta entrar em contato com o Solicitante duas vezes em um período de três dias. Se o administrador do Adobe não conseguir entrar em contato com o solicitante, ele deixará uma mensagem solicitando uma chamada de retorno ou fornecerá um horário em que ele fará uma chamada novamente. Se o administrador do Adobe não conseguir acessar o Solicitante, um email será enviado para os administradores.

>[!NOTE]
>
>Somente os administradores Conta e Secundário podem alterar o número de telefone da empresa e a frase de desafio do solicitante.

Se a identidade do solicitante for verificada, o solicitante receberá um email contendo o arquivo PKCS#7 ( [!DNL p7b]).

O solicitante pode copiar o conteúdo PKCS#7 do corpo do email e salvá-lo em um arquivo ou usar o arquivo anexado ao email. O Adobe recomenda que, ao salvar o arquivo PKSC#7, você use o nome básico usado para gerar a chave privada e o arquivo CSR.

>[!NOTE]
>
>O arquivo enviado ao solicitante contém apenas o certificado. O arquivo não contém informações de chave privada.

