---
description: O Adobe Primetime DRM é uma solução de Digital Rights Management avançada (DRM) e proteção de conteúdo para conteúdo audiovisual de alto valor. Em aplicativos que oferecem suporte à criação de APIs Java, você pode usar o SDK do DRM do Primetime para especificar políticas de DRM, aplicar essas políticas ao conteúdo e criptografar esse conteúdo.
title: Novidades no Adobe Primetime DRM
exl-id: 998dae80-b3d3-419e-8fd3-d925a83d8b53
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Novidades no Adobe Primetime DRM{#what-is-new-in-adobe-primetime-drm}

O Adobe Primetime DRM é uma solução de Digital Rights Management avançada (DRM) e proteção de conteúdo para conteúdo audiovisual de alto valor. Em aplicativos que oferecem suporte à criação de APIs Java, você pode usar o SDK do DRM do Primetime para especificar políticas de DRM, aplicar essas políticas ao conteúdo e criptografar esse conteúdo.

>[!NOTE]
>
>O Primetime DRM era anteriormente chamado de Adobe Access e, antes disso, Flash Access.

Esta é uma apresentação de alto nível do processo de proteção de conteúdo:

1. Use as APIs Java do DRM para definir as propriedades da política do DRM e os parâmetros de criptografia.
1. Crie uma política DRM que descreva as funções de uso para qualquer conteúdo.

   É possível criar qualquer número de políticas DRM. A maioria dos usuários cria um pequeno número de políticas e as aplica a muitos arquivos.
1. Compactar um arquivo de mídia.

   *`Packaging a file`* significa que você criptografa o arquivo e aplica uma política DRM ao arquivo.
1. Implemente o servidor de licenças para emitir uma licença para o usuário.

Com a conclusão dessas etapas, o conteúdo criptografado estará pronto para implantação. Após a implantação, um cliente pode solicitar uma licença do servidor de licenças e, no recebimento, pode reproduzir o conteúdo.

O SDK do DRM do Primetime fornece uma API Java para concluir essas tarefas. O SDK inclui implementações de referência do servidor de licenças e ferramentas de linha de comando, ambas baseadas nas APIs Java do SDK do DRM.

Os recursos descritos abaixo são novos nesta versão.

## Novos recursos {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **Parada fixa -** Você pode especificar se a reprodução pára ou continua no final de uma janela de reprodução.
* **Controles de saída dependentes de resolução -** Você pode especificar restrições de saída com base nas resoluções de pixel.
* **Anonimização de Respostas do License Server -** Para aprimorar a privacidade com os protocolos do servidor de licenças DRM Primetime, o número de série do certificado de transporte será zerado para as respostas do servidor de licenças aos clientes de suporte.
