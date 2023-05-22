---
title: Visão geral
description: Visão geral
copied-description: true
exl-id: 67c3d98f-8c17-4b5a-8abb-00f6f0f1e823
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Visão geral {#overview}

*Empacotamento* refere-se ao processo de criptografia e aplicação de uma política a arquivos FLV ou F4V. Use as APIs de empacotamento de mídia para empacotar arquivos. O SDK do Java do Adobe Access só pode empacotar Flash de download progressivo e conteúdo AIR, como FLV, F4V e MP4. Para empacotar conteúdo usando o DRM de acesso do Adobe para outros formatos de conteúdo, como o HTTP Dynamic Streaming Adobe (HDS) ou o Apple HTTP Live Streaming (HLS), será necessário usar outras ferramentas, como o Adobe Medium Server ( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html)) ou um codificador que implemente o SDK de transmissão do Adobe ( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf)). Como alternativa, os clientes têm a opção de usar o conjunto de ferramentas Java Primetime Packager do Adobe, que pode empacotar conteúdo para vários formatos de destino, como HDS, HLS e DASH.

O empacotamento é dissociado do servidor de licenças. Não há necessidade de o empacotador se conectar ao servidor de licenças para trocar informações sobre o conteúdo. Tudo o que o servidor de licenças precisa saber para emitir a licença está incluído nos metadados do conteúdo.

Quando um arquivo é criptografado, seu conteúdo não pode ser analisado sem a licença apropriada. O Adobe Access permite selecionar quais partes do arquivo serão criptografadas. Como o Adobe® Access™ pode analisar o formato de arquivo do conteúdo FLV e F4V, ele pode criptografar de forma inteligente partes seletivas do arquivo, em vez de todo o arquivo como um todo. Dados como metadados e pontos de sinalização podem permanecer não criptografados para que os mecanismos de pesquisa ainda possam pesquisar o arquivo.

É possível que um determinado conteúdo tenha várias políticas. Isso pode ser útil, por exemplo, se você quiser licenciar conteúdo em diferentes modelos de negócios sem precisar empacotar o conteúdo várias vezes. Por exemplo, você pode permitir o acesso anônimo por um curto período e, depois disso, permitir que o cliente compre o conteúdo e tenha acesso ilimitado. Se o conteúdo for empacotado usando várias políticas, o License Server deverá implementar uma lógica para selecionar qual política usar para emitir uma licença.

>[!NOTE]
>
>A arquitetura permite que as políticas de uso sejam especificadas e vinculadas ao conteúdo quando este for empacotado. Antes que um cliente possa reproduzir o conteúdo, ele deve adquirir uma licença para esse computador. A licença especifica as regras de uso aplicadas e fornece a chave usada para descriptografar o conteúdo. A política é um modelo para gerar a licença, mas o servidor de licença pode optar por substituir as regras de uso ao emitir a licença. Observe que a licença pode ser invalidada por restrições, como horas de expiração ou janelas de reprodução.

Há várias opções disponíveis ao empacotar conteúdo. Eles são especificados na `DRMParameters` interface e as classes que implementam essa interface, que são as `F4VDRMParameters` e `FLVDRMParameters`. Com essas classes, você pode definir parâmetros de assinatura e chave, bem como indicar se deve criptografar o conteúdo de áudio, conteúdo de vídeo ou dados de script. Para ver como elas são implementadas na implementação de referência, consulte as descrições das opções de linha de comando do Media Packager discutidas em *Uso das implementações de referência de acesso ao Adobe*. Essas opções são baseadas na API do Java e, portanto, estão disponíveis para uso programático.

As opções de empacotamento incluem:

* Opções de criptografia (áudio, vídeo, criptografia parcial).
* URL do servidor de licenças (o cliente usa isso como URL base para todas as solicitações enviadas ao servidor de licenças)
* Certificado de transporte do servidor de licenças
* Certificado do servidor de licenças, usado para criptografar o CEK.
* Credencial do empacotador para assinar metadados

O Acesso ao Adobe fornece uma API para passagem no CEK. Se nenhum CEK for especificado, o SDK o gerará aleatoriamente. Normalmente, você precisa de um CEK diferente para cada conteúdo. No entanto, no Dynamic Streaming, você provavelmente usaria o mesmo CEK para todos os arquivos desse conteúdo, de modo que o usuário só precisa de uma única licença e pode fazer a transição sem problemas de uma taxa de bits para outra. Para usar a mesma chave e licença para vários conteúdos, passe o mesmo `DRMParameters` objeto para `MediaEncrypter.encryptContent()`ou passe no CEK usando `V2KeyParameters.setContentEncryptionKey()`. Para usar uma chave e licença diferentes para cada conteúdo, crie um novo `DRMParameters` para cada arquivo.

Ao empacotar conteúdo usando a rotação de chaves, você pode controlar as Teclas de rotação usadas e a frequência com que elas mudam. `F4VDRMParameters` e `FLVDRMParameters` implementar a `KeyRotationParameters` interface. Por meio dessa interface, é possível ativar a rotação de chaves. Também é necessário especificar um `RotatingContentEncryptionKeyProvider`. Para cada amostra criptografada, essa classe determina a Chave de rotação a ser usada. Você pode implementar seu próprio provedor ou usar o `TimeBasedKeyProvider` incluído no SDK. Essa implementação gera aleatoriamente uma nova chave após um número especificado de segundos.

Em alguns casos, pode ser necessário armazenar os metadados do conteúdo como um arquivo separado e disponibilizá-los ao cliente separadamente do conteúdo. Para fazer isso, chame `MediaEncrypter.encryptContent()`, que retorna um `MediaEncrypterResult` objeto. Chame `MediaEncrypterResult.getKeyInfo()` e converter o resultado em `V2KeyStatus`. Em seguida, recupere os metadados de conteúdo e armazene-os em um arquivo.

Todas essas tarefas podem ser realizadas usando a API do Java. Para obter detalhes sobre a API Java discutida neste capítulo, consulte *Referência da API de acesso do Adobe*.

Para obter informações sobre a implementação de referência do Media Packager, consulte *Uso das implementações de referência de acesso ao Adobe*.
