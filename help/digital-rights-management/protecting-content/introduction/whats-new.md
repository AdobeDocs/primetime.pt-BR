---
description: O Adobe Primetime DRM é uma Digital Rights Management avançada (DRM) e uma solução de proteção de conteúdo para conteúdo audiovisual de alto valor. Em aplicativos que suportam a criação de APIs Java, você pode usar o SDK DRM Primetime para especificar políticas DRM, aplicar essas políticas ao conteúdo e criptografar esse conteúdo.
seo-description: O Adobe Primetime DRM é uma Digital Rights Management avançada (DRM) e uma solução de proteção de conteúdo para conteúdo audiovisual de alto valor. Em aplicativos que suportam a criação de APIs Java, você pode usar o SDK DRM Primetime para especificar políticas DRM, aplicar essas políticas ao conteúdo e criptografar esse conteúdo.
seo-title: Novidades do Adobe Primetime DRM
title: Novidades do Adobe Primetime DRM
uuid: 3c8da594-a231-4496-bffc-130775ecae50
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Novidades no Adobe Primetime DRM{#what-is-new-in-adobe-primetime-drm}

O Adobe Primetime DRM é uma Digital Rights Management avançada (DRM) e uma solução de proteção de conteúdo para conteúdo audiovisual de alto valor. Em aplicativos que suportam a criação de APIs Java, você pode usar o SDK DRM Primetime para especificar políticas DRM, aplicar essas políticas ao conteúdo e criptografar esse conteúdo.

>[!NOTE]
>
>O Primetime DRM era anteriormente chamado de Adobe Access, e antes disso, Flash Access.

Esta é uma caminhada de alto nível do processo de proteção de conteúdo:

1. Use as APIs Java DRM para definir as propriedades da política DRM e os parâmetros de criptografia.
1. Crie uma política de DRM que descreva as funções de uso de qualquer conteúdo.

   Você pode criar qualquer número de políticas de DRM. A maioria dos usuários cria um pequeno número de políticas e as aplica a muitos arquivos.
1. Empacote um arquivo de mídia.

   *`Packaging a file`* significa que você criptografa o arquivo e, em seguida, aplica uma política de DRM ao arquivo.
1. Implemente o servidor de licenças para emitir uma licença para o usuário.

Com a conclusão dessas etapas, seu conteúdo criptografado está pronto para implantação. Após a implantação, um cliente pode solicitar uma licença do servidor de licença e, após o recebimento, o conteúdo pode ser reproduzido.

O SDK do DRM Primetime fornece uma API Java para concluir essas tarefas. O SDK inclui implementações de referência do servidor de licenças e ferramentas de linha de comando, ambas baseadas nas APIs Java do SDK do DRM.

Os recursos descritos abaixo são novos nesta versão.

## Novos recursos {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **Parada sólida -** Você pode especificar se a reprodução para ou continua no final de uma janela de reprodução.
* **Controles de saída dependentes de resolução -** Você pode especificar restrições de saída com base em resoluções de pixel.
* **Anonimização das Respostas do License Server -** Para melhorar a privacidade com os protocolos do Primetime DRM License Server, o número de série do certificado de transporte será zerado para as respostas do servidor de licenças aos clientes que o suportam.

