---
seo-title: Visão geral
title: Visão geral
uuid: 11cf1f1f-a4b2-4ac2-aae7-e925d96729d2
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Visão geral {#overview}

*O empacotamento* se refere ao processo de criptografia e aplicação de uma política para arquivos FLV ou F4V. Use as APIs de empacotamento de mídia para disponibilizar arquivos. O Adobe Access Java SDK só pode disponibilizar conteúdo Flash e AIR de download progressivo, como FLV, F4V e MP4. Para disponibilizar o conteúdo usando o Adobe Access DRM para outros formatos de conteúdo, como o Adobe HTTP Dynamic Streaming (HDS) ou o Apple HTTP Live Streaming (HLS), é necessário usar outras ferramentas, como o Adobe Media Server ( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html)) ou um codificador que implementa o Adobe Broadcast SDK ( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf)). Como alternativa, os clientes têm a opção de usar o conjunto de ferramentas Java Primetime Packager da Adobe, que pode disponibilizar conteúdo para diversos formatos de destino, como HDS, HLS e DASH.

O empacotamento é desconectado do servidor de licenças. Não há necessidade de o empacotador se conectar ao servidor de licenças para trocar informações sobre o conteúdo. Tudo o que o servidor de licenças precisa saber para emitir a licença está incluído nos metadados do conteúdo.

Quando um arquivo é criptografado, seu conteúdo não pode ser analisado sem a licença apropriada. O Adobe Access permite selecionar quais partes do arquivo serão criptografadas. Como o Adobe® Access™ pode analisar o formato de arquivo do conteúdo FLV e F4V, ele pode criptografar partes seletivas do arquivo de forma inteligente, em vez do arquivo inteiro. Dados como metadados e pontos de sinalização podem permanecer não criptografados para que os mecanismos de pesquisa ainda possam pesquisar o arquivo.

É possível que um determinado conteúdo tenha várias políticas. Isso pode ser útil, por exemplo, se você deseja licenciar o conteúdo em diferentes modelos de negócios sem precisar disponibilizar o conteúdo várias vezes. Por exemplo, você pode permitir acesso anônimo por um curto período de tempo e, depois disso, permitir que o cliente compre o conteúdo e tenha acesso ilimitado. Se o conteúdo for empacotado usando várias políticas, o License Server deverá implementar a lógica para selecionar qual política usar para emitir uma licença.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>A arquitetura permite que as políticas de uso sejam especificadas e vinculadas ao conteúdo quando o conteúdo for empacotado. Antes que um cliente possa reproduzir o conteúdo, ele deve adquirir uma licença para o computador. A licença especifica as regras de uso que são aplicadas e fornece a chave usada para descriptografar o conteúdo. A política é um modelo para gerar a licença, mas o servidor de licenças pode optar por substituir as regras de uso ao emitir a licença. Observe que a licença pode ser renderizada inválida por restrições como tempos de expiração ou janelas de reprodução.

Há várias opções disponíveis ao empacotar conteúdo. Elas são especificadas na `DRMParameters` interface e as classes que implementam essa interface, que são as `F4VDRMParameters` e `FLVDRMParameters`. Com essas classes, você pode definir parâmetros de assinatura e chave, bem como indicar se deseja criptografar conteúdo de áudio, conteúdo de vídeo ou dados de script. Para ver como eles são implementados na implementação de referência, consulte as descrições das opções de linha de comando do Media Packager discutidas em *Uso das Implementações* de referência do Adobe Access. Essas opções são baseadas na API Java e, portanto, estão disponíveis para uso programático.

As opções de empacotamento incluem:

* Opções de criptografia (áudio, vídeo, criptografia parcial).
* URL do servidor de licenças (o cliente usa esse URL como URL base para todas as solicitações enviadas ao servidor de licenças)
* Certificado de transporte do servidor de licenças
* Certificado do servidor de licença, usado para criptografar o CEK.
* Credencial do Packager para assinar metadados

O Adobe Access fornece uma API para envio no CEK. Se nenhum CEK for especificado, o SDK o gera aleatoriamente. Normalmente, você precisa de um CEK diferente para cada parte do conteúdo. Entretanto, no Dynamic Streaming, você provavelmente usaria o mesmo CEK para todos os arquivos desse conteúdo, de modo que o usuário só precisa de uma licença e pode fazer a transição sem problemas de uma taxa de bits para outra. Para usar a mesma chave e licença para vários conteúdos, passe o mesmo `DRMParameters` objeto para `MediaEncrypter.encryptContent()`ou passe no CEK usando `V2KeyParameters.setContentEncryptionKey()`. Para usar uma chave e uma licença diferentes para cada parte do conteúdo, crie uma nova `DRMParameters` instância para cada arquivo.

Ao empacotar o conteúdo usando a rotação de teclas, você pode controlar as Teclas de rotação usadas e a frequência com que elas são alteradas. `F4VDRMParameters` e `FLVDRMParameters` implemente a `KeyRotationParameters` interface. Por meio dessa interface, é possível ativar a rotação de chaves. Você também precisa especificar um `RotatingContentEncryptionKeyProvider`. Para cada amostra criptografada, essa classe determina a Chave de rotação a ser usada. Você pode implementar seu próprio provedor ou usar o `TimeBasedKeyProvider` incluído no SDK. Essa implementação gera aleatoriamente uma nova chave após um número especificado de segundos.

Em alguns casos, talvez seja necessário armazenar os metadados do conteúdo como um arquivo separado e disponibilizá-los ao cliente separadamente do conteúdo. Para fazer isso, chame `MediaEncrypter.encryptContent()`, que retorna um `MediaEncrypterResult` objeto. Chame `MediaEncrypterResult.getKeyInfo()` e converta o resultado para `V2KeyStatus`. Em seguida, recupere os metadados do conteúdo e armazene-os em um arquivo.

Todas essas tarefas podem ser realizadas usando a API Java. Para obter detalhes sobre a API Java discutida neste capítulo, consulte Referência *da API do* Adobe Access.

Para obter informações sobre a implementação de referência do Media Packager, consulte *Uso das implementações* de referência do Adobe Access.
