---
title: Notas de versão do TVSDK 3.15 para Android
description: As Notas de versão do TVSDK 3.15 para Android descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas de dispositivo no TVSDK Android 3.15
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '5516'
ht-degree: 0%

---

# Notas de versão do TVSDK 3.15 para Android {#tvsdk-for-android-release-notes}

As Notas de versão do TVSDK 3.15 para Android descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas de dispositivo no TVSDK Android 3.15.

O reprodutor de referência do Android está incluído com o Android TVSDK no diretório samples/ da sua distribuição. O arquivo README.md que o acompanha explica como criar o reprodutor de referência.

>[!NOTE]
>
>Para criar com sucesso o reprodutor de referência, conforme descrito no arquivo README.md distribuído com o lançamento, faça o seguinte:
>
>1. Baixar VideoHeartbeat.jar de [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) (Biblioteca do VideoHeartbeat para Android v2.0.0)
>1. Extraia VideoHeartbeat.jar para a pasta libs/.

O TVSDK para Android fornece muitas melhorias de desempenho em relação às versões anteriores. Ele fornece uma experiência de visualização de alta qualidade e transporta todos os recursos da versão 1.4, com exceção do suporte a Multi-CDN.

O conjunto abrangente de recursos compatíveis e não compatíveis é apresentado no [Matriz de recursos](#feature-matrix) seção das notas de versão.

## Android TVSDK 3.15

Esta versão corrige o problema em que o aplicativo trava várias vezes quando a tag criativa está ausente ou quando [!UICONTROL url CDATA] está vazio em [!UICONTROL VAST] resposta.

Para saber mais sobre as correções de erros nesta versão e em versões anteriores, consulte [problemas corrigidos no TVSDK para Android](#resolved-issueszd).

### Novos recursos e melhorias nas versões anteriores

**Android TVSDK 3.14**

Esta versão corrige o problema em que o aplicativo falha ao [!UICONTROL CDATA] está vazio para qualquer um dos [!UICONTROL ClickTracking], [!UICONTROL CustomClick] ou [!UICONTROL CompanionClickTracking] elementos na resposta VAST.

**Android TVSDK 3.13**

O fluxo DRM Widevine congela ou mostra quadros pretos no switch ABR em dispositivos FireTV, que incluem Fire TV 3ª geração Pendant e Fire TV Cube 1ª e 2ª geração dispositivos.

Para resolver o problema, defina a API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` para os dispositivos Fire TV especificados antes de iniciar a reprodução. O valor padrão é false.

**Android TVSDK 3.12**

Versão gradle do aplicativo de referência do Primetime atualizada para a versão 5.6.4.

Para configurar e executar o aplicativo de referência usando o Android Studio, siga as instruções do arquivo ReadMe disponível com o zip do TVSDK em `TVSDK_Android_x.x.x.x/samples/PrimetimeReference/src/README.md`.

Os principais problemas de clientes corrigidos na versão atual são mencionados em [problemas resolvidos](#resolved-issues) seção.

**Android TVSDK 3.11**

* **Busca de Caixa de Cabeçalho Específico do Sistema de Proteção (PSSH) permitida** - O TVSDK permite a busca da caixa de cabeçalho específica do sistema de proteção associada ao recurso de mídia carregado no momento. Nova API `getPSSH()` adicionado a `com.adobe.mediacore.drm.DRMManager`.

Para obter mais informações, consulte [DRM Widevine](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md).

**Android TVSDK 3.10**

A versão enfocou a correção dos principais problemas dos clientes, conforme mencionado na [problemas resolvidos](#resolved-issues) seção.

**Android TVSDK 3.9**

* **Entrega segura por HTTPS** - O Android TVSDK 3.9 apresentou os recursos de entrega segura via HTTPS para fornecer conteúdo com segurança, com escala e desempenho incomparáveis.

  Para habilitar a entrega segura por HTTPS, uma nova API foi introduzida no `NetworkConfiguration` classe.

  `public void setForceHTTPS (boolean value)`

  `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **Suporte antes da exibição com o recurso Ad-Break parcial** - Com esse aprimoramento, o TVSDK 3.8 é compatível com anúncios precedentes com o recurso Ad-Break parcial (PABI).

O anúncio precedente, se disponível, é reproduzido e, em seguida, o conteúdo é reproduzido a partir do ponto ao vivo, emulando a experiência da televisão ao vivo.

**Android TVSDK 3.7**

* Para conteúdo de teste do Widevine, uma nova API `setMediaDrmCallback` na classe DRMManager é exposta para substituir a implementação padrão da interface MediaDrmCallback.

  `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* Correção de um erro AppCrash para não manusear `MediaPlayerEvent.ITEM_UPDATED` na camada C++ (Android de 64 bits).

**Android TVSDK 3.6**

* **Aprimore seus aplicativos para atender ao requisito de 64 bits** - A biblioteca nativa `(libAVEAndroid.so)` O foi atualizado e disponibilizado em duas versões. O local da biblioteca nativa armeabi (32 bits) existente foi alterado de `/framework/Player to /framework/Player/armeabi` e uma biblioteca arm64-v8a adicional (64 bits) é introduzida no `/framework/Player/arm64-v8a.`

**Versão 3.5**

* **Resolução de anúncio just-in-time** - O TVSDK 3.5 remove o suporte dos anúncios reproduzidos da linha do tempo.

* **Suporte habilitado para reprodução offline** - Com a reprodução offline, os usuários agora podem baixar conteúdo de vídeo em seus dispositivos e assisti-lo quando não estiverem conectados. Para obter informações detalhadas, consulte &quot;[Reprodução offline com Android](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf).&quot;

**Versão 3.4**

* O TVSDK agora é compatível com a reprodução de fluxos CMAF para fluxos simples e criptografados CBC.

**Versão 3.3**

* **Alterações na API**

   * Uma nova API é adicionada ao `NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*` para lidar com erros de rede e tempos limite.
      * onde (n) é o número de tentativas.

**Versão 3.2**

* **Suporte ao download de Manifesto e Resolução de Anúncios Paralelos**

   * O TVSDK 3.2 é compatível com a resolução simultânea, em vez da resolução sequencial para todas as solicitações de Anúncios e Ad breaks, exceto para VMAP.

   * Todos os manifestos de anúncios em um ad break são baixados simultaneamente.

* **Ativação do suporte para Resolução de anúncio e Tempo limite de download do manifesto.**

   * Os usuários agora podem definir o valor de tempo limite para a resolução geral do anúncio e downloads de manifesto.  No caso do VMAP, o valor de tempo limite se aplica a ad breaks individuais, pois todos os ad breaks são resolvidos sequencialmente.

* **Introdução de novas APIs na classe AdvertisingMetadata:**

   * `void setAdResolutionTimeout(int adResolutionTimeout)`

   * `int getAdResolutionTimeout()`

   * `void setAdManifestTimeout(int adManifestTimeout)`

   * `int getAdManifestTimeout()`

* **Removidas as APIs abaixo da classe AdvertisingMetadata:**

   * `void setAdRequestTimeout(int adRequestTimeout)`

   * `int getAdRequestTimeout()`

* **Reprodução ativada de fluxos com o codec de áudio AC3/EAC3**

   * `void alwaysUseAC3OnSupportedDevices(boolean val)` in `MediaPlayer` classe

* **O TVSDK é compatível com CMAF e reprodução de fluxos simples para Widevine CTR criptografado.**

* **A reprodução de fluxos HEVC de 4K agora é compatível.**

* **Solicitações de chamada de anúncio paralelo** - O TVSDK agora busca previamente 20 solicitações de chamada de anúncio em paralelo.

**Versão 3.0**

* **O TVSDK 3.0 oferece suporte a fluxos HEVC (High Efficiency Video Coding).**

* **Just in Time - Resolver anúncios mais próximos a marcadores de anúncios**
A Resolução de anúncios lentos agora resolve cada ad break independentemente. Anteriormente, a resolução do anúncio era uma abordagem de duas fases: os pré-rolls eram resolvidos antes do início da reprodução e todos os slots de mid/post roll combinados após o início da reprodução. Com esse recurso aprimorado, cada ad break agora é resolvido em um momento específico antes do ponto de sinalização do anúncio.

>[!NOTE]
>
>A Resolução de anúncios lenta foi alterada para ser desativada por padrão e precisa ser ativada explicitamente.

Uma nova API é adicionada ao `AdvertisingMetadata::setDelayAdLoadingTolerance` para obter a tolerância de carregamento de anúncio atrasada associada a estes metadados de anúncio.\
A busca agora é permitida imediatamente após a PREPARAÇÃO. A busca por ad breaks resultará em resolução imediata antes da conclusão da busca.\
Modos de sinalização `SERVER_MAP` e `MANIFEST_CUES` são compatíveis.

Para obter mais informações, consulte [Guia do programador do TVSDK 3.0 para Android](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/c-lazy-ad-resolving.md) na API e alterações de evento.

* **Atualizado `targetSdkVersion` para a versão mais recente**

Atualizado `targetSdkVersion` de 19 a 27 para um funcionamento perfeito.

* **Placement.Type getPlacementType() agora é um método na interface TimelineMarker**

  Esse método retornará um tipo de posicionamento de Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL ou Placement.Type.POST_ROLL. Se um ad break não for resolvido, o método getDuration() na interface do TimelineMarker retornará 0.

**Versão 2.5.6.**

* **O TVSDK 2.5 é compatível com Android P.**

* **Habilitar áudio de fundo**

  Para habilitar a reprodução de áudio quando o aplicativo muda do primeiro para o segundo plano, o aplicativo deve chamar `enableAudioPlaybackInBackground` API do MediaPlayer com verdadeiro como argumento quando o player está no estado PREPARADO.

* **alwaysUseAudioOutputLatency(boolean val) na classe MediaPlayer**

Quando definido, use a latência de saída no cálculo do carimbo de data e hora de áudio.
Valor de parâmetros booleanos - True usará a latência de saída de áudio no cálculo do carimbo de data/hora de áudio.

* **Otimizado para obter a melhor experiência de reprodução mesmo se a velocidade da largura de banda cair repentinamente**

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

  Agora incluindo `AdSystem` e `CreativeId` como novos parâmetros nas solicitações 1401 e 1403.

* **API setEncodeUrlForTracking na classe NetworkConfiguration removida** como os caracteres inseguros em um URL devem ser codificados.

**Versão 2.5.4**

O Android TVSDK v2.5.4 oferece as seguintes atualizações e alterações de API:

* Alterações no valor padrão de `WebViewDebbuging`

  `WebViewDebbuging` o valor está definido como `Fals`e por padrão. Para ativá-lo, chame `setWebContentsDebuggingEnabled(true)` na petição.

* **Atualização da versão do OpenSSL e do Curl**

  Atualização de libcurl para v7.57.0 e OpenSSL para v1.0.2k.

* Acesso em nível de aplicativo para objeto de resposta VAST

  Introdução de uma nova API `NetworkAdInfo::getVastXml()` que fornece acesso do objeto de resposta VAST ao aplicativo.

**Versão 2.5.3**

O Android TVSDK v2.5.3 oferece as seguintes atualizações e alterações de API.

* Todos os clientes de TVSDK que usam CRS são incentivados a atualizar seus aplicativos com TVSDK 2.5.3.85 ou posterior no Android. Isso será uma substituição suspensa da implementação do aplicativo existente. Após a atualização do TVSDK, verifique as solicitações do URL criativo do CRS em uma ferramenta de proxy (por exemplo: Charles) e confirme se o nome do host e a versão no caminho refletem como na estrutura de URL de exemplo abaixo.

  `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* Personalizável Agente do usuário do TVSDK: adicionamos algumas novas APIs para personalizar os agentes do usuário.

   * `setCustomUserAgent(String value)`
   * `getCustomUserAgent()`

* Compartilhar cookies entre o aplicativo Android e o TVSDK: o Android TVSDK agora oferece suporte ao acesso de cookies entre a camada JAVA (armazenada no CookieStore do aplicativo Android) e a camada C++ TVSDK. Agora, é possível definir e/ou modificar os cookies na camada nativa do C++, pois eles serão expostos ao Java Cookie Store.

* Alterações na API:

   * Um novo evento `CookiesUpdatedEvent` é adicionado. Ele é despachado pelo reprodutor de mídia quando o cookie é atualizado.

   * Uma nova API é adicionada ao `NetworkConfiguration::set/ getCustomUserAgent()` para usar o agente de usuário personalizado.

   * Uma nova API é adicionada ao `NetworkConfiguration::set/ getEncodedUrlForTracking` para forçar a codificação de caracteres inseguros.

   * Uma nova API é adicionada ao `NetworkConfiguration::getNetworkDownVerificationUrl()` para definir um URL de verificação de rede em caso de failover.

   * Uma nova propriedade é adicionada a `TextFormat::treatSpaceAsAlphaNum` que definem se o espaço deve ser tratado como alfanumérico ao exibir legendas.

* Alterações em `SizeAvailableEvent`. Anteriormente, `getHeight()` e `getWidth()` métodos de `SizeAvailableEvent` na versão 2.5.2, costumava retornar a altura e a largura do quadro, retornadas pelo formato de mídia. Agora, retorna a altura e a largura da saída retornadas pelo decodificador, respectivamente.

* Alterações no comportamento de buffering: o comportamento de buffering é alterado. Fica a cargo do desenvolvedor do aplicativo o que ele deseja fazer no caso de buffer vazio. O 2.5.3 usa o tamanho do buffer de reprodução em uma situação de buffer vazio.

**Versão 2.5.2**

O Android TVSDK v2.5.2 oferece correções de erros importantes e algumas alterações na API.

**Versão 2.5.1**

Os novos recursos importantes lançados no Android 2.5.1.

* **Melhorias de desempenho -** A nova arquitetura TVSDK 2.5.1 traz várias melhorias de desempenho. Com base em estatísticas de um estudo de benchmarking de terceiros, a nova arquitetura fornece uma redução de 5x no tempo de inicialização e de 3,8x menos quadros ignorados em comparação com a média do setor:

* **Instantâneo para VOD e live -** Quando você ativa o recurso de ativação instantânea, o TVSDK inicializa e armazena em buffer a mídia antes do início da reprodução. Como é possível iniciar várias ocorrências de MediaPlayerItemLoader simultaneamente em segundo plano, você pode armazenar vários fluxos em buffer. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, a reprodução no novo canal é iniciada imediatamente. O TVSDK 2.5.1 também é compatível com Ativo instantâneo para **live** transmissões também. Os fluxos ativos são colocados em buffer novamente quando a janela ativa se move.

* **Lógica ABR aprimorada -** A nova lógica ABR é baseada no comprimento do buffer, na taxa de alteração do comprimento do buffer e na largura de banda medida. Isso garante que o ABR escolha a taxa de bits certa quando a largura de banda flutuar e também otimize o número de vezes que o switch de taxa de bits realmente ocorre, monitorando a taxa em que o comprimento do buffer muda.

* **Download/subsegmentação parcial do segmento -** O TVSDK reduz ainda mais o tamanho de cada fragmento para iniciar a reprodução o mais rápido possível. O fragmento ts deve ter um quadro principal a cada dois segundos.

* **Resolução de anúncio lento -** O TVSDK não espera a resolução de anúncios não precedentes antes de iniciar a reprodução, diminuindo assim o tempo de inicialização. APIs como busca e truque ainda não são permitidas até que todos os anúncios sejam resolvidos. Isso se aplica aos fluxos de VOD usados com o CSAI. Operações como busca e avanço rápido não são permitidas até que a resolução do anúncio seja concluída. Para transmissões ao vivo, esse recurso não pode ser ativado para resolução de anúncios durante um evento ao vivo.

* **Conexões de rede persistentes -** Esse recurso permite que o TVSDK crie e armazene uma lista interna de conexões de rede persistentes. Essas conexões são reutilizadas para várias solicitações, em vez de abrir uma nova conexão para cada solicitação de rede e destruí-la posteriormente. Isso aumenta a eficiência e diminui a latência no código de rede, resultando em um desempenho de reprodução mais rápido.
Quando o TVSDK abre uma conexão, ele solicita ao servidor uma *keep-alive* conexão. Alguns servidores podem não suportar esse tipo de conexão, nesse caso, o TVSDK voltará a fazer uma conexão para cada solicitação novamente. Além disso, enquanto as conexões persistentes estarão ativadas por padrão, o TVSDK agora tem uma opção de configuração para que os aplicativos possam desativar as conexões persistentes, se desejado.

* **Download paralelo -** O download de vídeo e áudio em paralelo em vez de em série reduz os atrasos de inicialização. Esse recurso permite que arquivos HLS Live e VOD sejam reproduzidos, otimiza o uso da largura de banda disponível de um servidor, reduz a probabilidade de entrar em situações de buffer em execução e minimiza o atraso entre o download e a reprodução.

* **Downloads de anúncios paralelos -** O TVSDK busca previamente os anúncios em paralelo à reprodução do conteúdo antes de atingir os ad breaks, permitindo assim a reprodução contínua de anúncios e conteúdo.

* **Reprodução**

* **Reprodução de conteúdo MP4 -** Os clipes MP4 curtos não precisam ser retranscodificados para serem reproduzidos no TVSDK.

  >[!NOTE]
  >
  >Switching ABR, truque, inserção de anúncio, vinculação de áudio tardia e subsegmentação não são suportados para reprodução MP4.

* **Truque com a taxa de bits adaptável (ABR) -** Esse recurso permite que o TVSDK alterne entre fluxos do iFrame no modo de reprodução de truque. Você pode usar perfis que não sejam do iFrame para executar truques em velocidades mais baixas.

* **Jogo de truque mais suave -** Essas melhorias melhoram a experiência do usuário:

   * Seleção da taxa de bits e da taxa de quadros adaptáveis durante a execução do truque, com base na largura de banda e no perfil de buffer

   * Use o fluxo principal em vez do fluxo IDR para obter reprodução rápida de até 30 qps.

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

   * **VHL 2.0 -** Esta é a integração otimizada mais recente da Biblioteca de heartbeats de vídeo (VHL) para a coleta automática de dados de uso do Adobe Analytics. A complexidade das APIs foi reduzida para facilitar a implementação. Baixar a biblioteca do VHL [v2.0.0 para Android](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) e extraia o arquivo JAR na pasta libs.

* **SizeAvailableEventListener**

   * `getHeight()` e `getWidth()` métodos de `SizeAvailableEvent` O agora retornará a saída em altura e largura, respectivamente. A taxa de proporção de exibição pode ser calculada da seguinte maneira:

     ```java
     SizeAvailableEvent e;
     DAR = e.getWidth()/ e.getHeight();
     ```

     A proporção de armazenamento em termos de largura de Sar e altura de Sar também pode ser usada para calcular a largura e a altura do Quadro:

     ```java
     SAR = e.getSarWidth()/e.getSarHeight();
     frameHeight = e.getHeight();
     frameWidth = e.getWidth()/SAR;
     ```

* **Cookies**

   * O Android TVSDK agora oferece suporte ao acesso a cookies JAVA armazenados no CookieStore do aplicativo Android. Uma API de retorno de chamada (onCookiesUpdated) é fornecida para registrar sempre que um novo cookie vem como parte de **Set-Cookie** Cabeçalho de resposta. Esses cookies estão disponíveis como uma Lista de cookies HTTP usados para um URI/domínio diferente definindo esses valores de cookies nesse URI/domínio específico usando o CookieStore. Da mesma forma, os valores de cookie no TVSDK são atualizados usando a API de adição do CookieStore.

## Matriz de recursos {#feature-matrix}

O TVSDK para Android oferece suporte a vários recursos que você pode implementar para adicionar funcionalidade a seus aplicativos de vídeo.

Nas tabelas de recursos abaixo, um &quot;Y&quot; indica que o recurso é compatível na versão atual.

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Reprodução geral (Reproduzir, Pausar, Buscar) | VOD + Ao vivo | Y |
| FER - Reprodução geral (Reproduzir, Pausar, Buscar) | FER VOD | Y |
| Buscar quando um anúncio estiver sendo reproduzido | VOD + Ao vivo | Não suportado |
| Reprodução HEVC | VOD + Ao vivo | Somente contêiner fMP4 |
| AC3 e EAC3 | VOD + Ao vivo | Não suportado |
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
| Reprodução com deslocamento | VOD + Ao vivo | Y |
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
| Inserção de ad break parcial | Ao vivo | Y |

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Criptografia AES | VOD + Ao vivo | Y |
| Exemplo de criptografia AES | VOD + Ao vivo | Y |
| Fluxos Tokenizados | VOD + Ao vivo | Y |
| DRM Widevine | VOD + Ao vivo | Somente contêiner fMP4 |
| DRM do Primetime | VOD + Ao vivo | Y |
| Reprodução externa (RBOP) | VOD + Ao vivo | Somente DRM do Primetime |
| Rotação de licenças | VOD + Ao vivo | Somente DRM do Primetime |
| Rotação de chaves | VOD + Ao vivo | Somente DRM do Primetime |

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Integração com o Adobe Analytics VHL | VOD + Ao vivo | Y |
| Faturamento | VOD + Ao vivo | Y |

## Problemas resolvidos {#resolved-issues}

Quando a resolução está associada a um problema relatado, uma referência do Zendesk é exibida, por exemplo, ZD#xxxxx.

**Android TVSDK 3.15**

Esta seção fornece um resumo do problema resolvido na versão do Android TVSDK 3.14.

* ZD#46903 - O aplicativo trava várias vezes quando a tag criativa está ausente ou quando [!UICONTROL url CDATA] está vazio em [!UICONTROL VAST] resposta.

**Android TVSDK 3.14**

* ZD#46903 - O aplicativo trava quando [!UICONTROL CDATA] está vazio para qualquer um dos [!UICONTROL ClickTracking], [!UICONTROL CustomClick] ou [!UICONTROL CompanionClickTracking] elemento em [!UICONTROL VAST] resposta.

### Problemas resolvidos nas versões anteriores

**Android TVSDK 3.12**

* ZD#40584 - O aplicativo Referência Primetime não compila com a versão mais recente do Gradle.

**Android TVSDK 3.11**

* ZD#41252 - Caracteres coreanos em WebVTT quebrados após o Android 7.1.

**Android TVSDK 3.10**

* ZD#40340 - O aplicativo trava com o erro &quot;O aplicativo não está respondendo&quot; ao tentar reproduzir após bloquear a listagem de todos os arquivos TS (TypeScript).

**Android TVSDK 3.8**

* Nenhum problema novo adicionado.

**Android TVSDK 3.7**

* Nenhum problema novo adicionado.

**Android TVSDK 3.6**

* Nenhum problema novo adicionado.

**Versão 3.5**

* ZD#37503 - As respostas JSON para as regras CRS são armazenadas em cache para evitar as solicitações duplicadas.

**Versão 3.4**

* ZD#37996 - Corrigido um problema sobre reprodução instável em fluxos HEVC lineares e VOD CMAF.
* ZD#37706 - Correção de um problema sobre legendas ilegíveis.
* ZD#37622 - Corrigido um problema sobre URISyntaxErrors fatais para anúncios específicos.
* ZD#36938 - Corrigido um problema sobre a taxa de bits descendo para a taxa de bits intermediária e aumentando para a taxa de bits mais alta depois de sair das reproduções.

**Versão 3.3**

* ZD#37394 - O avanço rápido do ativo CMAF causa artefatos após as alterações de velocidade.
   * Correção de um problema que ocorre com uma alteração de perfil durante a reprodução de truque.
* ZD#37396 - Os eventos de rastreamento de anúncios estão ausentes em algumas versões intermediárias e posteriores.
   * Correção de um caso específico sobre eventos de rastreamento de anúncios.
* ZD#37491 - O código de status HTTP com erro meta não está presente.
   * Trabalhado na propagação de erros de rede em posições mais altas na pilha.
* ZD#37808 - Lista de permissões novo cabeçalho personalizado.
   * Suporte a SSAI_TAG adicionado como parte dessa correção.
* ZD#37622 - Erros URISyntax de pods de anúncios específicos.
   * Correção de um problema sobre uma falha na reprodução do stream quando o aplicativo do Android do cliente recebe anúncios que contêm uma % não codificada
* ZD#37631 - Mecanismo de repetição de manifesto mestre para Android TVSDK.
   * Adição de uma nova API na configuração de rede para lidar com esse aprimoramento. Se essa API não for usada, o manifesto não será repetido. Se for usado, o manifesto será repetido para lidar com erros de rede e tempos limite.

**Versão 3.2**

* ZD#37493- Os sinais de rastreamento para reprodução ao vivo não são acionados intermitentemente para o primeiro anúncio em sequência.
* ZD#36985- Os sinais de rastreamento não são enviados para ad breaks vazios na resposta do VMAP.
* ZD#37134 - O TVSDK lança a ID errada para resposta do VMAP intermitentemente.

**Versão 3.0**

* ZD#33740 - TVSDK lança um aviso desnecessário logo após criar um objeto MediaPlayer e chamar replaceCurrentResource()

   * Correção anterior aprimorada ao chamar restaurar somente quando o player está em estado suspenso

* ZD#36442 - Cada nova reprodução desconecta a sessão de depuração remota, impossibilitando a depuração.

   * A depuração não é possível por padrão na exibição da Web, pois a depuração não está habilitada por padrão. O aplicativo deve ativar a depuração, se necessário, chamando setWebContentsDebuggingEnabled(true) no objeto retornado de MediaPlayer.getCustomAdView().

* ZD#33688 - Suporte para resolução de anúncios Just In Time

   * Os ad breaks são resolvidos em um intervalo especificado antes da posição do ad break.

* ZD#36441 - A duração da janela ativa continua aumentando além de 5 minutos, causando vários problemas.

   * Correção de um problema em que virtualStartTime estava sendo adicionado duas vezes ao calcular o ponto de ativação virtual, resultando nesse problema.

**Android TVSDK 2.5.6**

* ZD #34992 - O idioma está vazio nas Legendas ocultas.

   * Correção de um problema em que o TVSDK não analisava #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS do manifesto principal para obter os detalhes de rastreamento da legenda.

* ZD #35078 - Validação do Android P.

   * O TVSDK 2.5.6 foi validado com as compilações beta mais recentes do Android P. Nenhum problema encontrado devido ao novo sistema operacional Android.

* ZD #34149 - O player continua solicitando manifestos mesmo se um erro for encontrado.

   * Correção do problema em que o TVSDK fazia chamadas repetitivas mesmo quando todos os perfis estavam inativos (erro 404).

* ZD #31533 - Reproduzindo áudio no Android depois que o aplicativo é enviado para o plano de fundo.

   * Adicionado `enableAudioPlaybackInBackground` API do MediaPlayer que deve ser chamado com &quot;True&quot; como argumento (quando o player estiver no estado PREPARED) para ativar a reprodução de áudio quando o aplicativo estiver em segundo plano.

**Android TVSDK 2.5.5**

* ZD #21647 - O Android TVSDK notifica 640x368 quando o tamanho real do vídeo é 640x360.

   * Devido à variável m_nOutputHeight (dentro do AndroidMCVideoDecoder) sendo atualizada com a altura do quadro em vez da altura de saída real. Alterações relevantes feitas na função getVideoFrame para calcular m_nOutputHeight corretamente.

* ZD #26614 - Urgente — Veiculação de anúncios de terceiros/programática — falha ao veicular impressões.

   * Correção anterior aprimorada ao manipular o caso na análise XML, em que o problema era reproduzível quando &quot;espaço&quot; estava antes do sinal &quot;igual&quot;, como &lt;vast version=&quot;2.0&quot;>

* ZD #29296 - Android: adicionar AdSystem e ID criativa às solicitações do CRS.

   * Agora inclui &quot;AdSystem&quot; e &quot;CreativeId&quot; como novos parâmetros nas solicitações 1401 e 1403.

* ZD #33062 - O TVSDK trava na ocorrência do caractere de pipe na resposta VAST no nó CDATA

   * API setEncodeUrlForTracking na classe NetworkConfiguration removida como os caracteres não seguros em um URL a ser codificado

* ZD #33063 - A lógica de seleção de arquivo CRS foi interrompida - O TVSDK não estava enviando a solicitação CRS para o formato webm, mas sim enviando-a para arquivos 3gpp.

   * Correção da lógica agora. Ao usar arquivos de mídia com o formato webm e 3gpp, a solicitação de CRS é enviada para webm. E ao usar ambos os arquivos de mídia com formato 3gpp, a solicitação CRS é enviada para o arquivo 3gpp com a taxa de bits mais alta.

* ZD #33125 - O aplicativo Android trava com a tag DoubleClick específica no VMAP.

   * Corrigido o cenário para evitar a falha.

* ZD #32256 - Problema de rotação de licença e rotação de chaves - Acesso ao Adobe

   * Correção da inicialização de segmentos com os metadados DRM para o conteúdo SampleAES. Funciona bem com conteúdo AES128.

* ZD #33619 - Encaminhamento rápido de um conteúdo de lista de reprodução em crescimento preso no estado de buffering próximo a um ponto ativo.

   * Manipulou o caso ao cruzar o ponto ativo no modo de reprodução de truque

* ZD #34151 - Objetos TimedMetadata fora de ordem.

   * Dois eventos TimedMetadata apareciam em ordem aleatória se pertencessem ao mesmo tempo na linha do tempo. Manutenção do pedido original no manifesto.

* ZD #34189 - Problema ao tentar iniciar o ad break.

   * O problema era com anúncios SSAI que são compilados usando descontinuidade. E a causa foi um comportamento quando buscamos o começo de tais anúncios, procuramos por um quadro-chave e não o encontramos. O motivo era o carimbo de data e hora mín. do áudio do anúncio antes do carimbo de data e hora mín. do vídeo. Portanto, acabamos pesquisando um quadro principal em um fragmento de dados de Dump incorreto. Corrigido agora.

* ZD #34528 - Resolução de vídeo não atualizando além de 640x360 no FireTV 3rd gen dongle.

   * Correção aprimorada para incluir as atualizações de firmware mais recentes

* ZD #34793 - O TVSDK 2.5.x costumava falhar com o resolvedor de conteúdo personalizado em alguns casos, quando o VideoEngine assumia que as auditudeSettings estavam disponíveis e não estavam.

   * A falha ocorria devido a uma chamada de função em um ponteiro Nulo compartilhado (auditudeSettings). Adição de uma verificação condicional em VideoEngineTimeline::placeToSourceTimeline() para garantir que auditudeSettings esteja disponível antes de chamar qualquer coisa nesse objeto.

* ZD #32584 - Não é possível acessar informações completas presentes no &lt;extensions> nó de uma resposta VAST.

   * Corrigido o problema de análise XML e agora NetworkAdInfo fornece as informações completas presentes na &lt;extensions> nó

* ZD #35086 - Não obtendo dados de extensão completos do player no caso de respostas específicas do VMAP.

   * O problema era específico do xml de extensão, pois a análise XML não funcionava se o xml de extensão tivesse aspas duplas no valor do atributo. Correção do problema.

**Android TVSDK 2.5.4**

* ZenDesk#33659 - Sessão de reprodução que habilita a depuração remota do webview.

WebViewDebuging está definido como Falso por padrão. Para habilitar a depuração, defina como true por meio do aplicativo, usando setWebContentsDebuggingEnabled(true).

* ZenDesk#33011 - A linha do tempo do anúncio não é resolvida no caso de falha na solicitação de CRS.

  Quando uma solicitação do CRS para um anúncio falha, a linha do tempo é resolvida e os anúncios restantes são reproduzidos.

* ZenDesk#34528 - A resolução de vídeo não atualiza além de 640x360 no dongle de terceira geração FireTV.

  Os switches de resolução de vídeo são ativados como switches de taxa de bits.

* ZenDesk#33192 - AudioTrack tem nome nulo quando a faixa é recuperada via AudioUpdatedEventListener::onAudioUpdated.

  Em alguns cenários no FireTV Stick, o evento onAudioUpdate estava sendo acionado quando não havia nenhuma atualização de áudio real. Isso foi corrigido agora.

**Android TVSDK 2.5.3**

* Zendesk#32216 - A assinatura de tag personalizada TimedMetadata não está funcionando.

  Retornamos dados ID3 como uma matriz de bytes (para oferecer suporte a APIC ou dados genéricos) ao cliente, enquanto na sequência de retorno 1.4. A matriz de bytes não lida com o próprio caractere terminado por nulo, portanto, mostrava o caractere especial ao cliente. Esse problema foi corrigido agora.
* Zendesk#32670 - Player não falha na lista de reprodução redundante

  Isso está funcionando bem agora e setNetworkDownVerificationUrl está funcionando como esperado.
* Zendesk#32369 - A legenda oculta mostra lixo de cores ou artefato diferentes.

  Problema com falhas CC foi corrigido na última build
* Zendesk#25590 - Aprimoramento: armazenamento de cookies TVSDK ( C++ para JAVA )

  O Android TVSDK agora é compatível com o acesso de cookies entre a camada JAVA (armazenada no CookieStore do aplicativo Android) e a camada C++ TVSDK.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 não parece ter a correção para PTPLAY-20269

  Esse problema foi corrigido e integrado à ramificação 2.5.2.
* Zendesk#31806 - Auditude sticks na PREPARAÇÃO

  O player ficou preso no estado Preparação porque o xml de resposta tinha uma tag vazia. Agora o problema foi corrigido.
* Zendesk#31727 - Os caracteres de legendas ocultas do TVSDK 2.5 são soltos ou digitados incorretamente.

  Problema corrigido e não estamos soltando/digitando nenhum caractere incorretamente.
* Zendesk#31485 - DrmManager in 2.5

  Ocorreu um problema ao Criar o DrmManager por meio do novo DrmManager(Context context). Implementação da classe DRMService que forneceria o DRMSanager.
* Zendesk#32794- Fluxo de resolução de 1080P não está sendo reproduzido no Android

  alteramos os métodos SizeAvailableEvent e Previously, getHeight() e getWidth() de SizeAvailableEvent no 2.5 usados para retornar a altura e a largura do quadro, retornados pelo formato de mídia. Ele agora retorna a altura e a largura da saída respectivamente retornadas pelo decodificador.
* O Flash Player do Zendesk #19359 falha devido à posição do atributo #EXT-X-FAXS-CM no manifesto de nível de conjunto.

  A tag #EXT-X-FAXS-CM deve sempre aparecer na lista de reprodução principal antes que a taxa de bits ou os segmentos individuais apareçam na lista de reprodução.

**Android TVSDK 2.5.2**

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

**Android TVSDK 2.5.1**

* Falha específica do dispositivo (Samsung Galaxy Tab 4); LBA DRM VOD com Auditude e clique em anúncios.
* VHL - Chamadas de heartbeat incorretas são enviadas ao iniciar o conteúdo a partir de um deslocamento.
* Quando os anúncios VPAID são reproduzidos, o heartbeat do VHL chama para o evento:type:não estão presentes anúncios.
* Depois de entrar no status COMPLETO, o reprodutor volta para o status REPRODUZINDO com IGNORAR adBreakPolicy para anúncios posteriores.
* Os cookies não estão sendo anexados a retornos de chamada de anúncios de saída.
* Os pontos de sinalização de anúncios não estão visíveis.
* O HLS com o rastreamento SAP EAC3 separado não será carregado.
* O player trava quando o TVSDK recebe uma intenção Tela ativada após a restauração do reprodutor de mídia.

## Problemas conhecidos e limitações {#known-issues-and-limitations}

**Android TVSDK 3.11**

* Nenhuma limitação nova adicionada.

### Problemas conhecidos e limitações nas versões anteriores

**Android TVSDK 3.10**

* Nenhuma limitação nova adicionada.

**Android TVSDK 3.8**

* Nenhuma limitação nova adicionada.

**Android TVSDK 3.7**

* Nenhuma limitação nova adicionada.

**Android TVSDK 3.6**

* Nenhuma limitação nova adicionada.

**Android TVSDK 3.5**

* Nenhuma limitação nova adicionada.

**Android TVSDK 3.4**

* O suporte a ID3, Legendas ocultas e Áudio de ligação tardia não foi verificado para o fluxo de CMAF (CBC).
* Em alguns dispositivos, existe um problema de baixa reprodutibilidade, devido ao qual a distorção de vídeo pode aparecer na parte superior durante a reprodução de truques em fluxos CMAF.

**Android TVSDK 3.3**

* As legendas clcp:c608 não são compatíveis com a reprodução de fluxo do CMAF.

**Android TVSDK 3.2**

* O TVSDK 3.2 não é compatível com a reprodução de fluxos AES e AES128 de amostra do CMAF.
* Os fluxos HEVC CMAF não incluem suporte para reprodução de legendas ocultas.
* A coloração verde é exibida para fluxos criptografados WV quando a busca é realizada ao redor do segmento não criptografado.
* Fluxos CMAF não suportam eventos ID3.
* Fluxos HLS não oferecem suporte ao formato de legendas HTML.

**Android TVSDK 3.0**

* O suporte a HEVC tem as seguintes limitações nesta versão

   * DRM sem suporte
   * Suporte a CC (CEA 608/708) não verificado
   * Suporte a 4K ainda não presente
   * Suporte a tags ID3 não verificado

* Para eventos de progresso de anúncios, a barra de linha do tempo pode não refletir o tempo 100% preciso de reprodução do anúncio. Como solução alternativa, é possível usar `adcompleteevent` para saber a conclusão da reprodução do anúncio e atualizar a interface do usuário para vários propósitos, como atualizar a barra de linha do tempo, remover a interface do usuário relacionada ao anúncio etc.
* Chamadas de anúncios volumosos retornadas do VMAP não respeitam a posição de lookahead Just-In-Time.

**Android TVSDK 2.5.6**

* Não há suporte para várias interrupções de anúncios VMAP ao mesmo tempo.

**Android TVSDK 2.5.3**

Essa versão tem os seguintes problemas:

* A reprodução de vídeo ao vivo pode ter problemas de sincronização de áudio-vídeo em dispositivos low-end ou condições de rede ruins.
* Para fluxos FER, virtualTime e localTime podem diferir. Além disso, o FER com offset não funciona.
* A reprodução pode ficar paralisada quando o conteúdo do Áudio de vinculação tardia é buscado.
* Intermitentemente, as legendas webVTT podem ficar fora de sincronia para o conteúdo LIVE.
* Intermitentemente, a reprodução rápida de alguns quadros pode ser vista depois de sair de um ad break.
* Às vezes, o erro 303 é lançado para Ad Breaks de wrapper triplos, mesmo que Anúncios sejam reproduzidos.

**Android TVSDK 2.5.2**

Essa versão tem os seguintes problemas:

* A reprodução de vídeo ao vivo pode ter problemas de sincronização de áudio e vídeo em dispositivos low-end.
* A reprodução pode parar quando se tenta encerrar a mídia de VOD.
* Para fluxos FER, virtualTime e localTime podem diferir. Além disso, o FER com offset não funciona.

**Android TVSDK 2.5.1**

Essa versão do TVSDK apresenta os seguintes problemas:

* A reprodução de vídeo ao vivo pode ter problemas de sincronização de áudio e vídeo em dispositivos low-end.
* Para fluxos FER, virtualTime e localTime podem diferir. Além disso, o FER com offset não funciona.
* No XML do VMAP, se houver uma tag VAST vazia sem uma tag de fechamento explícita (&lt;/vast>) e sem uma nova linha depois dele, o XML do VMAP não é analisado corretamente e os anúncios podem não ser reproduzidos.
* Não há suporte para pós-implantação de VPAID.

## Recursos úteis {#helpful-resources}

* [Requisitos do sistema](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/android-3x-requirements.md)
* [Guia do programador do TVSDK 3.10 para Android](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/overview-prod-audience-guide/android-3x-overview-prod-audience-guide.md)
* [Referência de TVSDK Android Javadoc para API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [Documento da API TVSDK Android C++](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html) - Cada classe Java tem uma classe C++ correspondente, e a documentação C++ contém mais material explicativo do que os Javadocs, portanto, consulte a documentação C++ para obter uma compreensão mais profunda da API Java.
* [Guia de migração do TVSDK 1.4 para 2.5 para Android (Java)](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* Para lidar com cenários de ativação/desativação de tela, consulte `Application_Changes_for_Screen_On_Off.pdf` arquivo incluído na build.
* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
