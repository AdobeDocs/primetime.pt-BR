---
description: A interface do codificador de vídeo do AVE retorna essas notificações de reprodução de vídeo no objeto de metadados NATIVE_ERROR.
title: Valores de reprodução de vídeo NATIVE_ERROR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 6%

---


# NATIVE_ERROR: Valores da reprodução de vídeo{#native-error-video-playback-values}

A interface do codificador de vídeo do AVE retorna essas notificações de reprodução de vídeo no objeto de metadados NATIVE_ERROR.

<table> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Valor da chave de metadados RUNTIME_CODE </th> 
   <th colname="col2" class="entry"> Valor da chave de metadados RUNTIME_CODE_MESSAGE </th> 
   <th colname="col3" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> -1 </td> 
   <td colname="col2"><span class="codeph"> END_OF_PERIOD</span> </td> 
   <td colname="col3"> Fim do período. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> SUCESSO</span> </td> 
   <td colname="col3"> Operação bem-sucedida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> Operação assíncrona. A solicitação de operação foi feita. As informações de sucesso/falha estarão disponíveis mais tarde. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> A operação não é possível devido à condição de fim de arquivo (EOF). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> DECODER_FAILED</span> </td> 
   <td colname="col3"> O decodificador falhou no tempo de execução. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> DEVICE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Falha ao abrir o decodificador de hardware. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> FILE_NOT_FOUND  </span> </td> 
   <td colname="col3"> Não é possível localizar o recurso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> GENERIC_ERROR  </span> </td> 
   <td colname="col3"> Erro genérico. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> IRRECOVERABLE_ERROR  </span> </td> 
   <td colname="col3"> Uma condição de erro da qual o Mecanismo de vídeo não pode se recuperar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERABLE  </span> </td> 
   <td colname="col3"> Erro de rede, tentando recuperar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> NO_FIXED_SIZE  </span> </td> 
   <td colname="col3"> O tamanho do recurso não pode ser determinado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10º </td> 
   <td colname="col2"><span class="codeph"> NOT_IMPLEMENTED  </span> </td> 
   <td colname="col3"> Recurso não implementado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11º </td> 
   <td colname="col2"><span class="codeph"> OUT_OF_MEMORY  </span> </td> 
   <td colname="col3"> Memória insuficiente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12º </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR  </span> </td> 
   <td colname="col3"> Erro ao analisar o arquivo de mídia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13º </td> 
   <td colname="col2"><span class="codeph"> SIZE_UNKNOWN  </span> </td> 
   <td colname="col3"> O recurso tem um tamanho, mas é desconhecido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14. </td> 
   <td colname="col2"><span class="codeph"> SOB_FLUXO  </span> </td> 
   <td colname="col3"> Condição de subfluxo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15. </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_CONFIG  </span> </td> 
   <td colname="col3"> A configuração não é suportada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16º </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_OPERATION  </span> </td> 
   <td colname="col3"> Operação não suportada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17º </td> 
   <td colname="col2"><span class="codeph"> WAITING_FOR_INIT  </span> </td> 
   <td colname="col3"> Ainda não inicializado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18º </td> 
   <td colname="col2"><span class="codeph"> INVALID_PARAMETER  </span> </td> 
   <td colname="col3"> Parâmetro inválido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 19º </td> 
   <td colname="col2"><span class="codeph"> INVALID_OPERATION</span> </td> 
   <td colname="col3"> Operação não permitida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 20º </td> 
   <td colname="col2"><span class="codeph"> OP_ONLY_ALLOWED_IN_PAUSED_STATE</span> </td> 
   <td colname="col3"> A operação só é permitida durante uma pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21º </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> A operação não pode ser usada somente em arquivos de áudio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22º </td> 
   <td colname="col2"><span class="codeph"> PREVIOUS_STEP_SEEK_IN_PROGRESS</span> </td> 
   <td colname="col3"> A operação de busca anterior ainda está em andamento. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23º </td> 
   <td colname="col2"><span class="codeph"> SOURCE_NOT_SPECIFIED  </span> </td> 
   <td colname="col3"> Recurso não especificado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24º </td> 
   <td colname="col2"><span class="codeph"> RANGE_ERROR</span> </td> 
   <td colname="col3"> O valor especificado está fora do intervalo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25. </td> 
   <td colname="col2"><span class="codeph"> INVALID_SEEK_TIME</span> </td> 
   <td colname="col3"> Tempo de busca inválido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26º </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> O arquivo especificado não está em conformidade com a sintaxe esperada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27º </td> 
   <td colname="col2"><span class="codeph"> COMPONENT_CREATION_FAILURE</span> </td> 
   <td colname="col3"> Não foi possível criar um componente essencial. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28º </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> Falha ao criar contexto DRM. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29º </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORTED  </span> </td> 
   <td colname="col3"> Não há suporte para o tipo de contêiner. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30º </td> 
   <td colname="col2"><span class="codeph"> SEEK_FAILED</span> </td> 
   <td colname="col3"> Falha na busca. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31º </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Codec não suportado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32º </td> 
   <td colname="col2"><span class="codeph"> NETWORK_UNAVAILABLE</span> </td> 
   <td colname="col3"> A rede não está disponível. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33º </td> 
   <td colname="col2"><span class="codeph"> NETWORK_ERROR</span> </td> 
   <td colname="col3"> Erro ao obter dados da Rede. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34º </td> 
   <td colname="col2"><span class="codeph"> SOBREFLUXO</span> </td> 
   <td colname="col3"> Estouro. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35º </td> 
   <td colname="col2"><span class="codeph"> VIDEO_PROFILE_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Perfil de vídeo não suportado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36º </td> 
   <td colname="col2"><span class="codeph"> PERIOD_NOT_LOADED</span> </td> 
   <td colname="col3"> Tentou-se uma operação em um período de espera ou em um período que ainda não foi carregado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37º </td> 
   <td colname="col2"><span class="codeph"> INVALID_REPLACE_DURATION</span> </td> 
   <td colname="col3"> A duração de substituição especificada é inválida ou ultrapassa o fim do fluxo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38º </td> 
   <td colname="col2"><span class="codeph"> CALLED_FROM_WRONG_THREAD</span> </td> 
   <td colname="col3"> A API não pode ser chamada do thread errado. Principalmente para elementos de API que devem ser chamados somente do thread principal. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39º </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> Erro de leitura do fragmento. Não há failover presente. O mecanismo tentará ler o próximo fragmento. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40º </td> 
   <td colname="col2"><span class="codeph"> ABORTADO</span> </td> 
   <td colname="col3"> A operação foi abortada por uma chamada Cancelar ou Destruir explícita. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41º </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_HLS_VERSION</span> </td> 
   <td colname="col3"> Não é possível reproduzir esta versão da mídia HLS. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42º </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> Não é possível fazer failover. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43º </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> O download HTTP atingiu o tempo limite. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44º </td> 
   <td colname="col2"><span class="codeph"> NETWORK_DOWN  </span> </td> 
   <td colname="col3"> A conexão de rede do usuário está inativa. A reprodução pode parar a qualquer momento e será retomada quando a conexão estiver disponível. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45º </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> Nenhum perfil de taxa de bits utilizável encontrado no fluxo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46º </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> O manifesto tem uma assinatura incorreta. Falha no teste de assinatura do manifesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47º </td> 
   <td colname="col2"><span class="codeph"> CANNOT_LOAD_PLAYLIST</span> </td> 
   <td colname="col3"> Não é possível carregar uma lista de reprodução. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48º </td> 
   <td colname="col2"><span class="codeph"> REPLACEMENT_FAILED</span> </td> 
   <td colname="col3"> A substituição especificada em uma API de inserção não pôde ser bem-sucedida. Isso significa que a inserção foi bem-sucedida, mas a substituição não foi bem-sucedida. A substituição pode falhar se o manifesto a ser substituído tiver sido removido da linha do tempo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49º </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_ASYMMETRIC_PROFILE</span> </td> 
   <td colname="col3"> O DRM está alternando para um perfil assimétrico. Espera-se que todos os perfis estejam alinhados na duração. Caso contrário, esse aviso será lançado e poderá haver saltos na reprodução. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50º </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_BACKWARD</span> </td> 
   <td colname="col3"> Espera-se que a janela ativa avance apenas. Caso contrário, esse aviso será lançado e a janela não será lida. Por causa disso, pode haver saltos (ou parada/pausa longa) na reprodução. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51º </td> 
   <td colname="col2"><span class="codeph"> CURRENT_PERIOD_EXPIRED</span> </td> 
   <td colname="col3"> Janela ativa movida para além do período atual. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52º </td> 
   <td colname="col2"><span class="codeph"> CONTENT_LENGTH_MISMATCH</span> </td> 
   <td colname="col3"> O comprimento do conteúdo relatado pelo servidor HTTP não correspondia ao tamanho real da mídia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53º </td> 
   <td colname="col2"><span class="codeph"> PERIOD_HOLD</span> </td> 
   <td colname="col3"> O leitor de mídia não pode ler mais porque atingiu o tempo definido pela API <span class="codeph"> setholdAt</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> LIVE_HOLD  </span> </td> 
   <td colname="col3"> O leitor de mídia não pode carregar segmentos porque atingiu o fim da janela ativa. O carregamento do segmento será retomado quando o servidor adicionar nova mídia à janela ativa. Esse estado geralmente é alcançado se: 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48">O <span class="codeph"> bufferTime</span> é muito alto (igual ou superior à duração da janela ativa). </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">Uma combinação de uma ou mais API de inserção/exclusão substituiu mais mídia do que adicionou. </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">O próximo período é um período em tempo real com uma substituição de mídia pendente (devido à chamada à API <span class="codeph"> InsertBy</span>) </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEAVING  </span> </td> 
   <td colname="col3"> A intercalação de áudio e vídeo na mídia não é feita corretamente. Este é um erro de empacotamento. O aviso é despachado quando a diferença excede dois segundos. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56º </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57º </td> 
   <td colname="col2"><span class="codeph"> PLAYBACK_NOT_AUTHORIZED</span> </td> 
   <td colname="col3"> A reprodução de HLS não foi ativada no Flash Player. Consulte <span class="codeph"> AuthorizedFeatures.enableHLSPlayback</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58º </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> O decodificador recebeu uma amostra inválida que não pode ser decodificada. Geralmente, esse não é um erro fatal, mas indica que pode haver falhas no áudio/vídeo. Muitas instâncias desse erro indicam uma codificação incorreta ou um arquivo inválido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> Após o início da reprodução, o intervalo Inserir/Substituir não deve conter o cabeçalho de leitura. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60º </td> 
   <td colname="col2"><span class="codeph"> POSTROLL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> As inserções posteriores não são permitidas em uma mídia ao vivo. No entanto, eles são permitidos depois que o servidor marcar a mídia como concluída. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81º </td> 
   <td colname="col2"><span class="codeph"> INTERNAL_ERROR</span> </td> 
   <td colname="col3"> Um assunto muito raro que nunca deveria acontecer. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62º </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> O fluxo não segue a recomendação de embalagem de sempre colocar H264 SPS/PPS em um AVCC. Problemas de busca/reprodução podem ser vistos. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63º </td> 
   <td colname="col2"><span class="codeph"> PARAL_REPLACEMENT</span> </td> 
   <td colname="col3"> A substituição especificada em uma API de inserção foi feita apenas parcialmente. Isso acontece quando replaceDuration passa pela duração da linha do tempo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64º </td> 
   <td colname="col2"><span class="codeph"> RENDITION_M3U8_ERROR</span> </td> 
   <td colname="col3"> Erro ao carregar a lista de reprodução de representação. Isso é somente para AVE, não para FlashPlayer. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65º </td> 
   <td colname="col2"><span class="codeph"> NULL_OPERATION</span> </td> 
   <td colname="col3"> A operação não faz nada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66º </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SKIPPED_ON_FAILURE</span> </td> 
   <td colname="col3"> O segmento não pode ser reproduzido e é ignorado na falha. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67º </td> 
   <td colname="col2"><span class="codeph"> INCOMPATIBLE_RENDER_MODE</span> </td> 
   <td colname="col3"> Modo de renderização incompatível. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68º </td> 
   <td colname="col2"><span class="codeph"> PROTOCOL_NOT_SUPPORTED  </span> </td> 
   <td colname="col3"> Não há suporte para o protocolo Web usado no URL. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69º </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPATIBLE_VERSION</span> </td> 
   <td colname="col3"> Erro ao analisar o arquivo de mídia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70º </td> 
   <td colname="col2"><span class="codeph"> MANIFEST_FILE_UNEXPECTEDLY_CHANGED</span> </td> 
   <td colname="col3"> O arquivo de manifesto foi alterado de maneira inesperada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71º </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> Não é possível executar uma operação de divisão em uma linha do tempo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72º </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> Não é possível executar uma operação de apagamento em uma linha do tempo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73º </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_GET_NEXT_FRAGMENT</span> </td> 
   <td colname="col3"> Não recebeu o próximo fragmento. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74º </td> 
   <td colname="col2"><span class="codeph"> NO_TIMELINE</span> </td> 
   <td colname="col3"> Nenhuma linha do tempo presente em uma estrutura de dados interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> LISTENER_NOT_FOUND</span> </td> 
   <td colname="col3"> Nenhum ouvinte encontrado em uma estrutura de dados interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76º </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> Não é possível iniciar o áudio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77º </td> 
   <td colname="col2"><span class="codeph"> NO_AUDIO_SINK</span> </td> 
   <td colname="col3"> Nenhum dissipador de áudio presente em uma estrutura de dados interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78º </td> 
   <td colname="col2"><span class="codeph"> FILE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Não é possível abrir o arquivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79º </td> 
   <td colname="col2"><span class="codeph"> FILE_WRITE_ERROR</span> </td> 
   <td colname="col3"> Não é possível gravar em um arquivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80º </td> 
   <td colname="col2"><span class="codeph"> FILE_READ_ERROR</span> </td> 
   <td colname="col3"> Não é possível ler a partir de um ficheiro. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81º </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> Erro ao analisar os dados do ID3. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> SECURITY_ERROR  </span> </td> 
   <td colname="col3"> Falha ao carregar o conteúdo devido a restrições de segurança. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> TIMELINE_TOO_SHORT</span> </td> 
   <td colname="col3"> A duração da linha do tempo é muito curta. Se esse for um stream ao vivo, pode haver buffering frequente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> O fluxo foi alternado para um fluxo somente de áudio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> O fluxo foi alternado de somente áudio para um fluxo com vídeo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> KEY_NOT_FOUND  </span> </td> 
   <td colname="col3"> Não é possível localizar a chave. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> INVALID_KEY</span> </td> 
   <td colname="col3"> A chave é inválida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 89 </td> 
   <td colname="col2"> <span class="codeph"> KEY_SERVER_NOT_FOUND</span> </td> 
   <td colname="col3"> O servidor de chaves não retorna uma chave. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 90º </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> Não é possível processar a atualização do manifesto principal. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91º </td> 
   <td colname="col2"> <span class="codeph"> UNREPORTED_TIME_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> Descontinuidade de tempo não relatado (PTS) encontrada. </td> 
  </tr> 
 </tbody> 
</table>

