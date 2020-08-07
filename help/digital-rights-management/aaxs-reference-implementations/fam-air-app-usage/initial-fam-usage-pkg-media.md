---
seo-title: Mídia do pacote
title: Mídia do pacote
uuid: f6e877be-d916-4766-bc44-99891a3df3a8
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Mídia do pacote {#package-media}

Use a guia Package Media (Mídia do pacote) para empacotar o conteúdo. A seção Propriedades do Packager exibe as configurações do Packager que foram inseridas na guia Preferências. Para modificar essas configurações, vá para a guia Preferências, altere as configurações e Salve.

Se desejar disponibilizar um único arquivo FLV ou F4V, escolha a **[!UICONTROL Select Single File]** opção e insira o caminho completo para o arquivo de origem e o caminho completo onde o arquivo criptografado deve ser salvo.

Se desejar disponibilizar todos os arquivos em uma pasta, escolha a **[!UICONTROL Select Single Folder]** opção. Especifique a pasta que contém os arquivos de origem. Somente os arquivos na Pasta de entrada que correspondem aos **[!UICONTROL Input Media File Selection]** critérios serão empacotados (os arquivos nas subpastas não são empacotados). Opte por criptografar [!DNL .flv] arquivos, [!DNL .f4v] arquivos ou inserir uma expressão regular personalizada (por exemplo &quot;.*&quot; criptografa todos os arquivos na pasta). Os arquivos criptografados serão salvos na pasta de saída especificada, usando o mesmo nome de arquivo que o arquivo original.

>[!NOTE]
>
>Os caminhos de arquivo devem se referir aos arquivos disponíveis para o servidor de empacotamento. Se você estiver executando o Gerenciador de Flashes Access em uma máquina diferente do servidor de empacotamento, deverá especificar um caminho que seja acessível ao servidor (localizado em uma unidade de rede ou no próprio servidor).

A tabela a seguir descreve as preferências do Package Media:

| Preferência | Descrição |
|---|---|
| Nome(s) do arquivo de política | Selecione uma ou mais políticas na lista suspensa a serem aplicadas ao conteúdo. Para selecionar várias políticas, mantenha pressionada a tecla CTRL ao selecionar as políticas. |
| Segundos Não criptografados | Especifica o número de segundos de conteúdo a deixar não criptografado no início do arquivo. Para criptografar começando pelo início, digite &quot;0&quot;. |
| Criptografar vídeo | Marque essa caixa de seleção para criptografar dados de vídeo |
| Nível de criptografia | Se a criptografia de vídeo estiver ativada, selecione o nível de criptografia para os dados de vídeo. Alta criptografa todos os dados de vídeo. As partes média e baixa criptografam seletivamente o vídeo. (Somente para F4V com vídeo H.264) |
| Criptografar áudio | Marque essa caixa de seleção para criptografar dados de áudio |
| Criptografar script | Marque essa caixa de seleção para criptografar dados de script (somente FLV) |
| Propriedades personalizadas | Especifique as propriedades personalizadas a serem incluídas no conteúdo empacotado. Essas propriedades estarão disponíveis para o servidor de licenças ao emitir uma licença. (Opcional) |

Depois que as opções de empacotamento forem selecionadas, clique no **[!UICONTROL Package Media]** botão para começar a empacotar os arquivos.
