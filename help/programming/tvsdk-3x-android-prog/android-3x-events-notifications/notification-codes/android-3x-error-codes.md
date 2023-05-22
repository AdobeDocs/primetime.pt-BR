---
title: Códigos de erro PSDK
description: Informações sobre vários códigos de erro, avisos e códigos de erro nativos.
exl-id: 90d66c13-c40c-4602-83da-186c2b623375
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 6%

---

# Códigos de erro PSDK {#psdk-error-codes}

Leia para saber mais sobre códigos de erro PSDK, avisos e códigos de erro nativos.

## Erros

A tabela a seguir fornece informações detalhadas sobre notificações do tipo ERRO. A maioria dos erros contém metadados relevantes; por exemplo, o URL do recurso que falhou no download. Algumas notificações contêm metadados para especificar se o problema ocorreu no conteúdo de vídeo principal, no conteúdo de áudio alternativo ou em um anúncio.

<table frame="all" colsep="1" rowsep="1">
  <tr> 
   <th><b>Nome de erro PSDK</b></th>
   <th><b>Código de erro PSDK</b></th>
   <th><b>Descrição</b></th>
  </tr>
  <tr>
    <td>SUCESSO</td>
    <td>0</td>
    <td>A operação executada pela API subjacente foi bem-sucedida.</td>
  </tr>
  <tr>
    <td>INVALID_ARGUMENT</td>
    <td>1</td>
    <td>Os dados ou o formato do argumento fornecido para a API subjacente são inválidos.</td>
  </tr>
  <tr>
    <td>PONTEIRO_NULO</td>
    <td>2</td>
    <td>Um dos argumentos transmitidos é NULL ou um dos membros internos não foi inicializado.</td>
  </tr>
  <tr>
    <td>ILLEGAL_STATE</td>
    <td>3</td>
    <td>A operação não tem suporte no estado atual do player.</td>
  </tr>
  <tr>
    <td>INTERFACE_NOT_FOUND</td>
    <td>4</td>
    <td>O método interfaceCast lança esse erro quando a interface solicitada não é implementada/herdada por isso.</td>
  </tr>
  <tr>  
    <td>CREATION_FAILED</td>
    <td>5</td>
    <td>Falha na criação de um dos recursos internos.</td>
  </tr>
  <tr>
    <td>UNSUPPORTED_OPERATION</td>
    <td>6</td>
    <td>A operação solicitada não é suportada no momento.</td>
  </tr>
  <tr>
    <td>DADOS_NÃO_DISPONÍVEIS</td>
    <td>7</td>
    <td>Os dados solicitados não estão disponíveis no momento.</td>
  </tr>
  <tr>
    <td>SEEK_ERROR</td>
    <td>8</td>
    <td>Ocorreu um erro ao executar uma operação de busca.</td>
  </tr>
  <tr>
    <td>UNSUPPORTED_FEATURE</td>
    <td>9</td>
    <td>Este recurso/função não é compatível.</td>
  </tr>
  <tr>
    <td>RANGE_ERROR</td>
    <td>10</td>
    <td>O valor especificado está fora do intervalo.</td>
  </tr>
  <tr>
    <td>CODEC_NOT_SUPPORTED</td>
    <td>11</td>
    <td>O TVSDK ou o dispositivo subjacente não oferece suporte ao Codec de Áudio/Vídeo do fluxo.</td>
  </tr>
  <tr>
    <td>MEDIA_ERROR</td>
    <td>12</td>
    <td>A mídia especificada não foi encontrada.</td>
  </tr>
  <tr>
    <td>NETWORK_ERROR</td>
    <td>13</td>
    <td>Ocorreu um erro ao baixar um fragmento ou segmento (vídeo e áudio).</td>
  </tr>
  <tr>
    <td>GENERIC_ERROR</td>
    <td>14</td>
    <td>Evento de erro genérico. Não emitido pelo TVSDK. Isso é apenas um marcador para o final do intervalo de códigos numéricos correspondente aos eventos de erro do TVSDK.</td>
  </tr>
  <tr>
    <td>INVALID_SEEK_TIME</td>
    <td>15</td>
    <td>O tempo de busca fornecido é inválido.</td>
  </tr>
  <tr>
    <td>AUDIO_TRACK_ERROR</td>
    <td>16</td>
    <td>Ocorreu um erro relacionado a uma faixa de áudio (Áudio alternativo)</td>
  </tr>
  <tr>
    <td>ACCESS_FROM_DIFFERENT_THREAD</td>
    <td>17</td>
    <td>A API PSDK é chamada a partir de um thread diferente daquele no qual o PSDK foi inicializado.</td>
  </tr>
  <tr>
    <td>ELEMENT_NOT_FOUND</td>
    <td>18</td>
    <td>O elemento não foi encontrado.</td>
  </tr>
  <tr>
    <td>NOT_IMPLEMENTED</td>
    <td>19</td>
    <td>Recurso não implementado.</td>
  </tr>
  <tr>
    <td>PRE_ROLL_DISABLED</td>
    <td>20</td>
    <td>A pré-rolagem foi desativada via AdvertisingMetadata.</td>
  </tr>
  <tr>
    <td>PLAYBACK_NOT_AUTHORIZED</td>
    <td>57</td>
    <td>A reprodução HLS não foi habilitada no Flash Player. Consulte AuthorizedFeatures.enableMediaPlayerHLSPlayback().</td>
  </tr>
  <tr>
    <td>NETWORK_TIMEOUT</td>
    <td>58</td>
    <td>Tempo limite de rede atingido ao buscar um recurso/servidor de conexão.</td>
  </tr>
