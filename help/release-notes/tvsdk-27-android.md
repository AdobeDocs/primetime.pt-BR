---
title: Notas de versão do TVSDK 2.7 para Android™
description: As Notas de versão do TVSDK 2.7 para Android™ descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas de dispositivo no TVSDK Android™ 2.7
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '4037'
ht-degree: 0%

---

# Notas de versão do TVSDK 2.7 para Android™ {#tvsdk-for-android-release-notes}

As Notas de versão do TVSDK 2.7 para Android™ descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas de dispositivo no TVSDK Android™ 2.7

## TVSDK Android™ 2.7 {#tvsdk-android}

O reprodutor de referência Android™ está incluído com o Android™ TVSDK no diretório samples/ da sua distribuição. O arquivo README&lt;.md que o acompanha explica como criar o reprodutor de referência.

>[!NOTE]
>
>Para criar com sucesso o reprodutor de referência, conforme descrito no arquivo README.md distribuído com o lançamento, faça o seguinte:
>
>1. Baixar VideoHeartbeat.jar de [https://github.com/Adobe-Marketing-Cloud/media-sdks/releases](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) (Biblioteca do VideoHeartbeat para Android™ v2.0.0)
>1. Extraia VideoHeartbeat.jar para a pasta libs/.
>

## Novos recursos {#new-features}

O TVSDK 2.7 para Android™ inclui todos os recursos da versão 1.4, exceto os recursos não suportados listados em [Matriz de recursos](#feature-matrix).

**Android™ TVSDK 2.7**

* **Suporte para resolução de anúncios paralelos**

O TVSDK 2.7 é compatível com a resolução simultânea de todas as solicitações de anúncio em um Ad break, em vez da resolução sequencial.

### Novos recursos nas versões anteriores {#new-features-previous-releases}

**Versão 2.5.6**

* **O TVSDK 2.5 é compatível com Android™ P**
* **Habilitar áudio de fundo**

  Para habilitar a reprodução de áudio quando o aplicativo muda do primeiro para o segundo plano, o aplicativo deve chamar a API enableAudioPlaybackInBackground do MediaPlayer com true como argumento quando o player estiver no estado PREPARED.

* **alwaysUseAudioOutputLatency(boolean val) na classe MediaPlayer**

Quando definido, use a latência de saída no cálculo do carimbo de data e hora de áudio.
Valor de parâmetros booleanos - True usa a latência de saída de áudio no cálculo do carimbo de data e hora de áudio.

* **Otimizado para obter a melhor experiência de reprodução, mesmo que a velocidade da largura de banda diminua repentinamente.**
O TVSDK agora cancela o download do segmento em andamento, se necessário, e alterna dinamicamente para a representação apropriada. Isso é feito alternando perfeitamente entre as taxas de bits sem interrupções.

**Versão 2.5.5**

* **Inserção de ad-break parcial**

  Experiência semelhante à de TV ao ingressar no meio de um anúncio sem disparar o rastreamento do anúncio parcialmente assistido.\
  Exemplo: o usuário se junta ao meio (a 40 segundos) de um ad break de 90 segundos que consiste em três anúncios de 30 segundos. São 10 segundos do segundo anúncio no intervalo.
   * O segundo anúncio é reproduzido pelo tempo restante (20 segundos) seguido pelo terceiro anúncio.
   * Os rastreadores de anúncios do anúncio parcial reproduzido (segundo anúncio) não são acionados. Os rastreadores somente para o terceiro anúncio são acionados.

* **Carregamento de anúncio seguro em HTTPS**

  O Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios do primetime e CRS em https.

* **AdSystem e ID de criação adicionados às solicitações do CRS**

   * Agora incluindo `AdSystem` e `CreativeId` como novos parâmetros nas solicitações 1401 e 1403.

* **API setEncodeUrlForTracking na classe NetworkConfiguration removida** como os caracteres inseguros em um URL devem ser codificados.

**Versão 2.5.4**

O Android™ TVSDK v2.5.4 oferece as seguintes atualizações e alterações de API:

* Alterações no valor padrão de `WebViewDebbuging`

  A variável `WebViewDebbuging` o valor está definido como _Falso_ por padrão. Para ativá-lo, chame `setWebContentsDebuggingEnabled` para _True_ na petição.

* Atualização da versão do OpenSSL e do Curl atualizada `libcurl` para v7.57.0 e OpenSSL para v1.0.2k.
* Acesso em nível de aplicativo para objeto de resposta VAST Introduziu uma nova API NetworkAdInfo::getVastXml() que fornece acesso do objeto de resposta VAST ao aplicativo.

**Versão 2.5.3**

O Android™ TVSDK v2.5.3 oferece as seguintes atualizações e alterações de API.

* Todos os clientes de TVSDK que usam CRS são incentivados a atualizar seus aplicativos com TVSDK 2.5.3.85 ou mais recente no Android™. Esta é uma substituição suspensa da implementação do aplicativo existente. Após a atualização do TVSDK, verifique as solicitações do URL criativo do CRS em uma ferramenta de proxy (por exemplo: Charles) e confirme se o nome do host e a versão no caminho refletem como na estrutura de URL de exemplo abaixo.

  `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* Personalizável Agente do usuário do TVSDK: adicionamos algumas novas APIs para personalizar os agentes do usuário.

   * `setCustomUserAgent`(Valor da string)
   * `getCustomUserAgent`()

* Compartilhar cookies entre o aplicativo Android™ e o TVSDK: o Android™ TVSDK agora oferece suporte ao acesso de cookies entre a camada Java™ (armazenada no CookieStore do aplicativo Android™) e a camada C++ TVSDK. Agora, é possível definir e/ou modificar os cookies na camada nativa do C++, conforme eles são expostos ao Java™ Cookie Store.
* Alterações na API:

   * Um novo Evento CookiesUpdatedEvent é adicionado. Ele é despachado pelo reprodutor de mídia quando o cookie é atualizado.
   * Uma nova API é adicionada ao `NetworkConfiguration::set/ getCustomUserAgent()` para usar o agente de usuário personalizado.
   * Uma nova API é adicionada ao `NetworkConfiguration::set/ getEncodedUrlForTracking` para forçar a codificação de caracteres inseguros.
   * Uma nova API é adicionada ao `NetworkConfiguration::getNetworkDownVerificationUrl()` para definir um URL de verificação de rede se houver um failover.
   * Uma nova propriedade é adicionada a TextFormat::treatmentSpaceAsAlphaNum, que define se o espaço deve ser tratado como alfanumérico ao exibir legendas.

* Alterações em `SizeAvailableEvent`: anteriormente, os métodos getHeight() e getWidth() de `SizeAvailableEvent` na versão 2.5.2, costumava retornar a altura e a largura do quadro, retornadas pelo formato de mídia. Agora, retorna a altura e a largura da saída retornadas pelo decodificador, respectivamente.
* Alterações no comportamento de buffering: o comportamento de buffering é alterado. Fica a cargo do desenvolvedor do aplicativo o que ele deseja fazer se o buffer estiver vazio. O 2.5.3 usa o tamanho do buffer de reprodução em uma situação de buffer vazio.

**Versão 2.5.2**

O Android™ TVSDK v2.5.2 oferece correções de erros importantes e algumas alterações na API.

**Versão 2.5.1**

Os novos recursos importantes lançados no Android™ 2.5.1.

* **Melhorias de desempenho** A nova arquitetura TVSDK 2.5.1 traz várias melhorias de desempenho. Com base em estatísticas de um estudo de benchmarking de terceiros, a nova arquitetura oferece uma redução de 5x no tempo de inicialização e de 3,8x menos quadros ignorados em comparação com a média do setor:

   * **Instantâneo para VOD e live -** Quando você ativa o recurso de ativação instantânea, o TVSDK inicializa e armazena em buffer a mídia antes do início da reprodução. Como é possível iniciar várias ocorrências de MediaPlayerItemLoader simultaneamente em segundo plano, você pode armazenar vários fluxos em buffer. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, a reprodução no novo canal é iniciada imediatamente. O TVSDK 2.5.1 também é compatível com Ativo instantâneo para **live** transmissões também. Os fluxos ativos são colocados em buffer novamente quando a janela ativa se move.

      * **Lógica ABR aprimorada -** A nova lógica ABR é baseada no comprimento do buffer, na taxa de alteração do comprimento do buffer e na largura de banda medida. Isso garante que o ABR escolha a taxa de bits certa quando a largura de banda flutuar e também otimize o número de vezes que o switch de taxa de bits realmente ocorre, monitorando a taxa em que o comprimento do buffer muda.
      * **Download parcial de segmento / Subsegmentação -** O TVSDK reduz ainda mais o tamanho de cada fragmento para iniciar a reprodução o mais rápido possível. O fragmento ts deve ter um quadro principal a cada dois segundos.
      * **Resolução de anúncio lento -** O TVSDK não espera a resolução de anúncios não precedentes antes de iniciar a reprodução, diminuindo assim o tempo de inicialização. APIs como busca e truque ainda não são permitidas até que todos os anúncios sejam resolvidos. Isso se aplica aos fluxos de VOD usados com o CSAI. Operações como busca e avanço rápido não são permitidas até que a resolução do anúncio seja concluída. Para transmissões ao vivo, esse recurso não pode ser ativado para resolução de anúncios durante um evento ao vivo.
      * **Conexões de rede persistentes -** Esse recurso permite que o TVSDK crie e armazene uma lista interna de conexões de rede persistentes. Essas conexões são reutilizadas para várias solicitações, em vez de abrir uma nova conexão para cada solicitação de rede e destruí-la posteriormente. Isso aumenta a eficiência e diminui a latência no código de rede, resultando em um desempenho de reprodução mais rápido.
Quando o TVSDK abre uma conexão, ele solicita um *keep-alive* conexão. Alguns servidores podem não suportar esse tipo de conexão, nesse caso, o TVSDK voltará a fazer uma conexão para cada solicitação novamente. Além disso, enquanto as conexões persistentes estiverem ativadas por padrão, o TVSDK agora terá uma opção de configuração para que os aplicativos possam desativar as conexões persistentes, se desejado.
      * **Download paralelo -** O download de vídeo e áudio em paralelo em vez de em série reduz os atrasos de inicialização. Esse recurso permite que arquivos HLS Live e VOD sejam reproduzidos, otimiza o uso da largura de banda disponível de um servidor, reduz a probabilidade de entrar em situações de buffer em execução e minimiza o atraso entre o download e a reprodução.
      * **Downloads de anúncios paralelos -** O TVSDK busca previamente os anúncios em paralelo à reprodução do conteúdo antes de atingir os ad breaks, permitindo assim a reprodução contínua de anúncios e conteúdo.

* **Reprodução**

   * **Reprodução de conteúdo MP4 -** Os clipes curtos MP4 não precisam ser retranscodificados para serem reproduzidos no TVSDK.
Observação: não há suporte para switching ABR, reprodução de truque, inserção de anúncio, associação de áudio tardia e subsegmentação na reprodução MP4.
   * **Truque com a taxa de bits adaptável (ABR) -** Esse recurso permite que o TVSDK alterne entre fluxos do iFrame no modo de reprodução de truque. Você pode usar perfis que não sejam do iFrame para executar truques em velocidades mais baixas.
   * **Jogo de truque mais suave -** Essas melhorias melhoram a experiência do usuário:

         * Taxa de bits adaptável e seleção da taxa de quadros durante a execução do truque, com base na largura de banda e no perfil de buffer
         * Uso da transmissão principal em vez da transmissão IDR para obter até 30 fps de reprodução rápida.
     
* **Proteção de conteúdo**

   * **Proteção de saída com base em resolução -** Esse recurso vincula as restrições de reprodução a resoluções específicas, fornecendo controles DRM mais refinados.

* **Suporte a workflow**

   * **Integração de faturamento direto -** Isso envia métricas de cobrança para o back-end do Adobe Analytics, que é certificado pela Adobe Primetime para fluxos usados pelo cliente.
O TVSDK coleta métricas automaticamente, cumprindo o contrato de vendas do cliente para gerar relatórios de uso periódicos necessários para fins de faturamento. Em cada evento de início de fluxo, o TVSDK usa a API de inserção de dados do Adobe Analytics para enviar métricas de faturamento, como tipo de conteúdo, sinalizadores habilitados para inserção de anúncio e sinalizadores habilitados para drm, com base na duração do fluxo faturável, para o conjunto de relatórios do Adobe Analytics Primetime. Isso não interfere ou é incluído nos conjuntos de relatórios ou chamadas de servidor do próprio cliente do Adobe Analytics. Quando solicitado, esse relatório de uso de faturamento é enviado periodicamente aos clientes. Esta é a primeira fase do recurso de faturamento que suporta somente faturamento de uso. Ele pode ser configurado com base no contrato de vendas usando as APIs descritas na documentação. Esse recurso é ativado por padrão. Para desativar esse recurso, consulte a amostra do reprodutor de referência.
   * **Melhor suporte a failover -** Estratégias adicionais implementadas para continuar a reprodução ininterrupta, apesar das falhas de servidores host, arquivos de lista de reprodução e segmentos.

* **Publicidade**

   * **Integração do Mat -** Suporte para medição de visibilidade de anúncio do Mat.
   * **Banners complementares -** Banners de companhia são exibidos ao lado de um anúncio linear e geralmente continuam a ser exibidos na visualização após o fim do anúncio. Esses banners podem ser do tipo html (um trecho de HTML) ou do tipo iframe (um URL para uma página iframe).

* **Analytics**

   * **VHL 2.0 -** Esta é a integração otimizada mais recente da Biblioteca de heartbeats de vídeo (VHL) para a coleta automática de dados de uso do Adobe Analytics. A complexidade das APIs foi reduzida para facilitar a implementação. Baixar a biblioteca do VHL [v2.0.0 para Android™](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) e extraia o arquivo JAR na pasta libs.

* **SizeAvailableEventListener**
   * Os métodos getHeight() e getWidth() de SizeAvailableEvent agora retornam a saída em altura e largura, respectivamente. A taxa de proporção de exibição pode ser calculada da seguinte maneira:

     ```
     SizeAvailableEvent e;
     
     DAR = e.getWidth()/ e.getHeight();
     
     Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:
     
     SAR = e.getSarWidth()/e.getSarHeight();
     
     frameHeight = e.getHeight();
     
     frameWidth = e.getWidth()/SAR;    
     ```

* **Cookies**

   * O Android™ TVSDK agora oferece suporte ao acesso a cookies Java™ armazenados no CookieStore do aplicativo Android™. Uma API de retorno de chamada (onCookiesUpdated) é fornecida para registrar sempre que um novo cookie vem como parte do cabeçalho de resposta &quot;Set-Cookie&quot;. Esses cookies estão disponíveis como uma Lista de cookies HTTP usados para um URI/domínio diferente definindo esses valores de cookies nesse URI/domínio específico usando o CookieStore. Da mesma forma, os valores de cookie no TVSDK são atualizados usando a API de adição do CookieStore.

## Matriz de recursos {#feature-matrix}

O TVSDK para Android™ oferece suporte a vários recursos que você pode implementar para adicionar funcionalidade a seus aplicativos de vídeo.

Nas tabelas de recursos abaixo, um &quot;Y&quot; indica que o recurso é compatível na versão atual.

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Reprodução geral (Reproduzir, Pausar, Buscar) | VOD + Ao vivo | Y |
| FER - Reprodução geral (Reproduzir, Pausar, Buscar) | FER VOD | Y |
| Buscar quando um anúncio estiver sendo reproduzido | VOD + Ao vivo | Não suportado |
| AC3 | VOD + Ao vivo | Não suportado |
| MP3 | VOD | Não suportado |
| Reprodução de conteúdo MP4 | VOD | Y |
| Lógica de comutação de taxa de bits adaptável | VOD + Ao vivo | Y |
| Reprodução somente de áudio | VOD + Ao vivo | Y |
| Suporte a vários CDNs | VOD + Ao vivo | Não suportado |
| Reprodução de anúncios com mídia somente de áudio | VOD + Ao vivo | Não suportado |
| Legendas codificadas - 608/708 | VOD + Ao vivo | Y |
| Legendas codificadas - WebVTT | VOD + Ao vivo | Y |
| Failover do manifesto | VOD + Ao vivo | Y |
| Failover avançado | VOD + Ao vivo | Y |
| Notificações de QoS e player | VOD + Ao vivo | Y |
| Suporte para cabeçalhos de cookie | VOD + Ao vivo | Y |
| Suporte para cabeçalhos HTTP personalizados | VOD + Ao vivo | Y (é necessário incluir na lista de permissões) |
| Definir parâmetros de controle de buffer | VOD + Ao vivo | Y |
| Definir controles de taxa de bits adaptáveis | VOD + Ao vivo | Y |
| Tags de manifesto personalizadas | VOD + Ao vivo | Y |
| Associação de Áudio Atrasada | VOD + Ao vivo | Y |
| Redirecionamento 302 | VOD + Ao vivo | Y |
| Reprodução com Deslocamento | VOD + Ao vivo | Y |
| Reproduzir apenas áudio | VOD + Ao vivo | Y |
| Truque Play | VOD + Ao vivo | Y |
| Câmera lenta em truques | VOD + Ao vivo | Não suportado |
| Truque suave (com ABR) | VOD + Ao vivo | Y |
| Análise de ID3 | VOD + Ao vivo | Y |
| Blecaute de anúncios | VOD + Ao vivo | Não suportado |
| Instantâneo | VOD + Ao vivo | Não suportado |
| Suporte a marcador de descontinuidade | VOD + Ao vivo | Y |
| 302 Fixação de redirecionamento | VOD + Ao vivo | Y |

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Reprodução geral, anúncios ativados | VOD + Ao vivo | Y |
| Conteúdo de oferta com anúncios ativados | VOD | Y |
| Comportamentos de anúncio padrão | VOD + Ao vivo | Y |
| VAST 2.0/3.0 | VOD + Ao vivo | Y |
| VMAP 1.0 | VOD + Ao vivo | Y |
| Anúncios MP4 | VOD + Ao vivo | Y (do CRS) |
| Truque Play com anúncios ativados | VOD + Ao vivo | Y |
| Somente anúncio | VOD | Y |
| Parâmetros de direcionamento | VOD + Ao vivo | Y |
| Parâmetros personalizados | VOD + Ao vivo | Y |
| Comportamentos de anúncio personalizados | VOD + Ao vivo | Y |
| Tags de anúncio personalizadas | Ao vivo | Y |
| Resolvedores de anúncios personalizados | VOD + Ao vivo | Y |
| Resolvedor de anúncios personalizados Freewheel | VOD | Y |
| C3 | VOD + Ao vivo | Não suportado |
| Resolução de anúncio lento | VOD | Y |
| Suporte a marcador de descontinuidade - SSAI | VOD + Ao vivo | Y |
| Anúncios complementares, anúncios de banner e anúncios clicáveis | VOD + Ao vivo | Y |
| VPAID 2.0 | VOD + Ao vivo | Y (JS) |
| Saída antecipada do anúncio | Ao vivo | Y |
| Priorização criativa baseada em regras | VOD + Ao vivo | Y |
| Regras CRS | VOD + Ao vivo | Y |
| Resolvedor de anúncios JSON | VOD + Ao vivo | Não suportado |
| Integração do Mat | VOD + Ao vivo | Y |

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Criptografia AES | VOD + Ao vivo | Y |
| Exemplo de criptografia AES | VOD + Ao vivo | Y |
| Fluxos Tokenizados | VOD + Ao vivo | Y |
| DRM | VOD + Ao vivo | Somente DRM do Primetime (Futuro: Widevine) |
| Reprodução externa (RBOP) | VOD + Ao vivo | Somente DRM do Primetime |
| Rotação de licenças | VOD + Ao vivo | Somente DRM do Primetime |
| Rotação de chaves | VOD + Ao vivo | Somente DRM do Primetime |

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Integração com o Adobe Analytics VHL | VOD + Ao vivo | Y |
| Faturamento | VOD + Ao vivo | Y |

## Problemas resolvidos {#resolved-issues}

Quando a resolução estiver associada a um problema relatado, uma referência do Zendesk será exibida, por exemplo, ZD#xxxxx

**Android™ TVSDK 2.7**

Esta seção fornece um resumo do problema resolvido na versão do TVSDK 2.7.

* ZD#37166 - A chamada de rastreamento de erro é disparada mesmo quando o anúncio é reproduzido sem problemas.
* ZD#37134 - IDs de anúncio incorretas são retornadas, no caso, o anúncio wrapper(3P) está presente com vários anúncios na resposta do VMAP.

**Android™ TVSDK 2.5.6**

* ZD #34992 - O idioma está vazio nas Legendas ocultas.
   * Correção de um problema em que o TVSDK não analisava #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS do manifesto principal para obter os detalhes de rastreamento da legenda.
* ZD #35078 - Validação do Android P.
   * O TVSDK 2.5.6 foi validado com as compilações beta mais recentes do Android™ P. Nenhum problema encontrado devido ao novo sistema operacional Android™.
* ZD #34149 - O player continua solicitando manifestos mesmo se um erro for encontrado.
   * Correção do problema em que o TVSDK fazia chamadas repetitivas mesmo quando todos os perfis estavam inativos (erro 404).
* ZD #31533 - Reproduzindo áudio no Android™ depois que o aplicativo é enviado para o plano de fundo.
   * Adicionado `enableAudioPlaybackInBackground` API do MediaPlayer que deve ser chamado com &quot;True&quot; como argumento (quando o player estiver no estado PREPARED) para ativar a reprodução de áudio quando o aplicativo estiver em segundo plano.

**Android™ TVSDK 2.5.5**

* ZD #21647 - O Android TVSDK notifica 640x368 quando o tamanho real do vídeo é 640x360.
   * Devido à variável m_nOutputHeight (dentro do AndroidMCVideoDecoder) sendo atualizada com a altura do quadro em vez da altura de saída real. Alterações relevantes feitas na função getVideoFrame para calcular m_nOutputHeight corretamente.
* ZD #26614 - Urgente — veiculação de anúncios de terceiros/programática — falha ao veicular impressões.
   * Correção anterior aprimorada ao manipular o caso na análise XML, em que o problema era reproduzível quando &quot;espaço&quot; estava antes do sinal &quot;igual&quot;, como &lt;vast version=&quot;2.0&quot;>
* ZD #29296 - Android: adicionar AdSystem e ID criativa às solicitações do CRS.
   * Agora inclui &quot;AdSystem&quot; e &quot;CreativeId&quot; como novos parâmetros nas solicitações 1401 e 1403.
* ZD #33062 - O TVSDK trava na ocorrência do caractere de pipe na resposta VAST no nó CDATA
   * API setEncodeUrlForTracking na classe NetworkConfiguration removida como os caracteres inseguros em um URL a ser codificado.
* ZD #33063 - A lógica de seleção de arquivo CRS foi interrompida - O TVSDK não estava enviando a solicitação CRS para o formato webm, mas sim enviando-a para arquivos 3gpp.
   * Correção da lógica agora. Ao usar arquivos de mídia com o formato webm e 3gpp, a solicitação de CRS é enviada para webm. E ao usar ambos os arquivos de mídia com formato 3gpp, a solicitação CRS é enviada para o arquivo 3gpp com a taxa de bits mais alta.
* ZD #33125 - O aplicativo Android trava com a tag DoubleClick específica no VMAP.
   * Corrigido o cenário para evitar a falha.
* ZD #32256 - License Rotation &amp; Key Rotation Issue - Acesso ao Adobe.
   * Correção da inicialização de segmentos com os metadados DRM para o conteúdo SampleAES. Funciona bem com conteúdo AES128.
* ZD #33619 - Encaminhamento rápido de um conteúdo de lista de reprodução em crescimento preso no estado de buffering próximo a um ponto ativo.
   * Caso tratado ao cruzar o ponto ao vivo no modo de truque de reprodução.
* ZD #34151 - Objetos TimedMetadata fora de ordem.
   * Dois eventos TimedMetadata apareciam em ordem aleatória se pertencessem ao mesmo tempo na linha do tempo. Manutenção do pedido original no manifesto.
* ZD #34189 - Problema ao tentar iniciar o ad break.
   * O problema era com anúncios SSAI que são compilados usando descontinuidade. E a causa foi um comportamento quando procuramos o início de tais anúncios, procuramos por um quadro-chave e não o encontramos. O motivo era o carimbo de data e hora mín. do áudio do anúncio antes do carimbo de data e hora mín. do vídeo. Portanto, acabamos pesquisando um quadro principal em um fragmento de dados de Dump incorreto. Corrigido agora.
* ZD #34528 - A resolução de vídeo não atualiza além de 640x360 no dongle de terceira geração FireTV.
   * Correção aprimorada para incluir as atualizações de firmware mais recentes.
* ZD #34793 - O TVSDK 2.5.x costumava falhar com o resolvedor de conteúdo personalizado às vezes, quando o VideoEngine assumia que as auditudeSettings estavam disponíveis e não estavam.
   * A falha ocorria devido a uma chamada de função em um ponteiro Nulo compartilhado (auditudeSettings). Adição de uma verificação condicional em VideoEngineTimeline::placeToSourceTimeline() para garantir que auditudeSettings esteja disponível antes de chamar qualquer coisa nesse objeto.
* ZD #32584 - Não é possível acessar informações completas presentes no &lt;extensions> nó de uma resposta VAST.
   * Corrigido o problema de análise XML e agora NetworkAdInfo fornece as informações completas presentes na &lt;extensions> nó.
* ZD #35086 - Não obtendo dados de extensão completos do player se houver respostas VMAP específicas.
   * O problema era específico do xml de extensão, pois a análise XML não funcionava se o xml de extensão tivesse aspas duplas no valor do atributo. Correção do problema.

**Android™ TVSDK 2.5.4**

* ZenDesk#33659 - Sessão de reprodução que habilita a depuração remota do webview.
   * WebViewDebuging está definido como Falso por padrão. Para habilitar a depuração, defina como true por meio do aplicativo, usando setWebContentsDebuggingEnabled(true).
* ZenDesk#33011 - A linha do tempo do anúncio não é resolvida se houver uma solicitação CRS com falha.
   * Quando uma solicitação do CRS para um anúncio falha, a linha do tempo é resolvida e os anúncios restantes são reproduzidos.
* ZenDesk#34528 - A resolução de vídeo não atualiza além de 640x360 no dongle de terceira geração FireTV.
   * Os switches de resolução de vídeo são ativados como switches de taxa de bits.
* ZenDesk#33192 - AudioTrack tem nome nulo quando a faixa é recuperada via AudioUpdatedEventListener::onAudioUpdated.
   * Em alguns cenários no FireTV Stick, o evento onAudioUpdate estava sendo acionado quando não havia nenhuma atualização de áudio real. Isso foi corrigido agora.

**Android™ TVSDK 2.5.3**

* Zendesk#32216 - A assinatura de tag personalizada TimedMetadata não está funcionando.
   * Retornamos dados ID3 como uma matriz de bytes (para oferecer suporte a APIC ou dados genéricos) ao cliente, enquanto na sequência de retorno 1.4. A matriz de bytes não lida com o próprio caractere terminado por nulo, portanto, mostrava o caractere especial ao cliente. Esse problema foi corrigido agora.
* Zendesk#32670 - Player não falha na lista de reprodução redundante
   * Isso está funcionando bem agora e setNetworkDownVerificationUrl está funcionando como esperado.
* Zendesk#32369 - A legenda oculta mostra lixo de cores ou artefato diferentes.
   * Problema com falhas CC foi corrigido na última build
* Zendesk#25590 - Aprimoramento: loja de cookies TVSDK (C++ para Java™)
   * O Android™ TVSDK agora é compatível com o acesso de cookies entre a camada Java™ (armazenada no CookieStore do aplicativo Android™) e a camada C++ TVSDK.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 não parece ter a correção para PTPLAY-20269 Esse problema foi corrigido e integrado à ramificação 2.5.2.
* Zendesk#31806 - Auditude sticks em PREPARING Player ficou preso no estado Preparing porque o xml de resposta tinha uma tag vazia. Agora o problema foi corrigido.
* Zendesk#31727 - Os caracteres de legendas ocultas do TVSDK 2.5 são soltos ou digitados incorretamente.
   * Problema corrigido e não estamos soltando/digitando nenhum caractere incorretamente.
* Zendesk#31485 - DrmManager in 2.5
   * Ocorreu um problema ao Criar o DrmManager por meio do novo DrmManager(Context context). Implementação da classe DRMService que forneceria o DRMSanager.
* Zendesk#32794- Fluxo de resolução de 1080P não está sendo reproduzido no Android™.
   * Alteramos SizeAvailableEvent. Anteriormente, `getHeight()` e `getWidth()` Os métodos de SizeAvailableEvent no 2.5 usados para retornar a altura e a largura do quadro retornadas pelo formato de mídia. Ele agora retorna a altura e a largura da saída respectivamente retornadas pelo decodificador.
* O Flash Player do Zendesk #19359 falha devido à posição do atributo #EXT-X-FAXS-CM no manifesto de nível de conjunto.
   * A tag #EXT-X-FAXS-CM deve sempre aparecer na lista de reprodução principal antes que a taxa de bits ou os segmentos individuais apareçam na lista de reprodução.

**Android™ TVSDK 2.5.2**

* Zendesk#17305 Artefatos em legendas ocultas com fundo não opaco.
A propriedade setTreatSpaceAsAlphaNum em TextFormat está exposta. Por padrão, a propriedade é False. Defina a propriedade como True em um cliente para resolver o problema de espaço escuro.

* A exibição Zendesk#25097 CC tem artefatos visuais com configurações CC.
A propriedade setTreatSpaceAsAlphaNum em TextFormat está exposta. Por padrão, a propriedade é False. Defina a propriedade como True em um cliente para resolver o problema de espaço escuro.

* A sequência de agente do usuário do Zendesk #31620 que sai do player TVSDK está truncada.
A sequência de agente do usuário não será mais truncada após 128 caracteres.
A sequência de caracteres da versão do Adobe Primetime é adicionada ao agente do usuário do sistema.

* Zendesk #30809 Evento SEEK_END ausente impede que o aplicativo transite para um estado de reprodução.
* A cor &#39;Ciano&#39; da legenda oculta Zendesk #30415 agora é um tom mais escuro de azul (turquesa), em comparação às versões anteriores do Primetime TVSDK.

  A cor é alterada de Ciano escuro para Ciano.

* Os anúncios de VOD do Zendesk #30727 não estão sendo baixados/resolvidos.

  No XML do VMAP, se houver uma tag VAST vazia sem uma tag de fechamento explícita (‘&lt;/vast>&#39;) e sem um caractere de nova linha depois dele, o XML do VMAP não é analisado corretamente e os anúncios podem não ser reproduzidos.

**Android™ TVSDK 2.5.1**

* Falha específica do dispositivo (Samsung Galaxy Tab 4); LBA DRM VOD com Auditude e clique em anúncios.
* VHL - Chamadas de heartbeat incorretas são enviadas ao iniciar o conteúdo a partir de um deslocamento.
* Quando os anúncios VPAID são reproduzidos, o heartbeat do VHL chama para o evento:type:não estão presentes anúncios.
* Depois de entrar no status COMPLETO, o reprodutor volta para o status REPRODUZINDO com IGNORAR adBreakPolicy para anúncios posteriores.
* Os cookies não estão sendo anexados a retornos de chamada de anúncios de saída.
* Os pontos de sinalização de anúncios não estão visíveis.
* O HLS com o rastreamento SAP EAC3 separado não será carregado.
* O player trava quando o TVSDK recebe uma intenção Tela ativada após a restauração do reprodutor de mídia.

## Problemas conhecidos e limitações {#known-issues-and-limitations}

**Android™ TVSDK 2.7**

* O TVSDK 2.7 oferece suporte à resolução simultânea de até cinco anúncios.
* No caso de uma resposta VMAP, as chamadas de Anúncio em um único Ad break ocorrem simultaneamente e os Ad breaks são resolvidos sequencialmente.
* No caso de uma FER, as chamadas de anúncio em cada oportunidade são resolvidas simultaneamente.

### Problemas conhecidos e limitações nas versões anteriores{#known-issues-limitations-previous-releases}

**Android™ TVSDK 2.5.6**

* Não há suporte para várias interrupções de anúncios VMAP ao mesmo tempo.

**Android™ TVSDK 2.5.3**

Essa versão tem os seguintes problemas:

* A reprodução de vídeo ao vivo pode ter problemas de sincronização de áudio-vídeo em dispositivos low-end ou condições de rede ruins.
* Para fluxos FER, virtualTime e localTime podem diferir. Além disso, o FER com offset não funciona.
* A reprodução pode ficar paralisada quando o conteúdo do Áudio de vinculação tardia é buscado.
* Intermitentemente, as legendas webVTT podem ficar fora de sincronia para o conteúdo LIVE.
* Intermitentemente, a reprodução rápida de alguns quadros pode ser vista depois de sair de um ad break.
* Às vezes, o erro 303 é lançado para Ad Breaks de invólucro triplo, mesmo que Anúncios sejam reproduzidos.

**Android™ TVSDK 2.5.2**

Essa versão tem os seguintes problemas:

* A reprodução de vídeo ao vivo pode ter problemas de sincronização de áudio e vídeo em dispositivos low-end.
* A reprodução pode parar quando se tenta encerrar a mídia de VOD.
* Para fluxos FER, virtualTime e localTime podem diferir. Além disso, o FER com offset não funciona.

**Android™ TVSDK 2.5.1**

Essa versão do TVSDK apresenta os seguintes problemas:

* A reprodução de vídeo ao vivo pode ter problemas de sincronização de áudio e vídeo em dispositivos low-end.
* Para fluxos FER, virtualTime e localTime podem diferir. Além disso, o FER com offset não funciona.
* No XML do VMAP, se houver uma tag VAST vazia sem uma tag de fechamento explícita (&lt;/vast>) e sem uma nova linha depois dele, o XML do VMAP não é analisado corretamente e os anúncios podem não ser reproduzidos.
* Não há suporte para pós-implantação de VPAID.

## Recursos úteis {#helpful-resources}

* [Requisitos do sistema](/help/programming/tvsdk-2.7-for-android/c-psdk-android-2.7-requirements.md)
* [Guia do programador do TVSDK 2.7 para Android™](/help/programming/tvsdk-2.7-for-android/overview-prod-audience-guide/c-psdk-android-2.7-overview-prod-audience-guide.md)
* [Referência de TVSDK Android™ Javadoc para API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html)
* [Documento da API TVSDK Android™ C++](https://help.adobe.com/en_US/primetime/api/psdk/cpp/namespaces.html) - Cada classe Java™ tem uma classe C++ correspondente, e a documentação C++ contém mais material explicativo do que os documentos Java™, portanto, consulte a documentação C++ para obter uma compreensão mais profunda da API Java™.
* [Guia de migração TVSDK 1.4 para 2.5 para Android™ (Java™)](/help/migration-guides/tvsdk-14-25-android.md)
* Para lidar com cenários de ativação/desativação de tela, consulte `Application_Changes_for_Screen_On_Off.pdf` arquivo incluído na build.
* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
