---
title: Notas de versão do TVSDK 2.7 para Android
seo-title: Notas de versão do TVSDK 2.7 para Android
description: As Notas de versão do TVSDK 2.7 para Android descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK Android 2.7
seo-description: As Notas de versão do TVSDK 2.7 para Android descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK Android 2.7
uuid: 4013b97d-29f9-435b-8772-b19df7054282
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: bab78e9f-f9ba-4e1c-b778-0936ae704037
translation-type: tm+mt
source-git-commit: 36a1619b43d22ccc7286d4a4b74f2c6297d0fd47

---


# Notas de versão do TVSDK 2.7 para Android {#tvsdk-for-android-release-notes}

As Notas de versão do TVSDK 2.7 para Android descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK Android 2.7

## TVSDK Android 2.7 {#tvsdk-android}

O player de referência do Android está incluído no Android TVSDK no diretório samples/ de sua distribuição. O arquivo README&lt;.md que o acompanha explica como criar o player de referência.

>[!NOTE]
>
>Para criar com êxito o player de referência, conforme descrito em README.md distribuído com a versão, certifique-se de fazer o seguinte:
>
>1. Baixe o VideoHeartbeat.jar de [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) (biblioteca VideoHeartbeat para Android v2.0.0)
>1. Extraia VideoHeartbeat.jar para a pasta libs/.
>



## Novos recursos {#new-features}