</table>

## Avisos

A tabela a seguir fornece informações detalhadas sobre notificações do tipo WARN.
A maioria dos avisos contém metadados relevantes; por exemplo, o URL do recurso que falhou no download. Algumas notificações contêm metadados para especificar se o problema ocorreu no conteúdo de vídeo principal, no conteúdo de áudio alternativo ou em um anúncio.

<table frame="all" colsep="1" rowsep="1">
  <tr>
    <th><b>Nome do erro</b></th>
    <th><b>Código</b></th>
    <th><b>Descrição</b></th>
  </tr>
  <tr>
    <td>PLAYBACK_OPERATION_FAILED</td>
    <td>200</td>
    <td>Ocorreu um erro durante a operação de reprodução. Falha em uma operação relacionada à reprodução</td>
  </tr>
  <tr>  
    <td>NATIVE_WARNING</td>
    <td>201</td>
    <td>A biblioteca AVE de baixo nível emitiu um erro.</td>
  </tr>
  <tr>
    <td>AD_RESOLVER_FAILED</td>
    <td>202</td>
    <td>O plug-in de publicidade não conseguiu resolver os anúncios.</td>
  </tr>
  <tr>
    <td>AD_MANIFEST_LOAD_FAILED</td>
    <td>203</td>
    <td>Falha ao carregar o manifesto de anúncio.</td>
  </tr>
  <tr>
    <td>AD_RESOLUTION_IN_PROGRESS</td>
    <td>204</td>
    <td>A operação para solucionar anúncios está em andamento.</td>
  </tr>
  </table>

## Informações

<table frame="all" colsep="1" rowsep="1">
  <tr> 
    <th><b>Nome do erro</b></th>
    <th><b>Código</b></th>
    <th><b>Descrição</b></th>
  </tr>
  <tr>
    <td>REVENUE_OTIMIZATION_REPORTING</td>
    <td>300</td>
    <td>Notificações detalhadas do TVSDK para relatórios e análises adicionais.</td>
  </tr>
 </table>

## Códigos de erro nativo

A interface do Codificador de vídeo do AVE retorna essas notificações de reprodução de vídeo no objeto de metadados NATIVE_ERROR.

