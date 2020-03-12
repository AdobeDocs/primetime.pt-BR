---
title: Notas de versão do TVSDK 2.4.1 para Android
seo-title: Notas de versão do TVSDK 2.4.1 para Android
description: As Notas de versão do TVSDK 2.4.1 para Android descrevem os recursos novos e compatíveis e os problemas conhecidos e as limitações no TVSDK Android 2.4.1.
seo-description: As Notas de versão do TVSDK 2.4.1 para Android descrevem os recursos novos e compatíveis e os problemas conhecidos e as limitações no TVSDK Android 2.4.1.
uuid: 929fc577-e851-4e03-9201-13280cc6137a
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: a6dbcc4a-9e14-4452-9004-b39ed13fad6f
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Notas de versão do TVSDK 2.4.1 para Android {#tvsdk-for-android-release-notes}

As Notas de versão do TVSDK 2.4.1 para Android descrevem os recursos novos e compatíveis e os problemas conhecidos e as limitações no TVSDK Android 2.4.1.

## TVSDK Android 2.4.1 {#tvsdk-android}

A Adobe está lançando o TVSDK 2.4.1 para Android.

Para usar esta versão do TVSDK, verifique se o sistema atende aos requisitos descritos em Requisitos [do sistema](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

Aqui é onde você encontra a documentação:

・ Sistema de ajuda online TVSDK 2.4 para Ajuda do Android

・ [Javadocs TVSDK 2.4 para API Java Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Os Javadocs são a autoridade final, pois são gerados automaticamente diretamente do código-fonte TVSDK.

・ Documentação da API [C++ TVSDK 2.4 para API C++ Android](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

Cada classe Java tem uma classe C++ correspondente e a documentação C++ contém mais material explicativo do que o Javadocs, portanto consulte a documentação C++ para obter uma compreensão mais profunda da API Java.

・ Guia de migração ([TVSDK 2.4 para o Guia](../migration-guides/tvsdk-14-25-android.md)de migração do Android)

Este guia explica o que você precisa modificar para migrar um aplicativo com base no TVSDK 1.4 para um com base no TVSDK 2.4.

## Novos recursos {#new-features}

O TVSDK 2.4.1 para Android fornece várias melhorias de desempenho em relação às versões anteriores. Ele oferece uma experiência de visualização de alta qualidade.

Esta versão inclui todos os recursos das versões 2.4 e 2.4.1, e nenhum recurso está obsoleto.

Estes são os principais novos recursos da versão 2.4.1:

* Recursos da versão 4 do HLS

   * **Reprodução** de vídeo (reprodução, pausa, busca) com controle de player para fluxos ao vivo, lineares e VOD.
   * **Legendagem fechada.** O TVSDK pode exibir legendas 608/708 fechadas com uma seleção de fontes, tamanhos de fonte, cores e plano de fundo. Ele também pode suportar vídeos com legendas de roll-up e alternar entre as faixas de idioma, se estiverem disponíveis.
   * **O modo** Trick play suporta avanço rápido e retrocesso para fluxos HLS que usam I-Frames. Todos os controles de reprodução de vídeo funcionam no conteúdo. O movimento lento (para frente) está disponível para o modo de reprodução de vídeo externo com taxas entre 0 e 1.
   * **A ABR (Adaptive Bitrate)** permite que o player selecione dinamicamente qual das várias versões do mesmo fluxo de conteúdo será reproduzido, com base na rede e em outras condições. Você pode definir parâmetros dinamicamente ou no arquivo manifest para selecionar entre políticas de seleção agressivas, moderadas e conservadoras.
   * **Os intervalos** de bytes permitem que um único arquivo TS contenha vários segmentos TS.
   * **As execuções** de áudio alternativas permitem que o player alterne entre as faixas de áudio disponíveis.
   * **Suporte para ID3.** O TVSDK pode reproduzir fluxos de áudio e vídeo HLS que contêm metadados de áudio ID3, como nome do artista, título e álbum.
   * **Failover. **O TVSDK usa estratégias para continuar a reprodução ininterrupta, apesar de falhas de servidores host, arquivos de lista de reprodução e segmentos.
   * **Passagem de áudio multicanal (DD+).** O TVSDK pode passar dados de áudio Dolby Digital Plus (E-AC3) para o hardware de suporte.

* Recursos de proteção de conteúdo

   * **DRM para HLS.** Todas as APIs de reprodução de vídeo funcionam com conteúdo de vídeo criptografado protegido pelo Adobe Access. Os seguintes recursos de DRM são suportados:

      * Rotação da licença
      * Rotação da chave
      * Cache de licenças
      * Hora da política
      * Rotação IV

* **AES 128 Playback.** O TVSDK pode reproduzir conteúdo HLS padrão de criptografia avançada (AES) com tamanho de chave de 128 bits.
* **O PHLS (Protected HLS)** fornece um conjunto limitado de políticas de DRM pré-criadas, um subconjunto do que o Adobe Access fornece, para habilitar o DRM leve sobre HLS para fluxos ao vivo e VOD.

* Conteúdo de anúncio/alternativo e recursos de monetização

   * **Rastreamento para anúncios inseridos no servidor.** O TVSDK pode rastrear publicidades inseridas pelo serviço de inserção de publicidade da Adobe Cloud. Ele suporta anúncios lineares nos formatos VAST2, VAST3 e VMAP para fluxos VOD e live/linear.
   * **Tags HLS personalizadas.** O TVSDK usa sua `MediaPlayerConfig` classe para ativar a notificação do aplicativo do player quando tags HLS personalizadas aparecem no fluxo.
   * **Inserção de anúncio do lado do cliente.** A biblioteca de inserção de anúncio do Auditude funciona com os servidores Adobe Auditude para resolver anúncios para inserção dinamicamente em conteúdo ativo, linear e VOD, em posições precedente, intermediário ou posterior.
   * **Resolvedores de anúncios personalizados.** As interfaces `ContentResolver, OpportunityGenerator,` e `MediaPlayerClientFactory` permitem implementar um resolvedor de conteúdo alternativo/anúncio personalizado e registrar um detector de oportunidade personalizado para trabalhar com o TVSDK. As classes `TestAdResolver` e `AuditudeResolver` fornecem exemplos C++ da implementação de um resolvedor de conteúdo. Você pode encontrar um exemplo de Javascript em `samples/jspsdk/testapp/psdk.js`.
   * **Comportamento consistente do anúncio.** Use a `AdPolicySelector` interface para permitir um comportamento consistente em todos os players para operações como busca e reprodução de truques quando os anúncios estiverem presentes no conteúdo. Se você não implementar o seu próprio, o TVSDK usará `DefaultAdPolicySelector`.
   * **Remova/substitua anúncios C3.** Use a API TVSDK apropriada para remover intervalos de conteúdo personalizados e inserir dinamicamente novos anúncios sem trabalho de preparação adicional. Isso é útil quando o conteúdo ao vivo/linear é transmitido e imediatamente disponibilizado sob demanda sem limpeza.

Estes são os principais novos recursos da versão 2.4:

* **Instantâneo para VOD e live** Quando você ativa instantaneamente, o TVSDK inicializa e armazena a mídia antes do início da reprodução. Como você pode iniciar várias `MediaPlayerItemLoader` instâncias simultaneamente em segundo plano, é possível fazer o buffer de vários fluxos. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, a reprodução no novo canal é iniciada imediatamente. O TVSDK 2.4 também é compatível com o Instant On para fluxos ao vivo. Os fluxos ao vivo são armazenados novamente quando a janela ao vivo se move.

* **Melhorias de desempenho **A nova arquitetura TVSDK 2.4 traz várias melhorias de desempenho:

   * **Sub-segmentação** - o TVSDK reduz ainda mais o tamanho de cada fragmento para iniciar a reprodução o mais rápido possível.
   * **Downloads** de anúncios paralelos - O TVSDK pré-busca os anúncios em paralelo à reprodução do conteúdo antes de bater nos intervalos do anúncio, permitindo uma reprodução contínua de anúncios e conteúdo.
   * **Resolução** de anúncios ociosa - com esse recurso, não esperamos pela resolução de anúncios não pré-implantados antes de iniciar a reprodução, diminuindo assim o tempo de inicialização. As APIs como busca e reprodução de truques ainda não são permitidas até que todos os anúncios sejam resolvidos.

* **Reprodução de conteúdo MP4**

Esta versão do TVSDK suporta a reprodução de MP4 como conteúdo principal.

* **Conexões de rede persistentes**

O TVSDK mantém um conjunto de conexões de rede reutilizáveis, de modo que não incorre na sobrecarga de criação e destruição de uma conexão de rede para cada solicitação de rede.

* **Proteção de saída baseada em resolução**

Este recurso vincula as restrições de reprodução a resoluções específicas, fornecendo controles de DRM mais finos.

* **Reprodução de truques com taxa de bits adaptável (ABR)**

Esse recurso permite que o TVSDK alterne entre fluxos de iFrame no modo de reprodução de truques. Você pode usar perfis que não sejam iFrame para executar truques em velocidades menores.

* **Brincadeira mais suave**

Essas melhorias aprimoram a experiência do usuário:

・ Seleção adaptável da taxa de bits e da taxa de quadros durante a reprodução do truque, com base na largura de banda e no perfil do buffer

・ Use o fluxo principal em vez do fluxo IDR para obter uma reprodução rápida de até 30 fps.

* **Lógica de ABR aprimorada**

A nova lógica ABR baseia-se no comprimento do buffer, na taxa de alteração do comprimento do buffer e na largura de banda medida. Isso garante que o ABR escolha a taxa de bits correta quando a largura de banda flutuar e também otimiza o número de vezes que a alternância de taxa de bits realmente acontece monitorando a taxa na qual o comprimento do buffer muda.

* **Cobrança**

O TVSDK coleta automaticamente métricas, respeitando o contrato de vendas do cliente para gerar relatórios de uso periódicos necessários para fins de faturamento. Em cada evento de início de fluxo, o TVSDK usa a API de inserção de dados do Adobe Analytics para enviar métricas de faturamento, como tipo de conteúdo, sinalizadores ativados para inserção de anúncio e sinalizadores habilitados para drm - com base na duração do fluxo faturável - para o conjunto de relatórios pertencente ao Adobe Analytics Primetime. Isso não interfere nem é incluído nos conjuntos de relatórios ou nas chamadas do servidor do Adobe Analytics. Mediante solicitação, este relatório de uso de faturamento é enviado periodicamente aos clientes. Esta é a primeira fase do recurso de faturamento que suporta somente faturamento de uso. Ele pode ser configurado com base no contrato de vendas usando as APIs descritas na documentação.

## Recursos suportados {#supported-features}

O TVSDK para Android 2.4 é compatível com vários recursos que podem ser implementados para adicionar funcionalidade aos aplicativos de vídeo.

>[!NOTE]
>
>Nas tabelas de matriz de recursos abaixo, um √ significa que o recurso é suportado na versão atual.

### Principais recursos de reprodução {#core-playback-features}

| **Recurso** | **Tipo de conteúdo** | **HLS** | **TRAÇO** |
|---|---|---|---|
| Reprodução geral (Reproduzir, Pausar, Buscar) | VOD + Live | √ | √ (apenas VOD) |
| FER - Reprodução geral (Reproduzir, Pausar, Procurar) | FER VOD | √ | Não suportado |
| MP3 | VOD | Não suportado | Não suportado |
| Reprodução de conteúdo MP4 | VOD | √ | √ |
| Lógica de troca da taxa de bits adaptável | VOD + Live | √ | Não suportado |
| Reprodução somente áudio | VOD + Live | √ | Não suportado |
| Legendas ocultas - 608/708 | VOD + Live | √ | √ (apenas VOD) |
| Legendas ocultas - WebVTT | VOD + Live | √ | √ (apenas VOD) |
| Failover Manifest | VOD + Live | √ | √ (apenas VOD) |
| Failover avançado | VOD + Live | √ | √ (apenas VOD) |
| Notificações de QoS e player | VOD + Live | √ | √ (apenas VOD) |
| Suporte para cabeçalhos de cookies | VOD + Live | √ | √ (apenas VOD) |
| Suporte para cabeçalhos personalizados | VOD + Live | Não suportado | Não suportado |
| Definir parâmetros de controle de buffer | VOD + Live | √ | √ (apenas VOD) |
| Definir controles adaptáveis de taxa de bits | VOD + Live | √ | √ (apenas VOD) |
| Tags de manifesto personalizado (HLS) / Fluxos de evento (DASH) | VOD + Live | √ | √ (apenas VOD) |
| Áudio com limite atrasado | VOD + Live | √ | √ (apenas VOD) |
| Redirecionamento 302 | VOD + Live | √ | √ (apenas VOD) |

### Recursos avançados de reprodução {#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>Recurso</strong></td> 
   <td><strong>Tipo de conteúdo</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>TRAÇO</strong></td> 
  </tr>
  <tr>
   <td>Reprodução com deslocamento</td> 
   <td>Live</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Reprodução somente áudio</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Trick Play </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Reprodução suave de truques (com ABR)</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Análise de ID3 (HLS) / Metadados cronometrados (DASH)</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Blackouts </td> 
   <td>VOD + Live</td> 
   <td>Não suportado</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Instantâneo ativado</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Suporte a marcadores de descontinuidade (HLS) </li> 
     <li>Vários períodos (DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>302 Autoaderência de redirecionamento</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√ (apenas VOD)</td> 
  </tr>
  <tr>
   <td>Depuração em miniatura (Iframe e JPEG)</td> 
   <td>VOD + Live</td> 
   <td>Não suportado</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Integridade do fluxo </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
 </tbody>
</table>

### Principais recursos de inserção de anúncios (CSAI) {#core-ad-insertion-features-csai}

| **Recurso** | **Tipo de conteúdo** | **HLS** | **TRAÇO** |
|---|---|---|---|
| Reprodução geral, anúncios ativados | VOD + Live | √ | √ (apenas VOD Pre-rolls) |
| FERE conteúdo com anúncios ativados | VOD | √ | Não suportado |
| Comportamentos de anúncio padrão | VOD + Live | √ | √ (apenas VOD Pre-rolls) |
| VAST 2.0/3.0 | VOD + Live | √ | √ (apenas VOD Pre-rolls) |
| VMAP 1.0 | VOD + Live | √ | √ (apenas VOD Pre-rolls) |
| Anúncios MP4 | VOD + Live | √ (do SIR) | √ (do SIR, apenas para os pré-rolos) |

### Recursos avançados de inserção de anúncios (CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>Recurso</strong></td> 
   <td><strong>Tipo de conteúdo</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>TRAÇO</strong></td> 
  </tr>
  <tr>
   <td>Reprodução de truques com anúncios ativada</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Somente publicidade </td> 
   <td>VOD</td> 
   <td>Não suportado</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Parâmetros de definição de metas</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√ (apenas VOD Pre-rolls)</td> 
  </tr>
  <tr>
   <td>Parâmetros personalizados</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√ (apenas VOD Pre-rolls)</td> 
  </tr>
  <tr>
   <td>Comportamentos de anúncio personalizados</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√ (apenas VOD Pre-rolls)</td> 
  </tr>
  <tr>
   <td>Tags de anúncio personalizadas</td> 
   <td>Live</td> 
   <td>√ </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Resolvedores de anúncios personalizados</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Resolvedor de anúncios personalizado do FreeWheel</td> 
   <td>VOD</td> 
   <td>Não suportado</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Substituição de anúncio C3 </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Carregamento de anúncio ocioso</td> 
   <td>VOD</td> 
   <td>√ </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Suporte a marcadores de descontinuidade - SSAI (HLS) </li> 
     <li>Vários períodos (DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>Anúncios complementares, anúncios em banner e anúncios clicáveis</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>√ (apenas VOD Pre-rolls)</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + Live</td> 
   <td>√ (JS) </td> 
   <td>√ (apenas VOD Pre-rolls)</td> 
  </tr>
  <tr>
   <td>Saída antecipada do anúncio</td> 
   <td>Live</td> 
   <td>√ </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Creative VOD com base em regras + Priorização ao vivo</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Regras CRS </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Não suportado</td> 
  </tr>
 </tbody>
</table>

## Recursos de proteção de conteúdo {#content-protection-features}

| **Recurso** | **Tipo de conteúdo** | **HLS** | **TRAÇO** |
|---|---|---|---|
| Criptografia AES | VOD + Live | √ | √ (apenas VOD) |
| Criptografia AES de amostra | VOD + Live | √ |  |
| Fluxos Tokenized | VOD + Live | √ |  |
| DRM | VOD + Live | Somente DRM Primetime (Futuro: Widevine) | Somente Widevine |
| Reprodução externa (RBOP) | VOD + Live | Somente DRM Primetime | Não suportado |
| Rotação de licença | VOD + Live | Somente DRM Primetime | Não suportado |
| Rotação da tecla | VOD + Live | Somente DRM Primetime | Não suportado |

### Recursos de integração {#integration-features}

| **Recurso** | **Tipo de conteúdo** | **HLS** | **TRAÇO** |
|---|---|---|---|
| Integração VHL do Adobe Analytics | VOD + Live | √ | √ |
| Cobrança | VOD + Live | √ | Não suportado |

## Recursos não suportados {#features-not-supported}

Esta versão do TVSDK não é compatível:

* Blecaute de anúncios.
* Movimento lento na peça.
* Busca e jogada com conteúdo MP4.
* Inserção de anúncio com conteúdo principal MP4.
* Procure quando um anúncio está sendo reproduzido.
* Reprodução de anúncios com mídia somente de áudio.

## Problemas conhecidos e limitações {#known-issues-and-limitations}

Esta versão do TVSDK apresenta os seguintes problemas:

* LBA VOD DRM com auditude e clique nos anúncios específicos do dispositivo (Samsung Galaxy Tab 4) falha
* O anúncio posterior não é reproduzido para um conteúdo específico.
* A definição da legenda close para idiomas CJK não funciona.
* O vídeo pode sair do modo de truque automaticamente entre VOD e live.
* VHL - chamadas de pulsação incorretas são enviadas quando iniciamos um conteúdo de um deslocamento.
* Quando os anúncios VPAID são reproduzidos, as chamadas de pulsação VHL para event:type:play ad estão ausentes.
* O anúncio precedente é reproduzido mesmo quando o adBreakPolicy SKIP é escolhido.
* Depois de entrar no modo Completo, o player voltará ao estado Reproduzindo com SKIP adBreakPolicy para anúncios posteriores.

Sem vídeo, não há dimensão viewport e, sem uma dimensão viewport, não é possível exibir gráficos para legendas.

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página Aprendizagem e suporte [do](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.