---
title: Mídia do pacote
description: Mídia do pacote
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Mídia de pacote {#package-media}

Use a guia Package Media para empacotar o conteúdo. A seção Propriedades do Empacotador exibe as configurações do Empacotador que foram inseridas na guia Preferências. Para modificar essas configurações, vá para a guia Preferências , altere as configurações e Salve.

Se quiser empacotar um único arquivo FLV ou F4V, escolha a opção **[!UICONTROL Select Single File]** e insira o caminho completo para o arquivo de origem e o caminho completo onde o arquivo criptografado deve ser salvo.

Se quiser empacotar todos os arquivos em uma pasta, escolha a opção **[!UICONTROL Select Single Folder]**. Especifique a pasta que contém os arquivos de origem. Somente os arquivos na Pasta de entrada que correspondem aos critérios **[!UICONTROL Input Media File Selection]** serão empacotados (os arquivos em subpastas não são empacotados). Opte por criptografar arquivos [!DNL .flv], arquivos [!DNL .f4v] ou inserir uma expressão regular personalizada (por exemplo, &quot;.*&quot; criptografa todos os arquivos na pasta). Os arquivos criptografados serão salvos na pasta de saída especificada, usando o mesmo nome de arquivo que o arquivo original.

>[!NOTE]
>
>Os caminhos de arquivo devem se referir aos arquivos disponíveis para o servidor de empacotamento. Se você estiver executando o Gerenciador de Flashes Access em uma máquina diferente do servidor de empacotamento, deverá especificar um caminho acessível pelo servidor (localizado em uma unidade de rede ou no próprio servidor).

A tabela a seguir descreve as preferências de Mídia do pacote:

| Preferência | Descrição |
|---|---|
| Nome(s) do arquivo de política | Selecione uma ou mais políticas na lista suspensa para aplicar ao conteúdo. Para selecionar várias políticas, mantenha a tecla CTRL pressionada ao selecionar as políticas. |
| Segundos não criptografados | Especifica o número de segundos do conteúdo a ser mantido não criptografado no início do arquivo. Para criptografar começando pelo início, digite &quot;0&quot;. |
| Criptografar vídeo | Marque essa caixa de seleção para criptografar dados de vídeo |
| Nível de criptografia | Se a criptografia de vídeo estiver ativada, selecione o nível de criptografia para os dados de vídeo. O modo Alto criptografa todos os dados de vídeo. As partes do vídeo são criptografadas seletivamente de médio e baixo. (Somente para F4V com vídeo H.264) |
| Criptografar áudio | Marque essa caixa de seleção para criptografar dados de áudio |
| Script de criptografia | Marque essa caixa de seleção para criptografar dados de script (somente FLV) |
| Propriedades personalizadas | Especifique as propriedades personalizadas para incluir no conteúdo empacotado. Essas propriedades estarão disponíveis para o servidor de licenças ao emitir uma licença. (Opcional) |

Depois que as opções de empacotamento forem selecionadas, clique no botão **[!UICONTROL Package Media]** para começar a empacotar os arquivos.