<table frame="all" colsep="1" rowsep="1">
  <tr>
    <th><b>Nome do erro</b></th>
    <th><b>Código</b></th>
    <th><b>Descrição</b></th>
  </tr>
  <tr>  
    <td>END_OF_PERIOD</td>
    <td>-1</td>
    <td>Fim do período.</td>
  </tr>
  <tr>
    <td>SUCESSO</td>
    <td>0</td>
    <td>Operação bem-sucedida.</td>
  </tr>
  <tr>
    <td>ASYNC_OPERATION_IN_PROGRESS</td>
    <td>1</td>
    <td>Operação assíncrona. A solicitação de operação foi feita. As informações de sucesso/ falha estarão disponíveis posteriormente.</td>
  </tr>
  <tr>
    <td>EOF</td>
    <td>2</td>
    <td>Operação não possível devido à condição de fim de arquivo (EOF).</td>
  </tr>
  <tr>
    <td>DECODIFICADOR_FALHA</td>
    <td>3</td>
    <td>Falha do decodificador no tempo de execução.</td>
  </tr>
  <tr>
    <td>DEVICE_OPEN_ERROR</td>
    <td>4</td>
    <td>Falha ao abrir o decodificador de hardware.</td>
  </tr>
  <tr>
    <td>ARQUIVO_NÃO_ENCONTRADO</td>
    <td>5</td>
    <td>O recurso não pode ser localizado.</td>
  </tr>
  <tr>
    <td>GENERIC_ERROR</td>
    <td>6</td>
    <td>Erro genérico.</td>
  </tr>
  <tr>
    <td>IRRECUPERÁVEL_ERRO</td>
    <td>7</td>
    <td>Uma condição de erro da qual o mecanismo de vídeo não pode se recuperar.</td>
  </tr>
  <tr>
    <td>LOST_CONNECTION_RECOVERABLE</td>
    <td>8</td>
    <td>Erro de rede, tentando recuperar.</td>
  </tr>
  <tr> 
    <td>NO_FIXED_SIZE</td>
    <td>9</td>
    <td>Não é possível determinar o tamanho do recurso.</td>
  </tr>
  <tr>
    <td>NOT_IMPLEMENTED</td>
    <td>10</td>
    <td>Recurso não implementado.</td>
  </tr>
  <tr>
    <td>SEM_MEMÓRIA</td>
    <td>11</td>
    <td>Sem memória.</td>
  </tr>
  <tr>
    <td>PARSE_ERROR</td>
    <td>12</td>
    <td>Erro ao analisar o arquivo de mídia.</td>
  </tr>
  <tr>  
    <td>TAMANHO_DESCONHECIDO</td>
    <td>13</td>
    <td>O recurso tem um tamanho, mas ele é desconhecido.</td>
  </tr>
  <tr>  
    <td>UNDER_FLOW</td>
    <td>14</td>
    <td>Condição de estouro negativo.</td>
  </tr>
  <tr> 
    <td>UNSUPPORTED_CONFIG</td>
    <td>15</td>
    <td>A configuração não é compatível.</td>
  </tr>
  <tr>  
    <td>UNSUPPORTED_OPERATION</td>
    <td>16</td>
    <td>A operação não é aceita.</td>
  </tr>
  <tr>
    <td>WAITING_FOR_INIT</td>
    <td>17</td>
    <td>Ainda não inicializado.</td>
  </tr>
  <tr>  
    <td>INVALID_PARAMETER</td>
    <td>18</td>
    <td>Parâmetro inválido.</td>
  </tr>
  <tr>
    <td>INVALID_OPERATION</td>
    <td>19</td>
    <td>Operação não permitida.</td>
  </tr>
  <tr>
    <td>OP_ONLY_ALLOWED_IN_PAUSED_STATE</td>
    <td>20</td>
    <td>A operação é permitida somente enquanto está pausada.</td>
  </tr>
  <tr> 
    <td>OP_INVALID_WITH_AUDIO_ONLY_FILE</td>
    <td>21</td>
    <td>A operação não pode ser usada em arquivos somente de áudio.</td>
  </tr>
  <tr>
    <td>PREVIOUS_STEP_SEEK_IN_PROGRESS</td>
    <td>22</td>
    <td>A operação de busca anterior ainda está em andamento.</td>
  </tr>
  <tr> 
    <td>SOURCE_NOT_SPECIFIED</td>
    <td>23</td>
    <td>Recurso não especificado.</td>
  </tr>
  <tr>
    <td>RANGE_ERROR</td>
    <td>24</td>
    <td>O valor especificado está fora do intervalo.</td>
  </tr>
  <tr>
    <td>INVALID_SEEK_TIME</td>
    <td>25</td>
    <td>Tempo de busca inválido.</td>
  </tr>
  <tr>
    <td>FILE_STRUCTURE_INVALID</td>
    <td>26</td>
    <td>O arquivo especificado não está em conformidade com a sintaxe esperada.</td>
  </tr>
  <tr>
    <td>COMPONENT_CREATION_FAILURE</td>
    <td>27</td>
    <td>Não foi possível criar um componente essencial.</td>
  </tr>
  <tr>
    <td>DRM_INIT_ERROR</td>
    <td>28</td>
    <td>Falha ao criar o contexto de DRM.</td>
  </tr>
  <tr>
    <td>CONTAINER_NOT_SUPPORTED</td>
    <td>29</td>
    <td>O tipo de contêiner não é suportado.</td>
  </tr>
  <tr>
    <td>SEEK_FAILED</td>
    <td>30</td>
    <td>Falha na busca.</td>
  </tr>
  <tr>
    <td>CODEC_NOT_SUPPORTED</td>
    <td>31</td>
    <td>Codec sem suporte.</td>
  </tr>
  <tr>
    <td>REDE_INDISPONÍVEL</td>
    <td>32</td>
    <td>Rede não disponível.</td>
  </tr>
  <tr>  
    <td>NETWORK_ERROR</td>
    <td>33</td>
    <td>Erro ao obter dados da rede.</td>
  </tr>
  <tr>
    <td>ESTOURO</td>
    <td>34</td>
    <td>Estouro.</td>
  </tr>
  <tr>  
    <td>VIDEO_PROFILE_NOT_SUPPORTED</td>
    <td>35</td>
    <td>Perfil de vídeo não suportado.</td>
  </tr>
  <tr>
    <td>PERIOD_NOT_LOADED</td>
    <td>36</td>
    <td>Tentativa de operação em um período SUSPENSO ou em um período que ainda não foi carregado.</td>
  </tr>
  <tr> 
    <td>INVALID_REPLACE_DURATION</td>
    <td>37</td>
    <td>A duração de substituição especificada é inválida ou se estende além do final do fluxo.</td>
  </tr>
  <tr>
    <td>CALLED_FROM_WRONG_THREAD</td>
    <td>38</td>
    <td>A API não pode ser chamada do thread errado. Geralmente, para elementos de API que devem ser chamados somente a partir do thread principal.</td>
  </tr>
  <tr>
    <td>FRAGMENT_READ_ERROR</td>
    <td>39</td>
    <td>Erro de leitura do fragmento. Nenhum failover presente. O mecanismo tentará ler o próximo fragmento.</td>
  </tr>
  <tr>
    <td>ANULADO</td>
    <td>40</td>
    <td>A operação foi anulada por uma chamada explícita de Anular ou Destruir.</td>
  </tr>
  <tr>
    <td>UNSUPPORTED_HLS_VERSION</td>
    <td>41</td>
    <td>Não é possível reproduzir esta versão da mídia HLS.</td>
  </tr>
  <tr>
    <td>CANNOT_FAIL_OVER</td>
    <td>42</td>
    <td>Não é possível fazer failover.</td>
  </tr>
  <tr> 
    <td>HTTP_TIME_OUT</td>
    <td>43</td>
    <td>O download de HTTP atingiu o tempo limite.</td>
  </tr>
  <tr>
    <td>NETWORK_DOWN</td>
    <td>44</td>
    <td>A conexão de rede do usuário está inoperante. A reprodução pode parar a qualquer momento e será retomada quando a conexão estiver disponível.</td>
  </tr>
  <tr>
    <td>NO_USABLE_BITRATE_PROFILE</td>
    <td>45</td>
    <td>Nenhum perfil de taxa de bits utilizável encontrado no fluxo.</td>
  </tr>
  <tr>
    <td>BAD_MANIFEST_SIGNATURE</td>
    <td>46</td>
    <td>O manifesto tem uma assinatura incorreta. Falha no teste de assinatura de manifesto.</td>
  </tr>
  <tr>
    <td>CANNOT_LOAD_PLAYLIST</td>
    <td>47</td>
    <td>Não é possível carregar uma lista de reprodução.</td>
  </tr>
  <tr>
    <td>REPLACEMENT_FAILED</td>
    <td>48</td>
    <td>A substituição especificada em uma API de Inserção não teve êxito. Isso significa que a inserção foi bem-sucedida, mas a substituição não. A substituição poderá falhar se o manifesto que será substituído tiver sido removido da linha do tempo.</td>
  </tr>
  <tr>
    <td>SWITCH_TO_ASYMMETRIC_PROFILE</td>
    <td>49</td>
    <td>O DRM está alternando para um perfil assimétrico. Espera-se que todos os perfis estejam alinhados em duração. Caso contrário, esse aviso será exibido e poderá haver saltos na reprodução.</td>
  </tr>
  <tr>
    <td>LIVE_WINDOW_MOVED_BACKWARD</td>
    <td>50</td>
    <td>Espera-se que a janela ativa avance somente. Caso contrário, esse aviso será exibido e a janela não será lida. Por causa disso, pode haver saltos (ou parada/pausa longa) na reprodução.</td>
  </tr>
  <tr>
    <td>CURRENT_PERIOD_EXPIRED</td>
    <td>51</td>
    <td>A janela em tempo real foi movida para além do período atual.</td>
  </tr>
  <tr>
    <td>CONTENT_LENGTH_MISMATCH</td>
    <td>52</td>
    <td>O comprimento do conteúdo relatado pelo servidor HTTP não correspondia ao tamanho real da mídia.</td>
  </tr>
  <tr>
    <td>PERIOD_HOLD</td>
    <td>53</td>
    <td>O leitor de mídia não pode ler mais porque atingiu o tempo definido pela API setHoldAt.</td>
  </tr>
  <tr>  
    <td>LIVE_HOLD</td>
    <td>54</td>
    <td>O leitor de mídia não pode carregar segmentos porque atingiu o fim da janela ativa. O carregamento do segmento será retomado quando o servidor adicionar nova mídia à janela ativa. Normalmente, esse estado é atingido se:<ul><li>O bufferTime é muito alto (igual ou maior que a duração da janela ativa).</li><li>Uma combinação de uma ou mais API de inserção/ apagamento substituiu mais mídia do que foi adicionada.</li><li>O próximo período é um período em tempo real com uma substituição de mídia pendente (devido à chamada da API InsertBy )</li></ul></td>
  </tr>
  <tr>
    <td>BAD_MEDIA_INTERLEAVING</td>
    <td>55</td>
    <td>O intercalamento de áudio e vídeo na mídia não é feito corretamente. Este é um erro de empacotamento. O aviso é despachado quando a diferença excede dois segundos.</td>
  </tr>
  <tr>
    <td>DRM_NOT_AVAILABLE</td>
    <td>56</td>
    <td></td>
  </tr>
  <tr>  
    <td>PLAYBACK_NOT_AUTHORIZED</td>
    <td>57</td>
    <td>A reprodução HLS não foi habilitada no Flash Player. Consulte AuthorizedFeatures.enableHLSPlayback.</td>
  </tr>
  <tr>
    <td>BAD_MEDIA_SAMPLE_FOUND</td>
    <td>58</td>
    <td>O decodificador recebeu uma amostra inválida que não pode ser decodificada. Geralmente, esse não é um erro fatal, mas indica que pode haver falhas no áudio/vídeo. Muitas instâncias desse erro indicam uma codificação incorreta ou um arquivo inválido.</td>
  </tr>
  <tr>
    <td>RANGE_SPANS_READ_HEAD</td>
    <td>59</td>
    <td>Depois que a reprodução começar, o intervalo Inserir/Substituir não deve conter o indicador de leitura.</td>
  </tr>
  <tr> 
    <td>POSTROLL_WITH_LIVE_NOT_ALLOWED</td>
    <td>60</td>
    <td>Inserções pós-rolagem não são permitidas em uma mídia em tempo real. No entanto, elas são permitidas depois que o servidor marca a mídia como concluída.</td>
  </tr>
  <tr>
    <td>ERRO_INTERNO</td>
    <td>61</td>
    <td>Uma questão muito rara que nunca deve acontecer.</td>
  </tr>
  <tr>  
    <td>SPS_PPS_FOUND_OUTSIDE_AVCC</td>
    <td>62</td>
    <td>O fluxo não segue a recomendação de empacotamento de sempre colocar H264 SPS/PPS em um AVCC. Problemas de busca/reprodução podem ser vistos.</td>
  </tr>
  <tr>  
    <td>PARTIAL_REPLACEMENT</td>
    <td>63</td>
    <td>A substituição especificada em uma API de Inserção foi feita apenas parcialmente. Isso acontece quando replaceDuration ultrapassa a duração da linha do tempo.</td>
  </tr>
  <tr>
    <td>REPRESENTAÇÃO_M3U8_ERRO</td>
    <td>64</td>
    <td>Erro ao carregar a lista de reprodução de representação. Isso é apenas para o AVE, não para o FlashPlayer.</td>
  </tr>
  <tr>
    <td>NULL_OPERATION</td>
    <td>65</td>
    <td>A operação não faz nada.</td>
  </tr>
  <tr>
    <td>SEGMENT_SKIPPED_ON_FAILURE</td>
    <td>66</td>
    <td>O segmento não pode ser reproduzido e é ignorado na falha.</td>
  </tr>
  <tr>
    <td>INCOMPATIBLE_RENDER_MODE</td>
    <td>67</td>
    <td>Modo de processamento incompatível.</td>
  </tr>
  <tr>
    <td>PROTOCOLO_NÃO_SUPORTADO</td>
    <td>68</td>
    <td>O protocolo da Web usado no URL não é compatível.</td>
  </tr>
  <tr>
    <td>PARSE_ERROR_INCOMPATIBLE_VERSION</td>
    <td>69</td>
    <td>Erro ao analisar o arquivo de mídia.</td>
  </tr>
  <tr>  
    <td>MANIFEST_FILE_UNEXPECTEDLY_CHANGED</td>
    <td>70</td>
    <td>O arquivo de manifesto foi alterado de uma maneira inesperada.</td>
  </tr>
  <tr>
    <td>CANNOT_SPLIT_TIMELINE</td>
    <td>71</td>
    <td>Não é possível executar uma operação de divisão em uma linha do tempo.</td>
  </tr>
  <tr>
    <td>CANNOT_ERASE_TIMELINE</td>
    <td>72</td>
    <td>Não é possível executar uma operação de apagar em uma linha do tempo.</td>
  </tr>
  <tr>
    <td>DID_NOT_GET_NEXT_FRAGMENT</td>
    <td>73</td>
    <td>Não obteve o próximo fragmento.</td>
  </tr>
  <tr>
    <td>NO_TIMELINE</td>
    <td>74</td>
    <td>Nenhuma linha do tempo presente em uma estrutura de dados interna.</td>
  </tr>
  <tr>
    <td>LISTENER_NOT_FOUND</td>
    <td>75</td>
    <td>Nenhum ouvinte encontrado em uma estrutura de dados interna.</td>
  </tr>
  <tr>
    <td>AUDIO_START_ERROR</td>
    <td>76</td>
    <td>Não é possível iniciar o áudio.</td>
  </tr>
  <tr>
    <td>NO_AUDIO_SINK</td>
    <td>77</td>
    <td>Nenhum coletor de áudio presente em uma estrutura de dados interna.</td>
  </tr>
  <tr>  
    <td>FILE_OPEN_ERROR</td>
    <td>78</td>
    <td>Não é possível abrir o arquivo.</td>
  </tr>
  <tr>
    <td>FILE_WRITE_ERROR</td>
    <td>79</td>
    <td>Não é possível gravar em um arquivo.</td>
  </tr>
  <tr>
    <td>FILE_READ_ERROR</td>
    <td>80</td>
    <td>Não é possível ler de um arquivo.</td>
  </tr>
  <tr>
    <td>ID3PARSE_ERROR</td>
    <td>81</td>
    <td>Ocorreu um erro ao analisar dados de ID3.</td>
  </tr>
  <tr>
    <td>SECURITY_ERROR</td>
    <td>82</td>
    <td>Falha ao carregar o conteúdo devido a restrições de segurança.</td>
  </tr>
  <tr>
    <td>LINHA DO TEMPO_MUITO_CURTA</td>
    <td>83</td>
    <td>A duração da linha do tempo é muito curta. Se for um stream ao vivo, buffering frequente pode ocorrer.</td>
  </tr>
  <tr>
    <td>AUDIO_ONLY_STREAM_START</td>
    <td>84</td>
    <td>O fluxo foi alternado para um fluxo somente de áudio.</td>
  </tr>
  <tr>  
    <td>AUDIO_ONLY_STREAM_END</td>
    <td>85</td>
    <td>O fluxo foi alternado de somente áudio para um fluxo com vídeo.</td>
  </tr>
  <tr>
    <td>CHAVE_NÃO_ENCONTRADA</td>
    <td>87</td>
    <td>A chave não pode ser encontrada.</td>
  </tr>
  <tr>
    <td>INVALID_KEY</td>
    <td>88</td>
    <td>A chave é inválida.</td>
  </tr>
  <tr>
    <td>KEY_SERVER_NOT_FOUND</td>
    <td>89</td>
    <td>O servidor de chaves não retorna uma chave.</td>
  </tr>
  <tr>
    <td>MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</td>
    <td>90</td>
    <td>Não é possível manipular a atualização do manifesto principal.</td>
  </tr>
  <tr>
    <td>UNREPORTED_TIME_DISCONTINUITY_FOUND</td>
    <td>91</td>
    <td>Descontinuidade de tempo não relatado (PTS) encontrada.</td>
  </tr>
  <tr>
    <td>UNMATCHED_AV_DISCONTINUITY_FOUND</td>
    <td>92</td>
    <td>Descontinuidade de Áudio e Vídeo sem Correspondência encontrada.</td>
  </tr>
  <tr>
    <td>TRICKPLAY_ENDED_DUE_TO_ERROR</td>
    <td>93</td>
    <td>Ocorreu um erro ao reproduzir mídia no modo de execução de truque. O modo de reprodução de truques é encerrado e o fluxo é pausado. Chame Play() para reproduzir a mídia no modo normal.</td>
  </tr>
  <tr>
    <td>LIVE_WINDOW_MOVED_AHEAD</td>
    <td>95</td>
    <td>O reprodutor está fora da janela ativa e deve ir em frente para alcançar o nível desejado.</td>
  </tr>
</table>
