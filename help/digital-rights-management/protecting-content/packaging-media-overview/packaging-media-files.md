---
seo-title: Visão geral dos arquivos de mídia de empacotamento
title: Visão geral dos arquivos de mídia de empacotamento
uuid: 9509bcdc-ee4d-4025-9bb6-9b8ac439b926
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Visão geral {#packaging-media-files-overview}

O empacotamento se refere ao processo de criptografia e aplicação de uma política de DRM ao conteúdo de vídeo. Você pode usar as APIs de empacotamento de mídia para empacotar arquivos. O Primetime DRM Java SDK só pode disponibilizar conteúdo de download progressivo, como MP4.

>[!NOTE]
>
>Entre em contato com seu representante DRM Primetime sobre como selecionar a opção de empacotamento mais apropriada para o formato de mídia e casos de uso.

O empacotamento é desconectado do servidor de licenças. Não há necessidade de o empacotador se conectar ao servidor de licenças para trocar informações sobre o conteúdo. Tudo o que o servidor de licenças precisa saber para emitir uma licença está incluído nos metadados do conteúdo.

Quando um arquivo é criptografado, seu conteúdo não pode ser analisado sem a licença apropriada. Você pode usar o Primetime DRM para selecionar as partes do arquivo que deseja criptografar. Como o Primetime DRM pode analisar o formato de arquivo do conteúdo de vídeo, ele pode criptografar partes seletivas de um arquivo de forma inteligente em vez de um arquivo inteiro. Os dados, como metadados e pontos de sinalização, podem permanecer não criptografados para que os mecanismos de pesquisa ainda possam pesquisar o arquivo.

Um conteúdo especificado pode ter várias políticas de DRM. Por exemplo, você pode licenciar o conteúdo em diferentes modelos de negócios sem precisar disponibilizar o conteúdo várias vezes. Além disso, você pode permitir o acesso anônimo por um curto período de tempo e permitir que o cliente compre o conteúdo para ter acesso ilimitado. Se o conteúdo for empacotado usando várias políticas de DRM, o License Server deverá implementar a lógica para selecionar qual política de DRM deve ser usada para emitir uma licença.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>A arquitetura permite que as políticas de DRM de uso sejam especificadas e vinculadas ao conteúdo quando o conteúdo for empacotado. Antes que um cliente possa reproduzir o conteúdo, ele deve adquirir uma licença para um computador especificado. A licença especifica as regras de uso que são aplicadas e fornece a chave que deve ser usada para descriptografar o conteúdo. A política de DRM representa um modelo para gerar uma licença. No entanto, o servidor de licenças pode substituir as regras de uso ao emitir uma licença. A licença pode ser renderizada inválida por tais restrições, como tempos de expiração ou janelas de reprodução.

O Primetime DRM fornece uma API para passar no CEK. Se nenhum CEK for especificado, o SDK o gera aleatoriamente. Normalmente, você precisa de um CEK diferente para cada seção do conteúdo. No entanto, no Dynamic Streaming, é provável que você use o mesmo CEK para todos os arquivos que compõem esse conteúdo. Portanto, um usuário só precisa de uma licença única para fazer a transição perfeitamente de uma taxa de bits para outra. Se você quiser usar a mesma chave e licença para vários conteúdos, é necessário enviar o mesmo `DRMParameters` objeto para `MediaEncrypter.encryptContent()`o CEK usando `V2KeyParameters.setContentEncryptionKey()`. Se quiser usar uma chave e uma licença diferentes para cada seção do conteúdo, é necessário criar uma nova `DRMParameters` instância para cada arquivo.

Ao empacotar o conteúdo usando a rotação de teclas, é possível controlar as Teclas de rotação usadas e a frequência com que as teclas são alteradas. `F4VDRMParameters` e `FLVDRMParameters` implemente a `KeyRotationParameters` interface. Por meio dessa interface, é possível ativar a rotação de chaves. Você também precisa especificar um `RotatingContentEncryptionKeyProvider`. Para cada amostra criptografada, essa classe determina a Chave de rotação a ser usada. Você pode implementar seu próprio provedor ou usar o `TimeBasedKeyProvider` incluído no SDK. Essa implementação gera aleatoriamente uma nova chave após um número especificado de segundos.

Em alguns casos, talvez seja necessário armazenar os metadados do conteúdo como um arquivo separado e disponibilizá-los ao cliente separadamente do conteúdo. Nesse caso, é necessário invocar `MediaEncrypter.encryptContent()`, que retorna um `MediaEncrypterResult` objeto. Chame `MediaEncrypterResult.getKeyInfo()` e converta o resultado para `V2KeyStatus`. Em seguida, recupere os metadados do conteúdo e armazene-os em um arquivo.

Todas essas tarefas podem ser realizadas com a API Java.

Consulte Referência *da API DRM do* Adobe Primetime para obter detalhes sobre a API do Java.

Consulte *Usando as Implementações* de referência do Adobe Primetime DRM para obter informações sobre a implementação de referência do Media Packager.
