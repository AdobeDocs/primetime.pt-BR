---
title: Visão geral
description: Visão geral
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---


# Visão geral {#overview}

** Packaging refere-se ao processo de criptografia e aplicação de uma política para arquivos FLV ou F4V. Use as APIs de empacotamento de mídia para empacotar arquivos. O SDK Java do Adobe Access só pode empacotar conteúdo do Flash e do AIR para download progressivo, como FLV, F4V e MP4. Para empacotar conteúdo usando o DRM de acesso ao Adobe para outros formatos de conteúdo, como Adobe HTTP Dynamic Streaming (HDS) ou Apple HTTP Live Streaming (HLS), será necessário usar outras ferramentas, como Adobe Medium Server ( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html)) ou um codificador que implementa o SDK de Transmissão do Adobe ( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf)). Como alternativa, os clientes têm a opção de usar o Adobe, Java Primetime Packager, conjunto de ferramentas, que pode disponibilizar conteúdo para uma variedade de formatos de destino, como HDS, HLS e DASH.

O empacotamento é dissociado do servidor de licenças. Não há necessidade de o empacotador se conectar ao servidor de licenças para trocar quaisquer informações sobre o conteúdo. Tudo o que o servidor de licenças precisa saber para emitir a licença está incluído nos metadados do conteúdo.

Quando um arquivo é criptografado, seu conteúdo não pode ser analisado sem a licença apropriada. Adobe Access permite selecionar quais partes do arquivo serão criptografadas. Como o Adobe® Access™ pode analisar o formato de arquivo do conteúdo FLV e F4V, ele pode criptografar de forma inteligente partes seletivas do arquivo em vez do arquivo inteiro. Dados como metadados e pontos de sinalização podem permanecer não criptografados para que os mecanismos de pesquisa ainda possam pesquisar o arquivo.

É possível que um determinado conteúdo tenha várias políticas. Isso pode ser útil, por exemplo, se você quiser licenciar conteúdo em diferentes modelos de negócios sem ter que compactar o conteúdo várias vezes. Por exemplo, você pode permitir acesso anônimo por um curto período de tempo e, depois disso, permitir que o cliente compre o conteúdo e tenha acesso ilimitado. Se o conteúdo for empacotado usando várias políticas, o License Server deverá implementar lógica para selecionar qual política usar para emitir uma licença.

>[!NOTE]
>
>A arquitetura permite que as políticas de uso sejam especificadas e vinculadas ao conteúdo quando o conteúdo for empacotado. Antes que um cliente possa reproduzir o conteúdo, ele deve adquirir uma licença para esse computador. A licença especifica as regras de uso que são aplicadas e fornece a chave usada para descriptografar o conteúdo. A política é um template para geração da licença, mas o servidor de licenças pode optar por substituir as regras de uso ao emitir a licença. Observe que a licença pode ser renderizada por restrições como tempos de expiração ou janelas de reprodução.

Há várias opções disponíveis ao empacotar conteúdo. Eles são especificados na interface `DRMParameters` e nas classes que implementam essa interface, que são `F4VDRMParameters` e `FLVDRMParameters`. Com essas classes, você pode definir parâmetros de assinatura e chave, bem como indicar se deseja criptografar conteúdo de áudio, conteúdo de vídeo ou dados de script. Para ver como eles são implementados na implementação de referência, consulte as descrições das opções de linha de comando do Media Packager discutidas em *Uso das implementações de referência de acesso ao Adobe*. Essas opções são baseadas na API do Java e, portanto, estão disponíveis para uso programático.

As opções de empacotamento incluem:

* Opções de criptografia (áudio, vídeo, criptografia parcial).
* URL do servidor de licenças (o cliente usa esse URL como base para todas as solicitações enviadas ao servidor de licenças)
* Certificado de transporte do servidor de licenças
* Certificado do servidor de licenças, usado para criptografar o CEK.
* Credencial do pacote para assinar metadados

O Adobe Access fornece uma API para transmitir no CEK. Se nenhum CEK for especificado, o SDK o gerará aleatoriamente. Normalmente, você precisa de um CEK diferente para cada parte do conteúdo. No entanto, no Dynamic Streaming, você provavelmente usaria o mesmo CEK para todos os arquivos desse conteúdo, de modo que o usuário só precisa de uma licença e pode fazer a transição sem interrupções de uma taxa de bits para outra. Para usar a mesma chave e licença para vários conteúdos, passe o mesmo objeto `DRMParameters` para `MediaEncrypter.encryptContent()` ou passe no CEK usando `V2KeyParameters.setContentEncryptionKey()`. Para usar uma chave e uma licença diferentes para cada parte do conteúdo, crie uma nova instância `DRMParameters` para cada arquivo.

Ao empacotar o conteúdo usando a rotação de teclas, é possível controlar as teclas de rotação usadas e a frequência com que elas são alteradas. `F4VDRMParameters` e  `FLVDRMParameters` implementar a  `KeyRotationParameters` interface. Por meio dessa interface, é possível ativar a rotação de chaves. Você também precisa especificar um `RotatingContentEncryptionKeyProvider`. Para cada amostra criptografada, essa classe determina a Chave de rotação a ser usada. Você pode implementar seu próprio provedor ou usar o `TimeBasedKeyProvider` incluído no SDK. Essa implementação gera aleatoriamente uma nova chave após um número especificado de segundos.

Em alguns casos, pode ser necessário armazenar os metadados do conteúdo como um arquivo separado e disponibilizá-los ao cliente separadamente do conteúdo. Para fazer isso, chame `MediaEncrypter.encryptContent()`, que retorna um objeto `MediaEncrypterResult`. Chame `MediaEncrypterResult.getKeyInfo()` e converta o resultado em `V2KeyStatus`. Em seguida, recupere os metadados do conteúdo e armazene-os em um arquivo.

Todas essas tarefas podem ser realizadas usando a API do Java. Para obter detalhes sobre a API do Java discutida neste capítulo, consulte *Referência da API de acesso ao Adobe*.

Para obter informações sobre a implementação de referência do Media Packager, consulte *Usando as Implementações de Referência do Acesso ao Adobe*.
