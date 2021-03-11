---
title: Visão geral dos arquivos de mídia de empacotamento
description: Visão geral dos arquivos de mídia de empacotamento
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---


# Visão geral {#packaging-media-files-overview}

Empacotamento refere-se ao processo de criptografia e aplicação de uma política de DRM ao conteúdo de vídeo. Você pode usar as APIs de empacotamento de mídia para empacotar arquivos. O SDK Java de DRM do Primetime só pode empacotar conteúdo de download progressivo, como MP4.

>[!NOTE]
>
>Entre em contato com o representante de DRM do Primetime para saber como selecionar a opção de empacotamento mais apropriada para o formato de mídia e casos de uso.

O empacotamento é dissociado do servidor de licenças. Não há necessidade de o empacotador se conectar ao servidor de licenças para trocar quaisquer informações sobre o conteúdo. Tudo o que o servidor de licenças precisa saber para emitir uma licença está incluído nos metadados do conteúdo.

Quando um arquivo é criptografado, seu conteúdo não pode ser analisado sem a licença apropriada. Você pode usar o DRM do Primetime para selecionar as partes do arquivo que deseja criptografar. Como o DRM do Primetime pode analisar o formato de arquivo do conteúdo de vídeo, ele pode criptografar de forma inteligente partes seletivas de um arquivo em vez de um arquivo inteiro. Os dados, como metadados e pontos de sinalização, podem permanecer não criptografados para que os mecanismos de pesquisa ainda possam pesquisar o arquivo.

Um conteúdo especificado pode ter várias políticas de DRM. Por exemplo, você pode licenciar conteúdo em diferentes modelos de negócios sem precisar compactar o conteúdo várias vezes. Além disso, você pode permitir o acesso anônimo por um curto período de tempo e, em seguida, permitir que o cliente compre o conteúdo para ter acesso ilimitado. Se o conteúdo for empacotado usando várias políticas de DRM, o License Server deverá implementar a lógica para selecionar qual política de DRM deve ser usada para emitir uma licença.

>[!NOTE]
>
>A arquitetura permite que as políticas de DRM de uso sejam especificadas e vinculadas ao conteúdo quando o conteúdo for empacotado. Antes de um cliente poder reproduzir o conteúdo, ele deve adquirir uma licença para um computador especificado. A licença especifica as regras de uso que são aplicadas e fornece a chave que deve ser usada para descriptografar conteúdo. A política de DRM representa um template para gerar uma licença. No entanto, o servidor de licenças pode substituir as regras de uso ao emitir uma licença. A licença pode ser renderizada por tais restrições, como tempos de expiração ou janelas de reprodução.

O DRM do Primetime fornece uma API para transmitir o CEK. Se nenhum CEK for especificado, o SDK o gerará aleatoriamente. Normalmente, você precisa de um CEK diferente para cada seção de conteúdo. No entanto, no Dynamic Streaming, é provável que você use o mesmo CEK para todos os arquivos que compõem esse conteúdo. Portanto, um usuário precisa apenas de uma licença única para fazer a transição sem interrupções de uma taxa de bits para outra. Se quiser usar a mesma chave e licença para vários conteúdos, será necessário transmitir o mesmo objeto `DRMParameters` para `MediaEncrypter.encryptContent()` ou transmitir no CEK usando `V2KeyParameters.setContentEncryptionKey()`. Se quiser usar uma chave e uma licença diferentes para cada seção de conteúdo, será necessário criar uma nova instância `DRMParameters` para cada arquivo.

Ao empacotar o conteúdo usando a rotação de teclas, você pode controlar as teclas de rotação usadas e a frequência com que as teclas são alteradas. `F4VDRMParameters` e  `FLVDRMParameters` implementar a  `KeyRotationParameters` interface. Por meio dessa interface, é possível ativar a rotação de chaves. Você também precisa especificar um `RotatingContentEncryptionKeyProvider`. Para cada amostra criptografada, essa classe determina a Chave de rotação a ser usada. Você pode implementar seu próprio provedor ou usar o `TimeBasedKeyProvider` incluído no SDK. Essa implementação gera aleatoriamente uma nova chave após um número especificado de segundos.

Em alguns casos, pode ser necessário armazenar os metadados do conteúdo como um arquivo separado e disponibilizá-los ao cliente separadamente do conteúdo. Nesse caso, você precisa invocar `MediaEncrypter.encryptContent()`, que retorna um objeto `MediaEncrypterResult`. Chame `MediaEncrypterResult.getKeyInfo()` e converta o resultado em `V2KeyStatus`. Em seguida, recupere os metadados do conteúdo e armazene-os em um arquivo.

Todas essas tarefas podem ser realizadas com a API do Java.

Consulte *Referência da API DRM do Adobe Primetime* para obter detalhes sobre a API do Java.

Consulte *Usando as Implementações de Referência de DRM do Adobe Primetime* para obter informações sobre a implementação de referência do Media Packager.
