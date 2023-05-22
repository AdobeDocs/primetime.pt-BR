---
title: Visão geral dos arquivos de mídia de empacotamento
description: Visão geral dos arquivos de mídia de empacotamento
copied-description: true
exl-id: 88c593a7-33b5-4773-b283-2ab16f9e8c3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---

# Visão geral {#packaging-media-files-overview}

Empacotamento refere-se ao processo de criptografia e aplicação de uma política de DRM ao conteúdo de vídeo. Você pode usar as APIs de empacotamento de mídia para empacotar arquivos. O SDK do Java DRM do Primetime só pode empacotar conteúdo de download progressivo, como MP4.

>[!NOTE]
>
>Entre em contato com o representante do Primetime DRM sobre como selecionar a opção de pacote mais apropriada para o formato de mídia e casos de uso.

O empacotamento é dissociado do servidor de licenças. Não há necessidade de o empacotador se conectar ao servidor de licenças para trocar informações sobre o conteúdo. Tudo o que o servidor de licenças precisa saber para emitir uma licença está incluído nos metadados do conteúdo.

Quando um arquivo é criptografado, seu conteúdo não pode ser analisado sem a licença apropriada. Você pode usar o Primetime DRM para selecionar as partes do arquivo que deseja criptografar. Como o Primetime DRM pode analisar o formato de arquivo do conteúdo de vídeo, ele pode criptografar de forma inteligente partes seletivas de um arquivo, em vez de um arquivo inteiro. Os dados, como metadados e pontos de sinalização, podem permanecer não criptografados para que os mecanismos de pesquisa ainda possam pesquisar o arquivo.

Um conteúdo especificado pode ter várias políticas de DRM. Por exemplo, você pode licenciar o conteúdo em diferentes modelos de negócios sem precisar empacotar o conteúdo várias vezes. Além disso, você pode permitir o acesso anônimo por um curto período e permitir que o cliente compre o conteúdo para ter acesso ilimitado. Se o conteúdo for empacotado com o uso de várias políticas de DRM, o License Server deverá implementar uma lógica para selecionar qual política de DRM deverá ser usada para emitir uma licença.

>[!NOTE]
>
>A arquitetura permite que as políticas de DRM de uso sejam especificadas e vinculadas ao conteúdo quando o conteúdo for empacotado. Para que um cliente possa reproduzir o conteúdo, ele deve adquirir uma licença para um computador especificado. A licença especifica as regras de uso aplicadas e fornece a chave que deve ser usada para descriptografar o conteúdo. A política DRM representa um modelo para gerar uma licença. No entanto, o servidor de licenças pode substituir as regras de uso ao emitir uma licença. A licença pode ser invalidada por essas restrições, como horas de expiração ou janelas de reprodução.

O DRM do Primetime fornece uma API para transmissão no CEK. Se nenhum CEK for especificado, o SDK o gerará aleatoriamente. Normalmente, você precisa de um CEK diferente para cada seção do conteúdo. No entanto, no Dynamic Streaming, é provável que você use o mesmo CEK para todos os arquivos que compõem esse conteúdo. Portanto, um usuário só precisa de uma única licença para fazer a transição perfeita de uma taxa de bits para outra. Se quiser usar a mesma chave e licença para vários conteúdos, você precisará passar a mesma `DRMParameters` objeto para `MediaEncrypter.encryptContent()`ou passe no CEK usando `V2KeyParameters.setContentEncryptionKey()`. Se quiser usar uma chave e licença diferentes para cada seção do conteúdo, será necessário criar um novo `DRMParameters` para cada arquivo.

Ao criar pacotes de conteúdo usando a rotação de chaves, você pode controlar as Teclas de rotação usadas e a frequência com que elas são alteradas. `F4VDRMParameters` e `FLVDRMParameters` implementar a `KeyRotationParameters` interface. Por meio dessa interface, é possível ativar a rotação de chaves. Também é necessário especificar um `RotatingContentEncryptionKeyProvider`. Para cada amostra criptografada, essa classe determina a Chave de rotação a ser usada. Você pode implementar seu próprio provedor ou usar o `TimeBasedKeyProvider` incluído no SDK. Essa implementação gera aleatoriamente uma nova chave após um número especificado de segundos.

Em alguns casos, pode ser necessário armazenar os metadados do conteúdo como um arquivo separado e disponibilizá-los ao cliente separadamente do conteúdo. Nesse caso, é necessário invocar `MediaEncrypter.encryptContent()`, que retorna um `MediaEncrypterResult` objeto. Chame `MediaEncrypterResult.getKeyInfo()` e converter o resultado em `V2KeyStatus`. Em seguida, recupere os metadados de conteúdo e armazene-os em um arquivo.

Todas essas tarefas podem ser realizadas com a API Java.

Consulte *Referência da API do Adobe Primetime DRM* para obter detalhes sobre a API do Java.

Consulte *Uso das implementações de referência do Adobe Primetime DRM* para obter informações sobre a implementação da referência do Media Packager.
