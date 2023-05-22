---
title: Compactar mídia
description: Compactar mídia
copied-description: true
exl-id: fc2d1f12-8fab-4e62-8d4c-527911be347f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Compactar mídia {#package-media}

Use a guia Empacotar mídia para empacotar conteúdo. A seção Propriedades do empacotador exibe as configurações do empacotador inseridas na guia Preferências. Para modificar essas configurações, vá para a guia Preferências, altere as configurações e Salve.

Se quiser criar um pacote com um único arquivo FLV ou F4V, escolha o **[!UICONTROL Select Single File]** e insira o caminho completo para o arquivo de origem e o caminho completo onde o arquivo criptografado deve ser salvo.

Se quiser criar um pacote de todos os arquivos em uma pasta, escolha o **[!UICONTROL Select Single Folder]** opção. Especifique a pasta que contém os arquivos de origem. Somente os arquivos na Pasta de entrada que correspondam a **[!UICONTROL Input Media File Selection]** os critérios serão empacotados (os arquivos nas subpastas não são empacotados). Optar por criptografar [!DNL .flv] arquivos, [!DNL .f4v] ou insira uma expressão regular personalizada (por exemplo, &quot;.&#42;&quot; criptografa todos os arquivos na pasta). Os arquivos criptografados serão salvos na pasta de saída especificada, usando o mesmo nome do arquivo original.

>[!NOTE]
>
>Os caminhos de arquivo devem se referir aos arquivos disponíveis para o servidor de empacotamento. Se você estiver executando o Gerenciador de Flashes Access em uma máquina diferente do servidor de empacotamento, deverá especificar um caminho que seja acessível pelo servidor (localizado em uma unidade de rede ou no próprio servidor).

A tabela a seguir descreve as preferências do pacote de mídia:

| Preferência | Descrição |
|---|---|
| Nome(s) de Arquivo de Diretiva | Selecione uma ou mais políticas na lista suspensa para aplicar ao conteúdo. Para selecionar várias políticas, mantenha pressionada a tecla CTRL enquanto seleciona as políticas. |
| Segundos sem criptografia | Especifica o número de segundos de conteúdo que devem permanecer não criptografados no início do arquivo. Para criptografar desde o início, digite &quot;0&quot;. |
| Criptografar vídeo | Marque essa caixa de seleção para criptografar dados de vídeo |
| Nível de criptografia | Se a criptografia de vídeo estiver ativada, selecione o nível de criptografia para os dados de vídeo. Alta criptografia de todos os dados de vídeo. As funções Média e Baixa criptografam seletivamente partes do vídeo. (Somente para F4V com vídeo H.264) |
| Criptografar áudio | Marque esta caixa de seleção para criptografar dados de áudio |
| Criptografar Script | Marque essa caixa de seleção para criptografar dados de script (apenas FLV) |
| Propriedades Personalizadas | Especifique as propriedades personalizadas a serem incluídas no conteúdo do pacote. Essas propriedades estarão disponíveis para o servidor de licenças ao emitir uma licença. (Opcional) |

Após selecionar as opções de empacotamento, clique no link **[!UICONTROL Package Media]** botão para começar a empacotar os arquivos.
