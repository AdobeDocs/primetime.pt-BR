---
description: O Adobe Primetime DRM é uma solução avançada de Digital Rights Management (DRM) e proteção de conteúdo para conteúdo audiovisual de alto valor. Em aplicativos que oferecem suporte à criação de APIs Java, você pode usar o SDK de DRM do Primetime para especificar políticas de DRM, aplicar essas políticas ao conteúdo e criptografar esse conteúdo.
title: Novidades no Adobe Primetime DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Novidades no Adobe Primetime DRM{#what-is-new-in-adobe-primetime-drm}

O Adobe Primetime DRM é uma solução avançada de Digital Rights Management (DRM) e proteção de conteúdo para conteúdo audiovisual de alto valor. Em aplicativos que oferecem suporte à criação de APIs Java, você pode usar o SDK de DRM do Primetime para especificar políticas de DRM, aplicar essas políticas ao conteúdo e criptografar esse conteúdo.

>[!NOTE]
>
>O DRM do Primetime era anteriormente chamado de Adobe Access e, antes disso, Flash Access.

Veja a seguir um guia de alto nível do processo de proteção de conteúdo:

1. Use as APIs do DRM Java para definir as propriedades da política de DRM e os parâmetros de criptografia.
1. Crie uma política de DRM que descreva as funções de uso de qualquer conteúdo.

   Você pode criar qualquer número de políticas de DRM. A maioria dos usuários cria um pequeno número de políticas e as aplica a muitos arquivos.
1. Compacte um arquivo de mídia.

   *`Packaging a file`* significa que você criptografa o arquivo e, em seguida, aplica uma política de DRM ao arquivo.
1. Implemente o servidor de licenças para emitir uma licença para o usuário.

Com a conclusão dessas etapas, o conteúdo criptografado estará pronto para implantação. Após a implantação, um cliente pode solicitar uma licença do servidor de licenças e, após o recebimento, pode reproduzir o conteúdo.

O SDK de DRM do Primetime fornece uma API Java para concluir essas tarefas. O SDK inclui implementações de referência do servidor de licenças e ferramentas de linha de comando, ambas baseadas nas APIs Java do SDK do DRM.

Os recursos descritos abaixo são novos nesta versão.

## Novos recursos {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **Parada permanente -** Você pode especificar se a reprodução é interrompida ou continua no final de uma janela de reprodução.
* **Controles de saída dependentes de resolução -** Você pode especificar restrições de saída com base em resoluções de pixel.
* **Anonimização das Respostas do License Server -** Para melhorar a privacidade com os protocolos do Primetime DRM License Server, o número de série do certificado de transporte será zerado para as respostas do servidor de licenças aos clientes de suporte.