O TVSDK 2.7 para Android inclui todos os recursos da versão 1.4, exceto os recursos não suportados listados em Matriz de [recursos](#feature-matrix).

**Android TVSDK 2.7**

* **Suporte para resolução de anúncios paralela**

O TVSDK 2.7 suporta a resolução simultânea de todas as solicitações de anúncio em uma pausa de anúncio, em vez da resolução sequencial.

### Novos recursos das versões anteriores {#new-features-previous-releases}

**Versão 2.5.6**

* **O TVSDK 2.5 é compatível com Android P**
* **Habilitar áudio em segundo plano**

   Para ativar a reprodução de áudio quando o aplicativo se move de primeiro para segundo plano, o aplicativo deve chamar enableAudioPlaybackInBackground API do MediaPlayer como argumento quando o player está em estado PREPARADO.

* **alwaysUseAudioOutputLatency(boolean val) na classe MediaPlayer**

Quando definido, use a latência de saída no cálculo do carimbo de data e hora de áudio.
Parâmetros booleanos val - Verdadeiro usará a latência de saída de áudio no cálculo do carimbo de data e hora de áudio.

* **Otimizado para obter a melhor experiência de reprodução mesmo se a velocidade da largura de banda cair de repente.**
O TVSDK agora cancela o download do segmento em andamento, se necessário, e alterna dinamicamente para a execução apropriada. Isso é feito alternando perfeitamente entre as taxas de bits sem interrupções.

**Versão 2.5.5**

* **Inserção parcial de quebra de anúncio**

   Experiência semelhante à da TV de participar do meio de um anúncio sem acionar o rastreamento do anúncio assistido parcialmente.\
   Exemplo**: **O usuário ingressa no meio (em 40 segundos) de uma pausa de anúncio de 90 segundos que consiste em três anúncios de 30 segundos. Dez segundos depois do segundo anúncio no intervalo.
   * O segundo anúncio é reproduzido pela duração restante (20 segundos) seguido pelo terceiro anúncio.
   * Os rastreadores de anúncios para o anúncio parcial reproduzido (segundo anúncio) não são acionados. Os rastreadores apenas do terceiro anúncio são disparados.

* **Carregamento seguro de anúncios em HTTPS**

   O Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios primetime e CRS em https.

* **AdSystem e Creative Id adicionados às solicitações CRS**

   * Agora, incluindo &quot;AdSystem&quot; e &quot;CreativeId&quot; como novos parâmetros nas solicitações 1401 e 1403.

* **A API setEncodeUrlForTracking na classe NetworkConfiguration removida** como os caracteres não seguros em um URL devem ser codificados.

**Versão 2.5.4**

O Android TVSDK v2.5.4 oferece as seguintes atualizações e alterações de API:

* As alterações no valor padrão para o valor WebViewDebbugingWebViewDebbuging está definido como Falso por padrão. Para ativá-lo, chame setWebContentsDebuggingEnabled(true) no aplicativo.
* Atualização das versões OpenSSL e CurlAtualização do libcurl para v7.57.0 e OpenSSL para v1.0.2k.
* Acesso no nível do aplicativo para objeto de resposta VAST Introduziu uma nova API NetworkAdInfo::getVastXml() que fornece acesso ao objeto de resposta VAST ao aplicativo.

**Versão 2.5.3**

O Android TVSDK v2.5.3 oferece as seguintes atualizações e alterações de API.

* Todos os clientes TVSDK que usam CRS são incentivados a atualizar seus aplicativos com TVSDK 2.5.3.85 ou mais recente no Android. Isso será uma substituição instantânea da implementação do aplicativo existente. Após a atualização do TVSDK, verifique se há solicitações de URL criativo do CRS em uma ferramenta proxy (por exemplo: Charles) e confirme se o nome do host e a versão no caminho refletem como na estrutura de URL de amostra abaixo.

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* Agente de usuário do TVSDK personalizável: adicionamos novas APIs para personalizar os agentes do usuário.

   * setCustomUserAgent(valor String)
   * getCustomUserAgent()

* Compartilhe cookies entre o aplicativo Android e o TVSDK: O Android TVSDK agora oferece suporte ao acesso de cookies entre a camada JAVA (armazenada no CookieStore do aplicativo Android) e a camada C++ TVSDK. Agora, é possível definir e/ou modificar os cookies na camada C++ nativa, pois eles serão expostos à Loja de Cookies Java.
* Alterações de API:

   * Um novo CookiesUpdatesEvent de eventos é adicionado. Ele é despachado pelo player de mídia quando seu cookie é atualizado.
   * Uma nova API é adicionada a NetworkConfiguration::set/ getCustomUserAgent() para usar o agente de usuário personalizado.
   * Uma nova API é adicionada a NetworkConfiguration::set/ getEncodedUrlForTracking para forçar a Codificação de caracteres não seguros.
   * Uma nova API é adicionada à NetworkConfiguration::getNetworkDownVerificationUrl() para definir um URL de verificação de rede no caso de um failover.
   * Uma nova propriedade é adicionada a TextFormat::trataSpaceAsAlphaNum, que define se o espaço deve ser tratado como alfanumérico ao exibir legendas.

* Alterações em SizeAvailableEvent: Anteriormente, os métodos getHeight() e getWidth() de SizeAvailableEvent em 2.5.2 eram usados para retornar a altura e a largura do quadro, retornados pelo formato de mídia. Agora retorna a altura de saída e a largura de saída respectivamente retornadas pelo decodificador.
* Alterações no comportamento do Buffering: O comportamento de buffer é alterado. É deixada para o desenvolvedor do aplicativo no que ele quer fazer no caso de buffer vazio. 2.5.3 usa o tamanho do buffer de reprodução em uma situação vazia do buffer.

**Versão 2.5.2**

O Android TVSDK v2.5.2 oferece correções importantes de erros e algumas alterações na API.

**Versão 2.5.1**

Os novos recursos importantes lançados no Android 2.5.1.

* **Melhorias** no desempenhoA nova arquitetura TVSDK 2.5.1 traz várias melhorias no desempenho. Com base em estatísticas de um estudo de benchmarking de terceiros, a nova arquitetura oferece uma redução de 5 vezes no tempo de inicialização e de 3,8 vezes menos quadros em queda em relação à média do setor:

   * **Instant on for VOD and live -** Quando você ativa instantaneamente, o TVSDK inicializa e armazena a mídia antes do início da reprodução. Como você pode iniciar várias instâncias MediaPlayerItemLoader simultaneamente em segundo plano, é possível armazenar vários fluxos em buffer. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, a reprodução no novo canal é iniciada imediatamente. O TVSDK 2.5.1 também é compatível com o Instant On para fluxos **ao vivo** . Os fluxos ao vivo são armazenados novamente quando a janela ao vivo se move.

      * **Lógica ABR aprimorada -** a nova lógica ABR é baseada no comprimento do buffer, na taxa de alteração do comprimento do buffer e na largura de banda medida. Isso garante que o ABR escolha a taxa de bits correta quando a largura de banda flutuar e também otimiza o número de vezes que a alternância de taxa de bits realmente acontece monitorando a taxa na qual o comprimento do buffer muda.
      * **Download/sub-segmentação de segmento parcial -** o TVSDK reduz ainda mais o tamanho de cada fragmento, para iniciar a reprodução o mais rápido possível. O fragmento ts deve ter um quadro-chave a cada dois segundos.
      * **Resolução de anúncio lenta -** o TVSDK não espera pela resolução de anúncios não pré-implantados antes de iniciar a reprodução, diminuindo assim o tempo de inicialização. As APIs como busca e reprodução de truques ainda não são permitidas até que todos os anúncios sejam resolvidos. Isso se aplica aos fluxos VOD usados com CSAI. Operações como busca e avanço rápido não são permitidas até que a resolução do anúncio seja concluída. Para fluxos ao vivo, esse recurso não pode ser habilitado para a resolução de anúncios durante um evento ao vivo.
      * **Conexões de rede persistentes -** este recurso permite que o TVSDK crie e armazene uma lista interna de conexões de rede persistentes. Essas conexões são reutilizadas para várias solicitações, em vez de abrir uma nova conexão para cada solicitação de rede e depois destruí-la. Isso aumenta a eficiência e diminui a latência no código de rede, resultando em desempenho de reprodução mais rápido.
Quando o TVSDK abre uma conexão, ele solicita ao servidor uma conexão *de manutenção* . Alguns servidores podem não suportar esse tipo de conexão, caso em que o TVSDK voltará a fazer uma conexão para cada solicitação novamente. Além disso, embora as conexões persistentes estejam ativadas por padrão, o TVSDK agora tem uma opção de configuração para que os aplicativos possam desativar as conexões persistentes, se desejado.
      * **Download paralelo - O download de vídeo e áudio em paralelo em vez de em série reduz os atrasos na inicialização.** Esse recurso permite que arquivos HLS Live e VOD sejam reproduzidos, otimiza o uso da largura de banda disponível em um servidor, reduz a probabilidade de entrar em situações de buffer sem execução e minimiza o atraso entre o download e a reprodução.
      * **Downloads de anúncios paralelos - o TVSDK pré-busca anúncios em paralelo à reprodução do conteúdo antes de bater nos intervalos do anúncio, permitindo a reprodução contínua de anúncios e conteúdo.**

* **Reprodução**

   * **Reprodução de conteúdo MP4 -** Os clipes curtos de MP4 não precisam ser transcodificados novamente para reproduzir no TVSDK.
Observação: A comutação ABR, a reprodução de truques, a inserção de anúncios, o vínculo de áudio tardio e a subsegmentação não são compatíveis com a reprodução MP4.
   * **Reprodução de truques com a taxa de bits adaptável (ABR) -** Esse recurso permite que o TVSDK alterne entre fluxos de iFrame enquanto está no modo de reprodução de truques. Você pode usar perfis que não sejam iFrame para executar truques em velocidades menores.
   * **Reprodução de truques mais suave - Esses aprimoramentos aprimoram a experiência do usuário:**

          * Seleção adaptável da taxa de bits e da taxa de quadros durante a reprodução do truque, com base na largura de banda e no perfil
          de buffer* Use o fluxo principal em vez do fluxo IDR para obter uma reprodução rápida de até 30 fps.
      
* **Proteção de conteúdo**

   * **Proteção de saída com base em resolução - Esse recurso vincula restrições de reprodução a resoluções específicas, fornecendo controles de DRM com granulado mais fino.**

* **Suporte ao fluxo de trabalho**

   * **Integração de faturamento direto -** envia métricas de faturamento para o backend do Adobe Analytics, certificado pelo Adobe Primetime para fluxos usados pelo cliente.
O TVSDK coleta automaticamente métricas, respeitando o contrato de vendas do cliente para gerar relatórios de uso periódicos necessários para fins de faturamento. Em cada evento de início de fluxo, o TVSDK usa a API de inserção de dados do Adobe Analytics para enviar métricas de faturamento, como tipo de conteúdo, sinalizadores ativados para inserção de anúncio e sinalizadores habilitados para drm - com base na duração do fluxo faturável - para o conjunto de relatórios pertencente ao Adobe Analytics Primetime. Isso não interfere nem é incluído nos conjuntos de relatórios ou nas chamadas do servidor do Adobe Analytics. Mediante solicitação, este relatório de uso de faturamento é enviado periodicamente aos clientes. Esta é a primeira fase do recurso de faturamento que suporta somente faturamento de uso. Ele pode ser configurado com base no contrato de vendas usando as APIs descritas na documentação. Esse recurso é ativado por padrão. Para desativar esse recurso, consulte a amostra do player de referência.
   * **Suporte aprimorado a failover - estratégias adicionais implementadas para continuar a reprodução ininterrupta, apesar de falhas de servidores host, arquivos de lista de reprodução e segmentos.**

* **Publicidade**

   * **Integração perfeita - suporte para a avaliação da capacidade de visualização do anúncio pelo Moat** .
   * **Banners de companheiro - os banners de companheiro são exibidos ao lado de um anúncio linear e, muitas vezes, continuam a ser exibidos na exibição após o término do anúncio.** Esses banners podem ser do tipo html (um trecho HTML) ou do tipo iframe (um URL para uma página iframe).

* **Analytics**

   * **VHL 2.0 -** Esta é a mais recente integração otimizada da Biblioteca de pulsações de vídeo (VHL) para coleta automática de dados de uso do Adobe Analytics. A complexidade das APIs foi diminuída para facilitar a implementação. Baixe a biblioteca VHL [v2.0.0 para Android](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) e extraia o arquivo JAR na pasta libs.

* **SizeDisponableEventListener**
   * os métodos getHeight() e getWidth() de SizeAvailableEvent agora retornarão a saída em altura e largura respectivamente. A taxa de aspecto de exibição pode ser calculada da seguinte forma:

      ```
      SizeAvailableEvent e;
      
      DAR = e.getWidth()/ e.getHeight();
      
      Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:
      
      SAR = e.getSarWidth()/e.getSarHeight();
      
      frameHeight = e.getHeight();
      
      frameWidth = e.getWidth()/SAR;    
      ```

* **Cookies**

   * O Android TVSDK agora oferece suporte ao acesso a cookies JAVA armazenados no CookieStore do aplicativo Android. Uma API de retorno de chamada (onCookiesUpdates) é fornecida para gravar sempre que um novo cookie é fornecido como parte do cabeçalho de resposta &quot;Set-Cookie&quot;. Esses cookies estão disponíveis como uma Lista de HttpCookies usados para um URI/domínio diferente ao configurar esses valores de cookie nesse URI/domínio específico usando CookieStore. Da mesma forma, os valores de cookie no TVSDK são atualizados usando a API de adição do CookieStore.

## Matriz de recursos {#feature-matrix}

O TVSDK para Android oferece suporte a vários recursos que podem ser implementados para adicionar funcionalidade aos seus aplicativos de vídeo.

Nas tabelas de recursos abaixo, um &quot;Y&quot; indica que o recurso é suportado na versão atual.

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Reprodução geral (Reproduzir, Pausar, Buscar) | VOD + Live | Y |
| FER - Reprodução geral (Reproduzir, Pausar, Procurar) | FER VOD | Y |
| Procurar quando um anúncio está sendo reproduzido | VOD + Live | Não suportado |
| AC3 | VOD + Live | Não suportado |
| MP3 | VOD | Não suportado |
| Reprodução de conteúdo MP4 | VOD | Y |
| Lógica de troca da taxa de bits adaptável | VOD + Live | Y |
| Reprodução somente áudio | VOD + Live | Y |
| Suporte a vários CDN | VOD + Live | Não suportado |
| Reprodução de anúncios com mídia somente áudio | VOD + Live | Não suportado |
| Legendas ocultas - 608/708 | VOD + Live | Y |
| Legendas ocultas - WebVTT | VOD + Live | Y |
| Failover Manifest | VOD + Live | Y |
| Failover avançado | VOD + Live | Y |
| Notificações de QoS e player | VOD + Live | Y |
| Suporte para cabeçalhos de cookies | VOD + Live | Y |
| Suporte para cabeçalhos HTTP personalizados | VOD + Live | Y (Lista de permissões necessária) |
| Definir parâmetros de controle de buffer | VOD + Live | Y |
| Definir controles adaptáveis de taxa de bits | VOD + Live | Y |
| Tags de manifesto personalizadas | VOD + Live | Y |
| Vínculo de áudio tardio | VOD + Live | Y |
| Redirecionamento 302 | VOD + Live | Y |
| Reprodução com deslocamento | VOD + Live | Y |
| Reprodução somente áudio | VOD + Live | Y |
| Trick Play | VOD + Live | Y |
| Movimento lento na peça | VOD + Live | Não suportado |
| Reprodução suave de truques (com ABR) | VOD + Live | Y |
| Análise do ID3 | VOD + Live | Y |
| Blecaute de anúncios | VOD + Live | Não suportado |
| Instantâneo ativado | VOD + Live | Não suportado |
| Suporte ao marcador de descontinuidade | VOD + Live | Y |
| 302 Fixidade de redirecionamento | VOD + Live | Y |

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Reprodução geral, anúncios ativados | VOD + Live | Y |
| FERE conteúdo com anúncios ativados | VOD | Y |
| Comportamentos de anúncio padrão | VOD + Live | Y |
| VAST 2.0/3.0 | VOD + Live | Y |
| VMAP 1.0 | VOD + Live | Y |
| Anúncios MP4 | VOD + Live | Y (do CRS) |
| Reprodução de truques com anúncios ativada | VOD + Live | Y |
| Somente publicidade | VOD | Y |
| Parâmetros de definição de metas | VOD + Live | Y |
| Parâmetros personalizados | VOD + Live | Y |
| Comportamentos de anúncio personalizados | VOD + Live | Y |
| Tags de anúncio personalizadas | Live | Y |
| Resolvedores de anúncios personalizados | VOD + Live | Y |
| Resolvedor de anúncios personalizado do FreeWheel | VOD | Y |
| C3 | VOD + Live | Não suportado |
| Resolução de anúncios ociosa | VOD | Y |
| Suporte a marcadores de descontinuidade - SSAI | VOD + Live | Y |
| Anúncios complementares, anúncios em banner e anúncios clicáveis | VOD + Live | Y |
| VPAID 2.0 | VOD + Live | Y (JS) |
| Saída antecipada do anúncio | Live | Y |
| Priorização criativa baseada em regras | VOD + Live | Y |
| Regras CRS | VOD + Live | Y |
| JSON Ad Resolver | VOD + Live | Não suportado |
| Integração de moat | VOD + Live | Y |

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Criptografia AES | VOD + Live | Y |
| Criptografia AES de amostra | VOD + Live | Y |
| Fluxos Tokenized | VOD + Live | Y |
| DRM | VOD + Live | Somente DRM Primetime (Futuro: Widevine) |
| Reprodução externa (RBOP) | VOD + Live | Somente DRM Primetime |
| Rotação de licença | VOD + Live | Somente DRM Primetime |
| Rotação da tecla | VOD + Live | Somente DRM Primetime |

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Integração VHL do Adobe Analytics | VOD + Live | Y |
| Cobrança | VOD + Live | Y |

## Problemas resolvidos {#resolved-issues}

Quando a resolução estiver associada a um problema reportado, uma referência do Zendesk será exibida, por exemplo, ZD#xxxx

**Android TVSDK 2.7**

Esta seção fornece um resumo do problema resolvido na versão do TVSDK 2.7.

* ZD#37166 - A chamada de rastreamento de erros é acionada mesmo quando o anúncio é reproduzido corretamente.
* ZD#37134 - IDs de anúncio incorretas são retornadas, caso o anúncio em invólucro (3P) esteja presente com vários anúncios na resposta VMAP.

**Android TVSDK 2.5.6**

* ZD #34992 - O idioma está vazio em Legenda Fechada.
   * Correção de um caso em que o TVSDK não estava analisando #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS do manifesto principal para obter os detalhes do rastreamento da legenda.
* ZD #35078 - Validação P do Android.
   * O TVSDK 2.5.6 foi validado com as versões beta mais recentes do Android P. Nenhum problema encontrado devido ao novo sistema operacional Android.
* ZD #34149 - O player continua a solicitar manifestos mesmo se um erro for encontrado.
   * Corrigido o caso em que o TVSDK fazia chamadas repetitivas mesmo quando todos os perfis estavam inativos (erro 404).
* ZD #31533 - Reproduzir áudio no Android depois que o aplicativo é enviado para o plano de fundo.
   * Adição da `enableAudioPlaybackInBackground` API do MediaPlayer que deve ser chamada com &quot;True&quot; como argumento (quando o player está no estado PREPARED) para ativar a reprodução de áudio quando o aplicativo está em segundo plano.

**Android TVSDK 2.5.5**

* ZD #21647 - Android TVSDK notifica 640x368 quando o tamanho real do vídeo é 640x360.
   * Devido à variável m_nOutputHeight (dentro de AndroidMCVideoDecoder) ser atualizada com a altura do quadro em vez da altura de saída real. Alterações relevantes na função getVideoFrame foram feitas para calcular m_nOutputHeight corretamente.
* ZD #26614 - Urgente - serviço de anúncios de terceiros / programático - falha ao servir impressões.
   * Aprimoramento da correção anterior, manipulando o caso na análise XML, em que o problema era reproduzível quando &quot;space&quot; era anterior ao sinal &quot;Equal&quot;, como &lt;VAST version =&quot;2.0&quot;>
* ZD #29296 - Android: Adicione AdSystem e Creative ID às solicitações CRS.
   * Agora, incluindo &quot;AdSystem&quot; e &quot;CreativeId&quot; como novos parâmetros nas solicitações 1401 e 1403.
* ZD #33062 - O TVSDK falha na ocorrência do caractere pipe na resposta VAST em nó CDATA
   * API setEncodeUrlForTracking na classe NetworkConfiguration removida como os caracteres não seguros em um URL a ser codificado.
* ZD #33063 - A lógica de seleção de arquivo CRS foi quebrada - O TVSDK não estava enviando solicitação CRS para o formato Web, mas enviando-o para arquivos 3gpp.
   * A lógica foi corrigida agora. Ao usar arquivos de mídia com o formato webm e 3gpp, o CRS solicita que sejam enviados para o webm. E ao usar ambos os arquivos de mídia com o formato 3gpp, o CRS solicita que seja enviado para o arquivo 3gpp com taxa de bits mais alta.
* ZD #33125 - O aplicativo Android trava com uma tag DoubleClick específica no VMAP.
   * Corrigido o cenário para evitar a falha.
* ZD #32256 - Problema de rotação de licença e rotação de chave - Adobe Access.
   * Correção da inicialização de segmentos com metadados DRM para conteúdo do SampleAES. Funciona bem com conteúdo AES128.
* ZD #33619 - Encaminhamento rápido de um conteúdo crescente da lista de reprodução preso no estado de buffering próximo ao ponto ativo.
   * Tratava-se do caso ao atravessar o ponto ao vivo no modo de peça.
* ZD #34151 - Objetos TimedMetadata fora de ordem.
   * Dois eventos TimedMetadata apareciam em ordem aleatória se pertenciam ao mesmo tempo na linha do tempo. Manteve sua ordem original em manifesto.
* ZD #34189 - Problema ao tentar iniciar a pausa do anúncio.
   * O problema era com os anúncios SSAI que são costurados usando a descontinuidade. E a causa era um comportamento quando procuramos o início de tais anúncios, procuramos por um quadro-chave e não o encontramos. O motivo era que o carimbo de data e hora do áudio principal do anúncio era anterior ao carimbo de data e hora do vídeo principal. Portanto, acabamos procurando um quadro principal em um fragmentDump de dados incorreto. Corrigido agora.
* ZD #34528 - Resolução de vídeo que não atualiza além de 640x360 no dongle 3rd gen FireTV.
   * A correção foi aprimorada para incluir as atualizações de firmware mais recentes.
* ZD #34793 - TVSDK 2.5.x usado para travar com o resolvedor de conteúdo personalizado em alguns casos quando o VideoEngine presumia que as auditudeSettings estavam disponíveis e não estavam.
   * A falha ocorria devido a uma chamada de função em um ponteiro compartilhado Nulo (auditudeSettings). Adicionada uma verificação condicional em VideoEngineTimeline::placeToSourceTimeline() para garantir que auditudeSettings esteja disponível antes de chamar qualquer item nesse objeto.
* ZD #32584 - Não é possível acessar informações completas presentes no nó &lt;Extensões> de uma resposta VAST.
   * Correção do problema na análise de XML e agora NetworkAdInfo fornece as informações completas presentes no nó &lt;Extensions>.
* ZD #35086 - Não obtendo dados de extensão completos do player no caso de respostas VMAP específicas.
   * O problema era específico do xml de extensão, pois a análise XML não funcionava se o xml de extensão tivesse aspas duplas no valor do atributo. Correção do problema.

**Android TVSDK 2.5.4**

* ZenDesk#33659 - Sessão de reprodução que permite a depuração remota da visualização da Web.
   * WebViewDebbuging está definido como Falso por padrão. Para habilitar a depuração, defina como true pelo aplicativo, usando setWebContentsDebuggingEnabled(true).
* ZenDesk#33011 - A linha do tempo do anúncio não é resolvida no caso de uma solicitação CRS com falha.
   * Quando uma solicitação de CRS para um anúncio falha, a linha do tempo é resolvida e os anúncios restantes são reproduzidos.
* ZenDesk#34528 - A resolução de vídeo não atualiza além de 640x360 no dongle de terceira geração do FireTV.
   * A resolução do vídeo é alternada como interruptores de taxa de bits.
* ZenDesk#33192 - AudioTrack tem um nome nulo quando a faixa é recuperada via AudioUpdatesEventListener::onAudioUpdates.
   * Em alguns cenários no FireTV Stick, o evento onAudioUpdate estava sendo acionado quando não havia atualização de áudio real. Isto está consertado agora.

**Android TVSDK 2.5.3**

* Zendesk#32216 - A assinatura de tag personalizada TimedMetadata não está funcionando.
   * Estamos retornando dados ID3 como uma matriz de bytes (para suportar dados APIC ou genéricos) para o cliente, enquanto a sequência de caracteres 1.4 retorna. A matriz de bytes não lida com o caractere finalizado nulo, portanto, estava mostrando um caractere especial para o cliente. Esse problema foi corrigido agora.
* Zendesk#32670 - Player Not Fail Over to Redundant Playlist (O reprodutor não está passando para uma lista de reprodução redundante)
   * Isso está funcionando bem agora e setNetworkDownVerificationUrl está funcionando como esperado.
* Zendesk#32369 - A legenda fechada mostra lixo ou artefato de cores diferentes.
   * Problema com falhas de CC foi corrigido na versão mais recente
* Zendesk#25590 - Aprimoramento: Armazenamento de cookies TVSDK (C++ para JAVA)
   * O Android TVSDK agora oferece suporte ao acesso de cookies entre a camada JAVA (armazenada no CookieStore do aplicativo Android) e a camada C++ TVSDK.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 parece não ter a correção para PTPLAY-20269Esse problema foi corrigido e integrado à ramificação 2.5.2.
* Zendesk#31806 - Os paus de Auditude na PREPARINGPlayer estavam presos no estado de Preparação porque o xml de resposta tinha uma tag vazia. Agora o problema foi corrigido.
* Zendesk#31727 - Os caracteres de legenda codificada TVSDK 2.5 são descartados ou com erro ortográfico.
   * O problema foi corrigido e não estamos soltando/soltando nenhum caractere.
* Zendesk#31485 - DrmManager em 2.5
   * Ocorreu um problema em Criar DrmManager por meio do novo DrmManager (contexto de contexto). Implementada a classe DRMService que fornecia o DRMManager.
* Zendesk#32794-1080P fluxo de resolução não reproduzido no Android.
   * Alteramos os métodos SizeAvailableEvent e Previamente, getHeight() e getWidth() de SizeAvailableEvent em 2.5, usados para retornar a altura e a largura do quadro, que foram retornados pelo formato de mídia. Agora retorna a altura de saída e a largura de saída respectivamente retornadas pelo decodificador.
* O Zendesk #19359 Flash Player trava devido à posição do atributo #EXT-X-FAXS-CM no manifesto de nível definido.
   * A tag #EXT-X-FAXS-CM deve sempre aparecer na lista de reprodução superior antes que a taxa de bits individual ou os segmentos apareçam na lista de reprodução.

**Android TVSDK 2.5.2**

* Zendesk#17305 Artefatos em legendas fechadas com fundo não opaco.
a propriedade setTreatSpaceAsAlphaNum em TextFormat é exposta. Por padrão, a propriedade é False. Defina a propriedade como True em um cliente para resolver o problema de espaço escuro.

* A tela do Zendesk#25097 CC tem artefatos visuais com configurações de CC.
a propriedade setTreatSpaceAsAlphaNum em TextFormat é exposta. Por padrão, a propriedade é False. Defina a propriedade como True em um cliente para resolver o problema de espaço escuro.

* A sequência de caracteres do agente do usuário do Zendesk #31620 que sai do player do TVSDK está truncada.
A string do agente do usuário não será mais truncada após 128 caracteres.
A string de versão do Adobe Primetime é adicionada ao agente do usuário do sistema.

* O evento SEEK_END ausente do Zendesk #30809 impede que o aplicativo transfira para um estado de reprodução.
* A cor &#39;ciano&#39; da legenda fechada #30415 agora é uma matiz mais escura de azul (turquesa), em comparação com as versões anteriores do Primetime TVSDK.

   A cor muda de DarkCyan para Cyan.

* Os anúncios VOD do Zendesk #30727 não estão sendo baixados/resolvidos.

   No XML VMAP, se houver uma tag VAST vazia sem uma tag de fechamento explícita (‘&lt;/VAST>&#39;) e sem um caractere de nova linha depois dela, o XML VMAP não será analisado corretamente e os anúncios podem não ser reproduzidos.

**Android TVSDK 2.5.1**

* Falha específica do dispositivo (Samsung Galaxy Tab 4); VOD DRM LBA com Auditude e clique nos anúncios.
* VHL - Chamadas de pulsação incorretas são enviadas ao iniciar o conteúdo de um deslocamento.
* Quando os anúncios VPAID são reproduzidos, as chamadas de pulsação VHL para event:type:play ad estão ausentes.
* Depois de entrar no status COMPLETE, o player volta ao status PLAYING com SKIP adBreakPolicy para anúncios posteriores.
* Os cookies não estão sendo anexados aos retornos de anúncio de saída.
* Os pontos de sinalização dos anúncios não estão visíveis.
* O HLS com uma faixa SAP EAC3 separada não será carregado.
* O player trava quando o TVSDK recebe uma tela On intent após o Media Player ser restaurado.

## Problemas conhecidos e limitações {#known-issues-and-limitations}

**Android TVSDK 2.7**

* O TVSDK 2.7 suporta resolução simultânea de até 5 anúncios.
* No caso de resposta VMAP, as chamadas de anúncio em uma única quebra de anúncio são feitas simultaneamente e as quebras de anúncio são resolvidas sequencialmente.
* No caso de FER, as chamadas de anúncio em cada oportunidade são resolvidas simultaneamente.

### Problemas conhecidos e limitações nas versões anteriores{#known-issues-limitations-previous-releases}

**Android TVSDK 2.5.6**

* Não há suporte para várias quebras de anúncio VMAP ao mesmo tempo.

**Android TVSDK 2.5.3**

Esta versão apresenta os seguintes problemas:

* A reprodução de vídeo ao vivo pode ter problemas de sincronização de áudio e vídeo em dispositivos de baixa extremidade ou condições de rede ruins.
* Para fluxos FER, virtualTime e localTime podem ser diferentes. Além disso, FER com deslocamento não funciona.
* A reprodução pode ficar travada quando o conteúdo de Áudio de Vínculo Atrasado for procurado.
* Intermitentemente, as legendas webVTT podem ficar fora de sincronia para o conteúdo LIVE.
* Intermitentemente, uma reprodução rápida de alguns quadros pode ser vista após sair de uma pausa de anúncio.
* Às vezes, o erro 303 é lançado para quebras de anúncios de invólucro triplicado, mesmo que os anúncios sejam reproduzidos.

**Android TVSDK 2.5.2**

Esta versão apresenta os seguintes problemas:

* A reprodução de vídeo ao vivo pode ter problemas de sincronização de áudio e vídeo em dispositivos de baixa definição.
* A reprodução pode ser interrompida em momentos de busca até o fim da mídia VOD.
* Para fluxos FER, virtualTime e localTime podem ser diferentes. Além disso, FER com deslocamento não funciona.

**Android TVSDK 2.5.1**

Esta versão do TVSDK apresenta os seguintes problemas:

* A reprodução de vídeo ao vivo pode ter problemas de sincronização de áudio e vídeo em dispositivos de baixa definição.
* Para fluxos FER, virtualTime e localTime podem ser diferentes. Além disso, FER com deslocamento não funciona.
* No XML VMAP, se houver uma tag VAST vazia sem uma tag de fechamento explícita (&lt;/VAST>) e sem uma nova linha após ela, o XML VMAP não será analisado corretamente e os anúncios podem não ser reproduzidos.
* Não há suporte para VPAID pós-roll.

## Recursos úteis {#helpful-resources}

* [Requisitos do sistema](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2_7-requirements.html)
* [TVSDK 2.7 para Guia do programador do Android](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2_7-overview-prod-audience-guide.html)
* [TVSDK Android Javadoc para referência de API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html)
* [Documento](https://help.adobe.com/en_US/primetime/api/psdk/cpp/namespaces.html) da API do Android C++ TVSDK - Cada classe Java tem uma classe C++ correspondente e a documentação do C++ contém mais material explicativo do que o Javadocs, portanto, consulte a documentação do C++ para obter uma compreensão mais profunda da API do Java.
* [Guia de migração do TVSDK 1.4 a 2.5 para Android (Java)](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* Para lidar com cenários de ativação/desativação da tela, consulte o `Application_Changes_for_Screen_On_Off.pdf` arquivo incluído na compilação.
* Consulte a documentação de ajuda completa na página Aprendizagem e suporte [do](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.