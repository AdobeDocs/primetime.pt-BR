---
title: Notas de versão do TVSDK 3.12 para Android
seo-title: Notas de versão do TVSDK 3.12 para Android
description: As Notas de versão do TVSDK 3.12 para Android descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK Android 3.12
seo-description: As Notas de versão do TVSDK 3.12 para Android descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK Android 3.12
uuid: 685d46f5-5a02-4741-af5c-91e91babd6f7
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: 3a27379f-3cef-4ea3-bcae-21382dc1e9fd
translation-type: tm+mt
source-git-commit: 33509042e32c2167fab21788042bfb2bb877c0f4
workflow-type: tm+mt
source-wordcount: '5418'
ht-degree: 0%

---


# Notas de versão do TVSDK 3.12 para Android {#tvsdk-for-android-release-notes}

As Notas de versão do TVSDK 3.12 para Android descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK Android 3.12.

O player de referência do Android está incluído no Android TVSDK no diretório samples/ de sua distribuição. O arquivo README.md que o acompanha explica como criar o player de referência.

>[!NOTE]
>
>Para criar com êxito o player de referência, conforme descrito em README.md distribuído com a versão, certifique-se de fazer o seguinte:
>
>1. Baixe VideoHeartbeat.jar de [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) (biblioteca VideoHeartbeat para Android v2.0.0)
>1. Extraia VideoHeartbeat.jar para a pasta libs/.


O TVSDK para Android fornece várias melhorias de desempenho em relação às versões anteriores. Ele fornece uma experiência de visualização de alta qualidade e contém todos os recursos da versão 1.4, com exceção do suporte a vários CDN.

O conjunto abrangente de recursos suportados e não suportados é apresentado na seção [Features Matrix](#feature-matrix) das notas de versão.

## Android TVSDK 3.12

A versão gradle do aplicativo Primetime Reference agora é atualizada para a versão 5.6.4.

Para configurar e executar o aplicativo de referência usando o Android Studio, siga as instruções do arquivo ReadMe disponível com o zip TVSDK em `TVSDK_Android_x.x.x.x/samples/PrimetimeReference/src/README.md`.

Os principais problemas do cliente corrigidos na versão atual são mencionados na seção [problemas resolvidos](#resolved-issues).

### Novos recursos e melhorias nas versões anteriores

**Android TVSDK 3.11**

* **A busca de caixas PSSH (Protection System Specific Header) é permitida**  - o TVSDK permite a busca da Caixa de Cabeçalho Específico do Sistema de Proteção associada ao Recurso de Mídia carregado atual. Nova API `getPSSH()` adicionada a `com.adobe.mediacore.drm.DRMManager`.

Para obter mais informações, consulte [DRM do Widevine](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md).

**Android TVSDK 3.10**

O lançamento focou na correção de problemas principais do cliente, conforme mencionado na seção [problemas resolvidos](#resolved-issues).

**Android TVSDK 3.9**

* **Delivery seguro em HTTPS**  - o Android TVSDK 3.9 introduziu os recursos de delivery seguro por meio do HTTPS para fornecer conteúdo com segurança, com escala e desempenho inigualáveis.

   Para ativar o delivery seguro em HTTPS, a nova API foi introduzida na classe `NetworkConfiguration`.

   `public void setForceHTTPS (boolean value)`

   `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **Suporte pré-rolo com recurso**  Paral Ad-Break - Com esse aprimoramento, o TVSDK 3.8 suporta anúncios precedentes com o recurso Parcial Ad-Break (PABI).

O anúncio precedente, se disponível, é reproduzido e o conteúdo é reproduzido a partir do ponto ativo, emulando a experiência da televisão ao vivo.

**Android TVSDK 3.7**

* Para conteúdo de teste do Widevine, uma nova API `setMediaDrmCallback` na classe DRMManager é exposta para substituir a implementação padrão da interface MediaDrmCallback.

   `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* Corrigido o erro de AppCrash por não manipular `MediaPlayerEvent.ITEM_UPDATED` na camada C++ (Android 64 bits).

**Android TVSDK 3.6**

* **Aprimore seus aplicativos para o requisito**  de 64 bits - A biblioteca nativa  `(libAVEAndroid.so)` é atualizada e disponibilizada em duas versões. A localização da biblioteca nativa armeabi (32 bits) existente foi alterada de `/framework/Player to /framework/Player/armeabi` e uma biblioteca armada64-v8a (64 bits) adicional foi introduzida em `/framework/Player/arm64-v8a.`

**Versão 3.5**

* **Exatamente na resolução**  do anúncio no tempo - o TVSDK 3.5 remove o suporte dos anúncios reproduzidos da linha do tempo.

* **Suporte ativado para reprodução**  offline - Com a reprodução offline, os usuários agora podem baixar o conteúdo do vídeo em seus dispositivos e assistí-lo quando não estiverem conectados. Para obter informações detalhadas, consulte &quot;[Reprodução offline com Android](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf)&quot;.

**Versão 3.4**

* O TVSDK agora oferece suporte à reprodução de fluxos CMAF para fluxos criptografados e simples por CBC.

**Versão 3.3**

* **Alterações da API**

   * Uma nova API é adicionada a `NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*` para lidar com erros e tempos limite de rede.
      * em que n é o número de tentativas.

**Versão 3.2**

* **Resolução de anúncios paralelos e suporte para download do Manifest**

   * O TVSDK 3.2 suporta a resolução simultânea, em vez da resolução sequencial para todas as solicitações de anúncio e pausas de anúncio, exceto para VMAP.

   * Todos os manifestos de anúncio em uma pausa de anúncio são baixados simultaneamente.

* **Habilitado o suporte para Resolução de anúncio e Tempo limite de download do manifesto.**

   * Agora, os usuários podem definir o valor do tempo limite para a resolução geral do anúncio e para downloads de manifesto.  No caso de VMAP, o valor de tempo limite se aplica a quebras de anúncios individuais, já que todas as quebras de anúncios são resolvidas sequencialmente.

* **Novas APIs introduzidas na classe AdvertisingMetadata:**

   * `void setAdResolutionTimeout(int adResolutionTimeout)`

   * `int getAdResolutionTimeout()`

   * `void setAdManifestTimeout(int adManifestTimeout)`

   * `int getAdManifestTimeout()`

* **Removidas abaixo das APIs da classe AdvertisingMetadata:**

   * `void setAdRequestTimeout(int adRequestTimeout)`

   * `int getAdRequestTimeout()`

* **Reprodução de fluxos com codec de áudio AC3/EAC3 ativada**

   * `void alwaysUseAC3OnSupportedDevices(boolean val)` na  `MediaPlayer` classe

* **O TVSDK oferece suporte à reprodução de CMAF e streams simples para CTR de Widevine criptografado.**

* **A reprodução de fluxos HEVC 4K agora é suportada.**

* **Solicitações**  de chamada de anúncio paralela - O TVSDK agora busca 20 solicitações de chamada de anúncio em paralelo.

**Versão 3.0**

* **O TVSDK 3.0 suporta fluxos de codificação de vídeo de alta eficiência (HEVC).**

* **Exatamente no tempo - Resolver os anúncios mais perto dos**
marcadores de anúnciosA resolução lenta de anúncios agora resolve cada quebra de anúncio independentemente. Anteriormente, a resolução do anúncio era uma abordagem em duas fases: os pré-rolls foram resolvidos antes do start de reprodução e todos os slots de mid/post roll combinados após o início da reprodução. Com esse recurso aprimorado, cada quebra de anúncio é resolvida em um momento específico antes do ponto de sinalização do anúncio.

>[!NOTE]
>
>A Resolução de anúncios ociosos agora foi alterada para ser desativada por padrão, e explicitamente precisa ser ativada.

Uma nova API é adicionada a `AdvertisingMetadata::setDelayAdLoadingTolerance` para obter a tolerância de carregamento de anúncio atrasado associada a esses Metadados de anúncio.\
A busca agora é permitida imediatamente após a PREPARAÇÃO, procurar quebras de anúncios resultará na resolução imediata antes da conclusão da busca.\
Os modos de sinalização `SERVER_MAP` e `MANIFEST_CUES` são suportados.

Para obter mais informações, consulte [TVSDK 3.0 para o Guia do Programador Android](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/c-lazy-ad-resolving.md) sobre alterações de API e evento.

* **Atualizado  `targetSdkVersion` para a versão mais recente**

Atualizado `targetSdkVersion` de 19 para 27 para o funcionamento regular.

* **Placement.Type getPlacementType() agora é um método na interface TimelineMarker**

   Este método retornará um tipo de disposição de Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL ou Placement.Type.POST_ROLL. Se uma quebra de anúncio não for resolvida, o método getDuration() na interface TimelineMarker retornará 0.

**Versão 2.5.6.**

* **O TVSDK 2.5 é compatível com Android P.**

* **Habilitar áudio em segundo plano**

   Para ativar a reprodução de áudio quando o aplicativo se move de primeiro para segundo plano, o aplicativo deve chamar `enableAudioPlaybackInBackground` a API do MediaPlayer com verdadeiro como argumento quando o player está no estado PREPARADO.

* **alwaysUseAudioOutputLatency(boolean val) na classe MediaPlayer**

Quando definido, use a latência de saída no cálculo do carimbo de data e hora de áudio.
Parâmetros booleanos val - Verdadeiro usará a latência de saída de áudio no cálculo do carimbo de data e hora de áudio.

* **Otimizado para obter a melhor experiência de reprodução mesmo se a velocidade da largura de banda cair de repente**

O TVSDK agora cancela o download do segmento em andamento, se necessário, e alterna dinamicamente para a execução apropriada. Isso é feito alternando perfeitamente entre as taxas de bits sem interrupções.

**Versão 2.5.5**

* **Inserção parcial de quebra de anúncio**

   Experiência semelhante à da TV de participar do meio de um anúncio sem acionar o rastreamento do anúncio parcialmente assistido.\
   Exemplo: O usuário ingressa no meio (em 40 segundos) de um intervalo de anúncios de 90 segundos que consiste em três anúncios de 30 segundos. Dez segundos depois do segundo anúncio no intervalo.

   * O segundo anúncio é reproduzido pela duração restante (20 segundos) seguido pelo terceiro anúncio.

   * Os rastreadores de anúncios para o anúncio parcial reproduzido (segundo anúncio) não são acionados. Os rastreadores apenas do terceiro anúncio são disparados.

* **Carregamento seguro de anúncios em HTTPS**

   A Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios primetime e CRS em https.

* **AdSystem e Creative Id adicionados às solicitações CRS**

   Agora, incluindo `AdSystem` e `CreativeId` como novos parâmetros nas solicitações 1401 e 1403.

* **API setEncodeUrlForTracking na classe NetworkConfiguration** removeu os caracteres não seguros em um URL devem ser codificados.

**Versão 2.5.4**

O Android TVSDK v2.5.4 oferta as seguintes atualizações e alterações de API:

* Alterações no valor padrão de `WebViewDebbuging`

   `WebViewDebbuging` é definido como  `Fals`e por padrão. Para ativá-lo, chame `setWebContentsDebuggingEnabled(true)` no aplicativo.

* **Atualização de versão do OpenSSL e do Curl**

   Atualização do libcurl para v7.57.0 e OpenSSL para v1.0.2k.

* Acesso no nível do aplicativo para objeto de resposta VAST

   Introduziu uma nova API `NetworkAdInfo::getVastXml()` que fornece acesso do objeto de resposta VAST ao aplicativo.

**Versão 2.5.3**

O Android TVSDK v2.5.3 oferta as seguintes atualizações e alterações de API.

* Todos os clientes TVSDK que usam CRS são incentivados a atualizar seus aplicativos com TVSDK 2.5.3.85 ou mais recente no Android. Isso será uma substituição instantânea da implementação do aplicativo existente. Após a atualização do TVSDK, verifique se há solicitações de URL criativo do CRS em uma ferramenta proxy (por exemplo: Charles) e confirme se o nome do host e a versão no caminho refletem como na estrutura de URL de amostra abaixo.

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* Agente de usuário do TVSDK personalizável: adicionamos novas APIs para personalizar os agentes do usuário.

   * `setCustomUserAgent(String value)`
   * `getCustomUserAgent()`

* Compartilhe cookies entre o aplicativo Android e o TVSDK: O Android TVSDK agora oferece suporte ao acesso de cookies entre a camada JAVA (armazenada no CookieStore do aplicativo Android) e a camada C++ TVSDK. Agora, é possível definir e/ou modificar os cookies na camada C++ nativa, pois eles serão expostos à Loja de Cookies Java.

* Alterações de API:

   * Um novo Evento `CookiesUpdatedEvent` é adicionado. Ele é despachado pelo player de mídia quando seu cookie é atualizado.

   * Uma nova API é adicionada a `NetworkConfiguration::set/ getCustomUserAgent()` para usar o agente de usuário personalizado.

   * Uma nova API é adicionada a `NetworkConfiguration::set/ getEncodedUrlForTracking` para forçar a Codificação de caracteres não seguros.

   * Uma nova API é adicionada a `NetworkConfiguration::getNetworkDownVerificationUrl()` para definir um URL de verificação de rede em caso de failover.

   * Uma nova propriedade é adicionada a `TextFormat::treatSpaceAsAlphaNum`, que define se o espaço deve ser tratado como alfanumérico ao exibir legendas.

* Alterações em `SizeAvailableEvent`. Anteriormente, os métodos `getHeight()` e `getWidth()` de `SizeAvailableEvent` no 2.5.2 eram usados para retornar a altura e a largura do quadro, que eram retornados pelo formato de mídia. Agora retorna a altura de saída e a largura de saída respectivamente retornadas pelo decodificador.

* Alterações no comportamento do Buffering: O comportamento de buffer é alterado. É deixada para o desenvolvedor do aplicativo no que ele quer fazer no caso de buffer vazio. 2.5.3 usa o tamanho do buffer de reprodução em uma situação vazia do buffer.

**Versão 2.5.2**

O Android TVSDK v2.5.2 oferta correções importantes de erros e algumas alterações na API.

**Versão 2.5.1**

Os novos recursos importantes lançados no Android 2.5.1.

* **Melhorias no desempenho -** A nova arquitetura TVSDK 2.5.1 traz várias melhorias no desempenho. Com base em estatísticas de um estudo de benchmarking de terceiros, a nova arquitetura oferece uma redução de 5 vezes no tempo de inicialização e de 3,8 vezes menos quadros em queda em relação à média do setor:

* **Instant on for VOD and live -** Quando você ativa instantaneamente, o TVSDK inicializa e armazena a mídia antes dos start de reprodução. Como você pode iniciar várias instâncias MediaPlayerItemLoader simultaneamente em segundo plano, é possível armazenar vários fluxos em buffer. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, a reprodução é feita imediatamente nos novos start do canal. O TVSDK 2.5.1 também é compatível com os fluxos Instant On para **live** também. Os fluxos ao vivo são armazenados novamente quando a janela ao vivo se move.

* **Lógica ABR aprimorada -** A nova lógica ABR é baseada no comprimento do buffer, na taxa de alteração do comprimento do buffer e na largura de banda medida. Isso garante que o ABR escolha a taxa de bits correta quando a largura de banda flutuar e também otimiza o número de vezes que a alternância de taxa de bits realmente acontece monitorando a taxa na qual o comprimento do buffer muda.

* **Download/sub-segmentação de segmento parcial - o** TVSDK reduz ainda mais o tamanho de cada fragmento, a fim de reproduzir o start o mais rápido possível. O fragmento ts deve ter um quadro-chave a cada dois segundos.

* **Resolução de anúncios ociosa -** O TVSDK não espera pela resolução de anúncios não pré-implantados antes de iniciar a reprodução, diminuindo assim o tempo de inicialização. As APIs como busca e reprodução de truques ainda não são permitidas até que todos os anúncios sejam resolvidos. Isso se aplica aos fluxos VOD usados com CSAI. Operações como busca e avanço rápido não são permitidas até que a resolução do anúncio seja concluída. Para fluxos ao vivo, esse recurso não pode ser habilitado para a resolução de anúncios durante um evento ao vivo.

* **Conexões de rede persistentes -** Esse recurso permite que o TVSDK crie e armazene uma lista interna de conexões de rede persistentes. Essas conexões são reutilizadas para várias solicitações, em vez de abrir uma nova conexão para cada solicitação de rede e depois destruí-la. Isso aumenta a eficiência e diminui a latência no código de rede, resultando em desempenho de reprodução mais rápido.
Quando o TVSDK abre uma conexão, ele solicita ao servidor uma conexão *keep-alive*. Alguns servidores podem não suportar esse tipo de conexão, caso em que o TVSDK voltará a fazer uma conexão para cada solicitação novamente. Além disso, embora as conexões persistentes estejam ativadas por padrão, o TVSDK agora tem uma opção de configuração para que os aplicativos possam desativar as conexões persistentes, se desejado.

* **Download paralelo -** Baixar vídeo e áudio em paralelo em vez de em série reduz os atrasos na inicialização. Esse recurso permite que arquivos HLS Live e VOD sejam reproduzidos, otimiza o uso da largura de banda disponível em um servidor, reduz a probabilidade de entrar em situações de buffer sem execução e minimiza o atraso entre o download e a reprodução.

* **Downloads de anúncios paralelos - o** TVSDK pré-busca os anúncios em paralelo à reprodução do conteúdo antes de bater nos intervalos do anúncio, permitindo uma reprodução contínua de anúncios e conteúdo.

* **Reprodução**

* **Reprodução de conteúdo MP4 - Os clipes curtos de** MP4 não precisam ser transcodificados novamente para reproduzir no TVSDK.

   >[!NOTE]
   >
   >A comutação ABR, a reprodução de truques, a inserção de anúncios, o vínculo de áudio tardio e a subsegmentação não são compatíveis com a reprodução MP4.

* **Reprodução com taxa de bits adaptável (ABR) -** Esse recurso permite que o TVSDK alterne entre fluxos de iFrame no modo de reprodução de truques. Você pode usar perfis que não sejam iFrame para reproduzir truques em velocidades menores.

* **Reprodução de truques mais suave -** Essas melhorias aprimoram a experiência do usuário:

   * Seleção adaptável da taxa de bits e da taxa de quadros durante a reprodução do truque, com base na largura de banda e no perfil do buffer

   * Use o fluxo principal em vez do fluxo IDR para obter uma reprodução rápida de até 30 fps.

* **Proteção de conteúdo**

   * **Proteção de saída com base em resolução -** Esse recurso vincula restrições de reprodução a resoluções específicas, fornecendo controles de DRM com granulado mais fino.

* **Suporte ao fluxo de trabalho**

   * **Integração de faturamento direto -** isso envia métricas de faturamento para o backend da Adobe Analytics, certificado pela Adobe Primetime para fluxos usados pelo cliente.

   O TVSDK coleta automaticamente métricas, respeitando o contrato de vendas do cliente para gerar relatórios de uso periódicos necessários para fins de faturamento. Em cada evento de start de fluxo, o TVSDK usa a API de inserção de dados da Adobe Analytics para enviar métricas de faturamento, como tipo de conteúdo, sinalizadores habilitados para inserção de anúncio e sinalizadores habilitados para drm - com base na duração do fluxo faturável - para o conjunto de relatórios pertencente ao Adobe Analytics Primetime. Isso não interfere nem é incluído nos próprios conjuntos de relatórios ou chamadas de servidor do Adobe Analytics do cliente. Mediante solicitação, este relatório de uso de faturamento é enviado periodicamente aos clientes. Esta é a primeira fase do recurso de faturamento que suporta somente faturamento de uso. Ele pode ser configurado com base no contrato de vendas usando as APIs descritas na documentação. Esse recurso é ativado por padrão. Para desativar esse recurso, consulte a amostra do player de referência.

   * **Suporte aprimorado a failover - estratégias** adicionais implementadas para continuar a reprodução ininterrupta, apesar de falhas de servidores host, arquivos de lista de reprodução e segmentos.


* **Publicidade**

   * **Integração de moat -** suporte para a avaliação da capacidade de visualização de anúncios do Moat.

   * **Banners complementares - os banners** complementares são exibidos ao lado de um anúncio linear e, muitas vezes, continuam a ser exibidos na visualização após o término do anúncio. Esses banners podem ser do tipo html (um trecho HTML) ou do tipo iframe (um URL para uma página iframe).

* **Analytics**

   * **VHL 2.0 -** Esta é a mais recente integração otimizada da Biblioteca de pulsações de vídeo (VHL) para coleta automática de dados de uso para Adobe Analytics. A complexidade das APIs foi diminuída para facilitar a implementação. Baixe a biblioteca VHL [v2.0.0 para Android](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) e extraia o arquivo JAR na pasta libs.

* **SizeDisponableEventListener**

   * `getHeight()` e  `getWidth()` os métodos de  `SizeAvailableEvent` retornarão a saída, respectivamente, em altura e largura. A taxa de aspecto de exibição pode ser calculada da seguinte forma:

      ```java
      SizeAvailableEvent e;
      DAR = e.getWidth()/ e.getHeight();
      ```

      A proporção da imagem do armazenamento em termos de largura da barra e altura da barra pode também ser usada para calcular a largura e a altura da imagem da imagem:

      ```java
      SAR = e.getSarWidth()/e.getSarHeight();
      frameHeight = e.getHeight();
      frameWidth = e.getWidth()/SAR;
      ```

* **Cookies**

   * O Android TVSDK agora oferece suporte ao acesso a cookies JAVA armazenados no CookieStore do aplicativo Android. Uma API de retorno de chamada (onCookiesUpdates) é fornecida para gravar sempre que um novo cookie é fornecido como parte do cabeçalho de resposta **Set-Cookie**. Esses cookies estão disponíveis como uma Lista de HttpCookie(s) usados para um URI/domínio diferente ao configurar esses valores de cookie nesse URI/domínio específico usando CookieStore. Da mesma forma, os valores de cookie no TVSDK são atualizados usando a API de adição do CookieStore.

## Matriz de recursos {#feature-matrix}

O TVSDK para Android oferece suporte a vários recursos que podem ser implementados para adicionar funcionalidade aos seus aplicativos de vídeo.

Nas tabelas de recursos abaixo, um &quot;Y&quot; indica que o recurso é suportado na versão atual.

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Reprodução geral (Reproduzir, Pausar, Buscar) | VOD + Live | Y |
| FER - Reprodução geral (Reproduzir, Pausar, Procurar) | FER VOD | Y |
| Procurar quando um anúncio está sendo reproduzido | VOD + Live | Não suportado |
| Reprodução HEVC | VOD + Live | Somente container fMP4 |
| AC3 e EAC3 | VOD + Live | Não suportado |
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
| Suporte para cabeçalhos HTTP personalizados | VOD + Live | Y (permitir listagem obrigatória) |
| Definir parâmetros de controle de buffer | VOD + Live | Y |
| Definir controles adaptáveis de taxa de bits | VOD + Live | Y |
| Tags de manifesto personalizadas | VOD + Live | Y |
| Vínculo de áudio tardio | VOD + Live | Y |
| Redirecionamento 302 | VOD + Live | Y |
| Reprodução com deslocamento | VOD + Live | Y |
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
| Inserção parcial de quebra de anúncio | Live | Y |

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Criptografia AES | VOD + Live | Y |
| Criptografia AES de amostra | VOD + Live | Y |
| Fluxos Tokenized | VOD + Live | Y |
| DRM widevine | VOD + Live | Somente container fMP4 |
| DRM Primetime | VOD + Live | Y |
| Reprodução externa (RBOP) | VOD + Live | Somente DRM Primetime |
| Rotação de licença | VOD + Live | Somente DRM Primetime |
| Rotação da tecla | VOD + Live | Somente DRM Primetime |

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Integração Adobe Analytics VHL | VOD + Live | Y |
| Cobrança | VOD + Live | Y |

## Problemas resolvidos {#resolved-issues}

Quando a resolução estiver associada a um problema reportado, uma referência do Zendesk será exibida, por exemplo, ZD#xxxx.

**Android TVSDK 3.12**

Esta seção fornece um resumo do problema resolvido na versão TVSDK 3.12 do Android.

* ZD#40584 - O aplicativo Primetime Reference não é criado com a versão mais recente do gradle.

### Resolvidos problemas nas versões anteriores

**Android TVSDK 3.11**

* ZD#41252 - Caracteres coreanos no WebVTT quebrados após o Android 7.1.

**Android TVSDK 3.10**

* ZD#40340 - O aplicativo trava com o erro &quot;App Not Responding&quot; (Aplicativo não respondendo) ao tentar reproduzir após bloquear a listagem de todos os arquivos TS (TypeScript).

**Android TVSDK 3.8**

* Não foram adicionados novos problemas.

**Android TVSDK 3.7**

* Não foram adicionados novos problemas.

**Android TVSDK 3.6**

* Não foram adicionados novos problemas.

**Versão 3.5**

* ZD#37503 - As respostas JSON para as regras do CRS são armazenadas em cache para evitar solicitações de duplicado.

**Versão 3.4**

* ZD#37996 - Corrigido um problema sobre reprodução instável para fluxos lineares e VOD CMAF HEVC.
* ZD#37706 - Corrigido um problema sobre legendas distorcidas.
* ZD#37622 - Corrigido um problema sobre URISyntaxErrors fatais para anúncios específicos.
* ZD#36938 - Corrigido um problema sobre a alternância da taxa de bits para baixo na taxa de bits média e, em seguida, a maior taxa de bits após sair de reproduções de truques.

**Versão 3.3**

* ZD#37394 - O recurso CMAF avança rapidamente provoca artefatos após as mudanças de velocidade.
   * Correção de um problema que ocorria com uma alteração de perfil durante a reprodução do truque.
* ZD#37396 - eventos de rastreamento de anúncios estão ausentes em alguns mid-rolls e post-rolls.
   * Corrigido um caso específico em torno de eventos de rastreamento de anúncios.
* ZD#37491 - O código de status HTTP com meta de erro não está presente.
   * Funcionava na propagação de erros de rede mais alto na pilha.
* ZD#37808 - Lista de permissões do novo cabeçalho personalizado.
   * Suporte SSAI_TAG adicionado como parte dessa correção.
* ZD#37622 - URISerros de sintaxe de pods de anúncios específicos.
   * Correção de um problema sobre travamento da reprodução de fluxo quando o aplicativo Android do cliente recebe anúncios que contêm uma % não codificada
* ZD#37631 - Principal mecanismo de repetição do manifesto para Android TVSDK.
   * Adicionada uma nova API na configuração de rede para lidar com essa melhoria. Se essa API não for usada, o manifesto não será repetido. Se for usado, o manifesto será repetido para lidar com erros e tempos limite de rede.

**Versão 3.2**

* ZD#37493- O rastreamento de beacons para reprodução ao vivo não é acionado intermitentemente para o primeiro anúncio em sequência.
* ZD#36985- O rastreamento de beacons não é enviado para quebras de anúncios vazias na resposta VMAP.
* ZD#37134 - O TVSDK emite a ID incorreta para resposta VMAP intermitente.

**Versão 3.0**

* ZD#33740 - O TVSDK emite um aviso desnecessário logo após a criação de um objeto MediaPlayer e a chamada replaceCurrentResource()

   * A correção anterior foi aprimorada chamando a restauração somente quando o player está em estado suspenso

* ZD#36442 - Cada nova reprodução desconecta a sessão de depuração remota tornando impossível a depuração.

   * A depuração não é possível por padrão na visualização da Web, pois a depuração não está ativada por padrão. O aplicativo deve ativar a depuração, se necessário, chamando setWebContentsDebuggingEnabled(true) no objeto retornado de MediaPlayer.getCustomAdView().

* ZD#33688 - Suporte para just In time e solução

   * As quebras de anúncio são resolvidas em um intervalo especificado antes da posição da pausa do anúncio.

* ZD#36441 - A duração da janela ativa continua aumentando além de 5 minutos, causando vários problemas.

   * Correção de um problema em que virtualStartTime era adicionado duas vezes ao calcular o ponto ativo virtual que resultava nesse problema.

**Android TVSDK 2.5.6**

* ZD #34992 - O idioma está vazio em Legenda Fechada.

   * Correção de um caso em que o TVSDK não estava analisando #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS do manifesto principal para obter os detalhes do rastreamento da legenda.

* ZD #35078 - Validação P do Android.

   * O TVSDK 2.5.6 foi validado com as versões beta mais recentes do Android P. Nenhum problema encontrado devido ao novo sistema operacional Android.

* ZD #34149 - O player continua a solicitar manifestos mesmo se um erro for encontrado.

   * Corrigido o caso em que o TVSDK fazia chamadas repetitivas mesmo quando todos os perfis estavam inativos (erro 404).

* ZD #31533 - Reproduzir áudio no Android depois que o aplicativo é enviado para o plano de fundo.

   * Adição da API `enableAudioPlaybackInBackground` do MediaPlayer que deve ser chamada com &#39;True&#39; como argumento (quando o player está no estado PREPARADO) para habilitar a reprodução de áudio quando o aplicativo está em segundo plano.

**Android TVSDK 2.5.5**

* ZD #21647 - Android TVSDK notifica 640x368 quando o tamanho real do vídeo é 640x360.

   * Devido à variável m_nOutputHeight (dentro de AndroidMCVideoDecoder) ser atualizada com a altura do quadro em vez da altura de saída real. Alterações relevantes na função getVideoFrame foram feitas para calcular m_nOutputHeight corretamente.

* ZD #26614 - Urgente - serviço de anúncios de terceiros / programático - falha ao servir impressões.

   * Aprimoramento da correção anterior, manipulando o caso na análise XML, em que o problema era reproduzível quando &quot;space&quot; era anterior ao sinal &quot;Equal&quot;, como &lt;VAST version =&quot;2.0&quot;>

* ZD #29296 - Android: Adicione AdSystem e Creative ID às solicitações CRS.

   * Agora, incluindo &quot;AdSystem&quot; e &quot;CreativeId&quot; como novos parâmetros nas solicitações 1401 e 1403.

* ZD #33062 - O TVSDK falha na ocorrência do caractere pipe na resposta VAST em nó CDATA

   * API setEncodeUrlForTracking na classe NetworkConfiguration removido como os caracteres não seguros em um URL a ser codificado

* ZD #33063 - A lógica de seleção de arquivo CRS foi quebrada - O TVSDK não estava enviando solicitação CRS para o formato Web, mas enviando-o para arquivos 3gpp.

   * A lógica foi corrigida agora. Ao usar arquivos de mídia com o formato webm e 3gpp, o CRS solicita que sejam enviados para o webm. E ao usar ambos os arquivos de mídia com o formato 3gpp, o CRS solicita que seja enviado para o arquivo 3gpp com taxa de bits mais alta.

* ZD #33125 - O aplicativo Android trava com uma tag DoubleClick específica no VMAP.

   * Corrigido o cenário para evitar a falha.

* ZD #32256 - Problema de Rotação de Licença e Rotação de Chave - Acesso ao Adobe

   * Correção da inicialização de segmentos com metadados DRM para conteúdo do SampleAES. Funciona bem com conteúdo AES128.

* ZD #33619 - Encaminhamento rápido de um conteúdo crescente da lista de reprodução preso no estado de buffering próximo ao ponto ativo.

   * Manipulado o gabinete ao atravessar o ponto ativo no modo de peça

* ZD #34151 - Objetos TimedMetadata fora de ordem.

   * Dois eventos TimedMetadata apareciam em ordem aleatória se pertenciam ao mesmo tempo na linha do tempo. Manteve sua ordem original em manifesto.

* ZD #34189 - Problema ao tentar iniciar a pausa do anúncio.

   * O problema era com os anúncios SSAI que são costurados usando a descontinuidade. E a causa era um comportamento quando procuramos o início de tais anúncios, procuramos por um quadro-chave e não o encontramos. O motivo era que o carimbo de data e hora do áudio principal do anúncio era anterior ao carimbo de data e hora do vídeo principal. Portanto, acabamos procurando um quadro principal em um fragmentDump de dados incorreto. Corrigido agora.

* ZD #34528 - Resolução de vídeo que não atualiza além de 640x360 no dongle 3rd gen FireTV.

   * Aprimoramento da correção para incluir as atualizações de firmware mais recentes

* ZD #34793 - TVSDK 2.5.x usado para travar com o resolvedor de conteúdo personalizado em alguns casos quando o VideoEngine presumia que as auditudeSettings estavam disponíveis e não estavam.

   * A falha ocorria devido a uma chamada de função em um ponteiro compartilhado Nulo (auditudeSettings). Adicionada uma verificação condicional em VideoEngineTimeline::placeToSourceTimeline() para garantir que auditudeSettings esteja disponível antes de chamar qualquer item nesse objeto.

* ZD #32584 - Não é possível acessar informações completas presentes no nó &lt;Extensões> de uma resposta VAST.

   * Correção do problema na análise de XML e agora NetworkAdInfo fornece as informações completas presentes no nó &lt;Extensions>

* ZD #35086 - Não obtendo dados de extensão completos do player no caso de respostas VMAP específicas.

   * O problema era específico do xml de extensão, pois a análise XML não funcionava se o xml de extensão tivesse aspas de duplo dentro do valor do atributo. Correção do problema.

**Android TVSDK 2.5.4**

* ZenDesk#33659 - Sessão de reprodução que permite a depuração remota da visualização da Web.

WebViewDebbuging está definido como Falso por padrão. Para habilitar a depuração, defina como true pelo aplicativo, usando setWebContentsDebuggingEnabled(true).

* ZenDesk#33011 - A linha do tempo do anúncio não é resolvida no caso de uma solicitação CRS com falha.

   Quando uma solicitação de CRS para um anúncio falha, a linha do tempo é resolvida e os anúncios restantes são reproduzidos.

* ZenDesk#34528 - A resolução de vídeo não atualiza além de 640x360 no dongle de terceira geração do FireTV.

   A resolução do vídeo é alternada como interruptores de taxa de bits.

* ZenDesk#33192 - AudioTrack tem um nome nulo quando a faixa é recuperada via AudioUpdatesEventListener::onAudioUpdates.

   Em alguns cenários no FireTV Stick, o evento onAudioUpdate estava sendo acionado quando não havia atualização de áudio. Isto está consertado agora.

**Android TVSDK 2.5.3**

* Zendesk#32216 - A subscrição de tag personalizada TimedMetadata não está funcionando.

   Estamos retornando dados ID3 como uma matriz de bytes (para suportar dados APIC ou genéricos) para o cliente, enquanto a sequência de caracteres 1.4 retorna. A matriz de bytes não lida com o caractere finalizado nulo, portanto, estava mostrando um caractere especial para o cliente. Esse problema foi corrigido agora.
* Zendesk#32670 - Player Not Fail Over to Redundant Playlist (O reprodutor não está passando para uma lista de reprodução redundante)

   Isso está funcionando bem agora e setNetworkDownVerificationUrl está funcionando como esperado.
* Zendesk#32369 - A legenda fechada mostra lixo ou artefato de cores diferentes.

   Problema com falhas de CC foi corrigido na versão mais recente
* Zendesk#25590 - Aprimoramento: Armazenamento de cookies TVSDK ( C++ para JAVA )

   O Android TVSDK agora oferece suporte ao acesso de cookies entre a camada JAVA (armazenada no CookieStore do aplicativo Android) e a camada C++ TVSDK.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 parece não ter a correção para PTPLAY-20269

   Esse problema foi corrigido e integrado à ramificação 2.5.2.
* Zendesk#31806 - Auditude cola na PREPARAÇÃO

   O player ficou preso no estado de preparação porque o xml de resposta tinha uma tag vazia. Agora o problema foi corrigido.
* Zendesk#31727 - Os caracteres de legenda codificada TVSDK 2.5 são descartados ou com erro ortográfico.

   O problema foi corrigido e não estamos soltando/soltando nenhum caractere.
* Zendesk#31485 - DrmManager em 2.5

   Ocorreu um problema em Criar DrmManager por meio do novo DrmManager (contexto de contexto). Implementada a classe DRMService que fornecia o DRMManager.
* Fluxo de resolução Zendesk#32794-1080P não reproduzido no Android

   alteramos os métodos SizeAvailableEvent e Previous, getHeight() e getWidth() de SizeAvailableEvent em 2.5, usados para retornar a altura e a largura do quadro, que foram retornados pelo formato de mídia. Agora retorna a altura de saída e a largura de saída respectivamente retornadas pelo decodificador.
* O Flash Player do Zendesk #19359 trava devido à posição do atributo #EXT-X-FAXS-CM no manifesto de nível definido.

   A tag #EXT-X-FAXS-CM deve sempre aparecer na lista de reprodução superior antes que a taxa de bits individual ou os segmentos apareçam na lista de reprodução.

**Android TVSDK 2.5.2**

* Zendesk#17305 Artefatos em legendas fechadas com fundo não opaco.

   a propriedade setTreatSpaceAsAlphaNum em TextFormat é exposta. Por padrão, a propriedade é False. Defina a propriedade como True em um cliente para resolver o problema de espaço escuro.

* A tela do Zendesk#25097 CC tem artefatos visuais com configurações de CC.

   a propriedade setTreatSpaceAsAlphaNum em TextFormat é exposta. Por padrão, a propriedade é False. Defina a propriedade como True em um cliente para resolver o problema de espaço escuro.

* A sequência de caracteres do agente do usuário do Zendesk #31620 que sai do player do TVSDK está truncada.

   A string do agente do usuário não será mais truncada após 128 caracteres.

   A string da versão do Adobe Primetime é adicionada ao agente do usuário do sistema.

* O evento SEEK_END ausente do Zendesk #30809 impede que o aplicativo transfira para um estado de reprodução.
* A cor &#39;ciano&#39; da legenda fechada #30415 agora é uma matiz mais escura de azul (turquesa), em comparação com as versões anteriores do Primetime TVSDK.

   A cor muda de DarkCyan para Cyan.

* Os anúncios VOD do Zendesk #30727 não estão sendo baixados/resolvidos.

   No XML VMAP, se houver uma tag VAST vazia sem uma tag de fechamento explícita (‘&lt;/VAST>&#39;) e sem um caractere de nova linha depois dela, o XML VMAP não será analisado corretamente e os anúncios podem não ser reproduzidos.

**Android TVSDK 2.5.1**

* Falha específica do dispositivo (Samsung Galaxy Tab 4); VOD DRM LBA com Auditude e clique nos anúncios.
* VHL - Chamadas de pulsação incorretas são enviadas ao iniciar o conteúdo de um deslocamento.
* Quando os anúncios VPAID são reproduzidos, as chamadas de pulsação VHL para evento:type:play estão ausentes.
* Depois de entrar no status COMPLETE, o player volta ao status PLAYING com SKIP adBreakPolicy para anúncios posteriores.
* Os cookies não estão sendo anexados aos retornos de anúncio de saída.
* Os pontos de sinalização dos anúncios não estão visíveis.
* O HLS com uma faixa SAP EAC3 separada não será carregado.
* O player trava quando o TVSDK recebe uma tela On intent após o Media Player ser restaurado.

## Problemas conhecidos e limitações {#known-issues-and-limitations}

**Android TVSDK 3.11**

* Nenhuma nova limitação foi adicionada.

### Problemas conhecidos e limitações nas versões anteriores

**Android TVSDK 3.10**

* Nenhuma nova limitação foi adicionada.

**Android TVSDK 3.8**

* Nenhuma nova limitação foi adicionada.

**Android TVSDK 3.7**

* Nenhuma nova limitação foi adicionada.

**Android TVSDK 3.6**

* Nenhuma nova limitação foi adicionada.

**Android TVSDK 3.5**

* Nenhuma nova limitação foi adicionada.

**Android TVSDK 3.4**

* ID3, Legendas ocultas, suporte a Áudio de ligação tardia não foi verificado para o fluxo CMAF (CBC).
* Em alguns dispositivos, existe um problema de baixa reprodutibilidade, devido à qual a distorção de vídeo pode aparecer no topo durante a reprodução de truques em fluxos CMAF.

**Android TVSDK 3.3**

* legendas clcp:c608 não são compatíveis com reprodução de fluxo CMAF.

**Android TVSDK 3.2**

* O TVSDK 3.2 não oferece suporte à reprodução de fluxos AES de amostra e AES128 do CMAF.
* Os fluxos HEVC CMAF não incluem suporte para reprodução de legendas fechadas.
* A coloração verde é exibida para fluxos Criptografados de WV quando a busca é executada em torno do segmento não criptografado.
* Os fluxos CMAF não suportam eventos ID3.
* Os fluxos HLS não suportam o formato de legendas TTML.

**Android TVSDK 3.0**

* O suporte HEVC tem as seguintes limitações nesta versão

   * DRM não suportado
   * Suporte CC (CEA 608/708) não verificado
   * Suporte a 4K ainda não está presente
   * Suporte a tags ID3 não verificado

* Para eventos de andamento do anúncio, a barra da linha do tempo pode não refletir o tempo de reprodução do anúncio 100% preciso. Como solução, é possível usar `adcompleteevent` para saber a conclusão da reprodução do anúncio e atualizar a interface do usuário para vários fins, como atualizar a barra da linha do tempo, remover a interface do usuário relacionada ao anúncio etc.
* Vastas chamadas de anúncio retornadas pelo VMAP não cumprem a posição de pesquisa just-in-time futura.

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

* [Requisitos do sistema](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-android-prog/introduction/android-3x-requirements.html)
* [TVSDK 3.10 para o Guia do programador do Android](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-android-prog/introduction/android-3x-overview-prod-audience-guide.html)
* [TVSDK Android Javadoc para referência de API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [Documento](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html)  da API TVSDK Android C++ - Cada classe Java tem uma classe C++ correspondente e a documentação C++ contém mais material explicativo do que os Javadocs, portanto, consulte a documentação C++ para obter uma compreensão mais profunda da API Java.
* [Guia de migração do TVSDK 1.4 a 2.5 para Android (Java)](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* Para lidar com cenários de ativação/desativação da tela, consulte o arquivo `Application_Changes_for_Screen_On_Off.pdf` incluído na compilação.
* Consulte a documentação de ajuda completa na página [Aprendizagem e suporte da Adobe Primetime](https://helpx.adobe.com/support/primetime.html).
