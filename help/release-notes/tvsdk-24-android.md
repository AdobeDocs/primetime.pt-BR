---
title: Notas de versão do TVSDK 2.4.1 para Android
description: As Notas de versão do TVSDK 2.4.1 para Android descrevem os novos recursos compatíveis e os problemas e limitações conhecidos no TVSDK Android 2.4.1.
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 0%

---

# Notas de versão do TVSDK 2.4.1 para Android {#tvsdk-for-android-release-notes}

As Notas de versão do TVSDK 2.4.1 para Android descrevem os novos recursos compatíveis e os problemas e limitações conhecidos no TVSDK Android 2.4.1.

## TVSDK Android 2.4.1 {#tvsdk-android}

O Adobe está lançando o TVSDK 2.4.1 para Android.

Para usar esta versão do TVSDK, verifique se o seu sistema atende aos requisitos descritos em [Requisitos do sistema](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

Aqui está a documentação:

· Sistema de ajuda online TVSDK 2.4 para Ajuda do Android

· [Javadocs TVSDK 2.4 para API Java do Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Os Javadocs são a autoridade máxima, pois são gerados automaticamente diretamente do código-fonte do TVSDK.

· [Documentação da API C++ TVSDK 2.4 para API C++ do Android](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

Cada classe Java tem uma classe C++ correspondente, e a documentação C++ contém mais material explicativo do que os Javadocs, portanto, consulte a documentação C++ para obter uma compreensão mais profunda da API Java.

· Guia de migração ([Guia de migração do TVSDK 2.4 para Android](../migration-guides/tvsdk-14-25-android.md))

Este guia explica o que você precisa modificar para migrar um aplicativo baseado no TVSDK 1.4 para um baseado no TVSDK 2.4.

## Novos recursos {#new-features}

O TVSDK 2.4.1 para Android fornece muitas melhorias de desempenho em relação às versões anteriores. Ele oferece uma experiência de exibição de alta qualidade.

Esta versão inclui todos os recursos das versões 2.4 e 2.4.1 e nenhum recurso foi descontinuado.

Estes são os principais novos recursos na versão 2.4.1:

* Recursos da HLS versão 4

   * **Reprodução de vídeo** (reproduzir, pausar, buscar) com controle do player para fluxos ao vivo, lineares e de VOD.
   * **Legendas ocultas.** O TVSDK pode exibir legendas ocultas 608/708 com uma seleção de fontes, tamanhos de fonte, cores e plano de fundo. Ele também pode aceitar vídeos com legendas roll-up e alternar entre faixas de idioma, se disponíveis.
   * **Modo de truque** O suporta avanço e retrocesso rápidos para fluxos HLS que usam I-Frames. Todos os controles de reprodução de vídeo funcionam no conteúdo. A opção Movimento lento (avançar) está disponível para o modo de reprodução de vídeo externo com taxas entre 0 e 1.
   * **Taxa de bits adaptável (ABR)** permite que o reprodutor selecione dinamicamente qual das várias versões do mesmo fluxo de conteúdo deve ser reproduzido, com base na rede e em outras condições. É possível definir parâmetros dinamicamente ou no arquivo de manifesto para selecionar entre políticas de seleção agressivas, moderadas e conservadoras.
   * **Intervalos de bytes** permitir que um único arquivo TS contenha vários segmentos TS.
   * **Representações de áudio alternativas** habilite o reprodutor para alternar entre as faixas de áudio disponíveis.
   * **Suporte a ID3.** O TVSDK pode reproduzir fluxos de áudio e vídeo HLS que contêm metadados de áudio ID3, como nome do artista, título e álbum.
   * **Failover. **O TVSDK usa estratégias para continuar a reprodução ininterrupta, apesar das falhas de servidores host, arquivos de lista de reprodução e segmentos.
   * **Passagem de áudio multicanal (DD+).** O TVSDK pode passar dados de áudio Dolby Digital Plus (E-AC3) para o hardware de suporte.

* Recursos de proteção de conteúdo

   * **DRM para HLS.** Todas as APIs de reprodução de vídeo funcionam com conteúdo de vídeo criptografado protegido pelo Adobe Access. Os seguintes recursos DRM são compatíveis:

      * Rotação de licenças
      * Rotação de chaves
      * Cache de licença
      * Hora da política
      * Rotação IV

* **Reprodução AES 128.** O TVSDK pode reproduzir conteúdo HLS de padrão avançado de criptografia (AES) com tamanho de chave de 128 bits.
* **HLS protegido (PHLS)** O fornece um conjunto limitado de políticas de DRM pré-criadas, um subconjunto do que o Adobe Access oferece, para permitir DRM mais leve sobre HLS para fluxos ativos e de VOD.

* Recursos de publicidade/conteúdo alternativo e monetização

   * **Rastreamento de anúncios inseridos no lado do servidor.** O TVSDK pode rastrear anúncios inseridos pelo serviço de inserção de anúncios na nuvem do Adobe. Suporta anúncios lineares nos formatos VAST2, VAST3 e VMAP para VOD e fluxos dinâmicos/lineares.
   * **Tags HLS personalizadas.** O TVSDK usa o seu `MediaPlayerConfig` classe para ativar a notificação do aplicativo do reprodutor quando tags HLS personalizadas forem exibidas no fluxo.
   * **Inserção de anúncio no cliente.** A biblioteca de inserção de anúncios do Auditude funciona com servidores Adobe Auditude para resolver anúncios para inserção dinâmica em conteúdo dinâmico, linear e VOD, nas posições antes da exibição, durante a exibição ou após a exibição.
   * **Resolvedores de anúncios personalizados.** A variável `ContentResolver, OpportunityGenerator,` e `MediaPlayerClientFactory` As interfaces permitem implementar um resolvedor de conteúdo ad/alternativo personalizado e registrar um detector de oportunidade personalizado para trabalhar com o TVSDK. A variável `TestAdResolver` e `AuditudeResolver` As classes fornecem exemplos C++ de implementação de um resolvedor de conteúdo. Você pode encontrar um exemplo de Javascript em `samples/jspsdk/testapp/psdk.js`.
   * **Comportamento de anúncio consistente.** Use o `AdPolicySelector` para permitir um comportamento consistente em todos os players para operações como busca e truque de reprodução quando anúncios estão presentes no conteúdo. Se você não implementar o seu próprio, o TVSDK usa `DefaultAdPolicySelector`.
   * **Remova/substitua anúncios C3.** Use a API TVSDK apropriada para remover intervalos de conteúdo personalizados e inserir dinamicamente novos anúncios sem trabalho adicional de preparação. Isso é útil quando o conteúdo dinâmico/linear é transmitido e imediatamente disponibilizado sob demanda sem limpeza.

Estes são os novos recursos principais versão 2.4:

* **Instantâneo para VOD e live** Quando você ativa o recurso de ativação instantânea, o TVSDK inicializa e armazena em buffer a mídia antes do início da reprodução. Como é possível iniciar vários `MediaPlayerItemLoader` instâncias simultaneamente em segundo plano, é possível armazenar em buffer vários fluxos. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, a reprodução no novo canal é iniciada imediatamente. O TVSDK 2.4 também é compatível com o Instant On para fluxos ao vivo. Os fluxos ativos são colocados em buffer novamente quando a janela ativa se move.

* **Melhorias de desempenho **A nova arquitetura TVSDK 2.4 traz várias melhorias de desempenho:

   * **Subsegmentação** - O TVSDK reduz ainda mais o tamanho de cada fragmento para iniciar a reprodução o mais rápido possível.
   * **Downloads de anúncios paralelos** - O TVSDK busca previamente os anúncios em paralelo à reprodução do conteúdo antes de atingir os ad breaks, permitindo a reprodução perfeita de anúncios e conteúdo.
   * **Resolução de anúncio lento** - Com esse recurso, não aguardamos a resolução de anúncios não precedentes antes de iniciar a reprodução, diminuindo assim o tempo de inicialização. APIs como busca e truque ainda não são permitidas até que todos os anúncios sejam resolvidos.

* **Reprodução de conteúdo MP4**

Essa versão do TVSDK é compatível com a reprodução de MP4 como conteúdo principal.

* **Conexões de rede persistentes**

O TVSDK mantém um conjunto de conexões de rede reutilizáveis, de modo que não incorre na sobrecarga de criar e destruir uma conexão de rede para cada solicitação de rede.

* **Proteção de saída baseada em resolução**

Esse recurso vincula as restrições de reprodução a resoluções específicas, fornecendo controles DRM mais refinados.

* **Truque com a taxa de bits adaptável (ABR)**

Esse recurso permite que o TVSDK alterne entre fluxos do iFrame no modo de reprodução de truque. Você pode usar perfis que não sejam do iFrame para executar truques em velocidades mais baixas.

* **Truque mais suave**

Essas melhorias melhoram a experiência do usuário:

· Seleção adaptável da taxa de bits e da taxa de quadros durante a execução de truques, com base na largura de banda e no perfil de buffer

· Use a transmissão principal em vez da transmissão IDR para obter reprodução rápida de até 30 fps.

* **Lógica ABR aprimorada**

A nova lógica ABR é baseada no comprimento do buffer, na taxa de alteração do comprimento do buffer e na largura de banda medida. Isso garante que o ABR escolha a taxa de bits certa quando a largura de banda flutuar e também otimize o número de vezes que o switch de taxa de bits realmente ocorre, monitorando a taxa em que o comprimento do buffer muda.

* **Faturamento**

O TVSDK coleta métricas automaticamente, cumprindo o contrato de vendas do cliente para gerar relatórios de uso periódicos necessários para fins de faturamento. Em cada evento de início de fluxo, o TVSDK usa a API de inserção de dados do Adobe Analytics para enviar métricas de faturamento, como tipo de conteúdo, sinalizadores habilitados para inserção de anúncio e sinalizadores habilitados para drm, com base na duração do fluxo faturável, para o conjunto de relatórios do Adobe Analytics Primetime. Isso não interfere ou é incluído nos conjuntos de relatórios ou chamadas de servidor do próprio cliente do Adobe Analytics. Quando solicitado, esse relatório de uso de faturamento é enviado periodicamente aos clientes. Esta é a primeira fase do recurso de faturamento que suporta somente faturamento de uso. Ele pode ser configurado com base no contrato de vendas usando as APIs descritas na documentação.

## Recursos suportados {#supported-features}

O TVSDK para Android 2.4 é compatível com vários recursos que você pode implementar para adicionar funcionalidade aos seus aplicativos de vídeo.

>[!NOTE]
>
>Nas tabelas de matriz de recursos abaixo, um √ significa que o recurso é suportado na versão atual.

### Recursos principais de reprodução {#core-playback-features}

| **Recurso** | **Tipo de conteúdo** | **HLS** | **TRAÇO** |
|---|---|---|---|
| Reprodução geral (Reproduzir, Pausar, Buscar) | VOD + Ao vivo | √ | √ (somente VOD) |
| FER - Reprodução geral (Reproduzir, Pausar, Buscar) | FER VOD | √ | Não suportado |
| MP3 | VOD | Não suportado | Não suportado |
| Reprodução de conteúdo MP4 | VOD | √ | √ |
| Lógica de comutação de taxa de bits adaptável | VOD + Ao vivo | √ | Não suportado |
| Reprodução somente de áudio | VOD + Ao vivo | √ | Não suportado |
| Legendas codificadas - 608/708 | VOD + Ao vivo | √ | √ (somente VOD) |
| Legendas codificadas - WebVTT | VOD + Ao vivo | √ | √ (somente VOD) |
| Failover do manifesto | VOD + Ao vivo | √ | √ (somente VOD) |
| Failover avançado | VOD + Ao vivo | √ | √ (somente VOD) |
| Notificações de QoS e player | VOD + Ao vivo | √ | √ (somente VOD) |
| Suporte para cabeçalhos de cookie | VOD + Ao vivo | √ | √ (somente VOD) |
| Suporte para cabeçalhos personalizados | VOD + Ao vivo | Não suportado | Não suportado |
| Definir parâmetros de controle de buffer | VOD + Ao vivo | √ | √ (somente VOD) |
| Definir controles de taxa de bits adaptáveis | VOD + Ao vivo | √ | √ (somente VOD) |
| Tags de manifesto personalizadas (HLS) / Fluxos de eventos (DASH) | VOD + Ao vivo | √ | √ (somente VOD) |
| Áudio de associação tardia | VOD + Ao vivo | √ | √ (somente VOD) |
| Redirecionamento 302 | VOD + Ao vivo | √ | √ (somente VOD) |

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
   <td>Reprodução com Deslocamento</td> 
   <td>Ao vivo</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Reprodução somente de áudio</td> 
   <td>VOD + Ao vivo</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Truque Play </td> 
   <td>VOD + Ao vivo</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Truque suave (com ABR)</td> 
   <td>VOD + Ao vivo</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Análise de ID3 (HLS) / Metadados cronometrados (DASH)</td> 
   <td>VOD + Ao vivo</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Blecouts </td> 
   <td>VOD + Ao vivo</td> 
   <td>Não suportado</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Instantâneo</td> 
   <td>VOD + Ao vivo</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Suporte a marcador de descontinuidade (HLS) </li> 
     <li>Vários períodos (TRAÇO)</li> 
    </ul> </td> 
   <td>VOD + Ao vivo</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>302 Fisidez de redirecionamento</td> 
   <td>VOD + Ao vivo</td> 
   <td>√</td> 
   <td>√ (somente VOD)</td> 
  </tr>
  <tr>
   <td>Depuração de miniatura (Iframe e JPEG)</td> 
   <td>VOD + Ao vivo</td> 
   <td>Não suportado</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Integridade do fluxo </td> 
   <td>VOD + Ao vivo</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
 </tbody>
</table>

### Recursos do Ad Insertion principal (CSAI) {#core-ad-insertion-features-csai}

| **Recurso** | **Tipo de conteúdo** | **HLS** | **TRAÇO** |
|---|---|---|---|
| Reprodução geral, anúncios ativados | VOD + Ao vivo | √ | √ (apenas pré-rolagens de VOD) |
| Conteúdo de oferta com anúncios ativados | VOD | √ | Não suportado |
| Comportamentos de anúncio padrão | VOD + Ao vivo | √ | √ (apenas pré-rolagens de VOD) |
| VAST 2.0/3.0 | VOD + Ao vivo | √ | √ (apenas pré-rolagens de VOD) |
| VMAP 1.0 | VOD + Ao vivo | √ | √ (apenas pré-rolagens de VOD) |
| Anúncios MP4 | VOD + Ao vivo | √ (do CRS) | √ (do CRS, apenas pré-rolos) |

### Recursos avançados do Ad Insertion (CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>Recurso</strong></td> 
   <td><strong>Tipo de conteúdo</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>TRAÇO</strong></td> 
  </tr>
  <tr>
   <td>Truque Play com anúncios ativados</td> 
   <td>VOD + Ao vivo</td> 
   <td>√</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Somente anúncio </td> 
   <td>VOD</td> 
   <td>Não suportado</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Parâmetros de direcionamento</td> 
   <td>VOD + Ao vivo</td> 
   <td>√</td> 
   <td>√ (apenas pré-rolagens de VOD)</td> 
  </tr>
  <tr>
   <td>Parâmetros personalizados</td> 
   <td>VOD + Ao vivo</td> 
   <td>√</td> 
   <td>√ (apenas pré-rolagens de VOD)</td> 
  </tr>
  <tr>
   <td>Comportamentos de anúncio personalizados</td> 
   <td>VOD + Ao vivo</td> 
   <td>√</td> 
   <td>√ (apenas pré-rolagens de VOD)</td> 
  </tr>
  <tr>
   <td>Tags de anúncio personalizadas</td> 
   <td>Ao vivo</td> 
   <td>√ </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Resolvedores de anúncios personalizados</td> 
   <td>VOD + Ao vivo</td> 
   <td>√ </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Resolvedor de anúncios personalizados Freewheel</td> 
   <td>VOD</td> 
   <td>Não suportado</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Substituição de anúncio C3 </td> 
   <td>VOD + Ao vivo</td> 
   <td>√ </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Carregamento lento de anúncio</td> 
   <td>VOD</td> 
   <td>√ </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Suporte a marcador de descontinuidade - SSAI (HLS) </li> 
     <li>Vários períodos (TRAÇO)</li> 
    </ul> </td> 
   <td>VOD + Ao vivo</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>Anúncios complementares, anúncios de banner e anúncios clicáveis</td> 
   <td>VOD + Ao vivo</td> 
   <td>√ </td> 
   <td>√ (apenas pré-rolagens de VOD)</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + Ao vivo</td> 
   <td>√ (JS) </td> 
   <td>√ (apenas pré-rolagens de VOD)</td> 
  </tr>
  <tr>
   <td>Saída antecipada do anúncio</td> 
   <td>Ao vivo</td> 
   <td>√ </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>VOD criativo baseado em regras + Priorização em tempo real</td> 
   <td>VOD + Ao vivo</td> 
   <td>√ </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Regras CRS </td> 
   <td>VOD + Ao vivo</td> 
   <td>√ </td> 
   <td>Não suportado</td> 
  </tr>
 </tbody>
</table>

## Recursos de proteção de conteúdo {#content-protection-features}

| **Recurso** | **Tipo de conteúdo** | **HLS** | **TRAÇO** |
|---|---|---|---|
| Criptografia AES | VOD + Ao vivo | √ | √ (somente VOD) |
| Exemplo de criptografia AES | VOD + Ao vivo | √ |  |
| Fluxos Tokenizados | VOD + Ao vivo | √ |  |
| DRM | VOD + Ao vivo | Somente DRM do Primetime (Futuro: Widevine) | Somente Widevine |
| Reprodução externa (RBOP) | VOD + Ao vivo | Somente DRM do Primetime | Não suportado |
| Rotação de licenças | VOD + Ao vivo | Somente DRM do Primetime | Não suportado |
| Rotação de chaves | VOD + Ao vivo | Somente DRM do Primetime | Não suportado |

### Recursos da integração {#integration-features}

| **Recurso** | **Tipo de conteúdo** | **HLS** | **TRAÇO** |
|---|---|---|---|
| Integração com o Adobe Analytics VHL | VOD + Ao vivo | √ | √ |
| Faturamento | VOD + Ao vivo | √ | Não suportado |

## Recursos não suportados {#features-not-supported}

Esta versão do TVSDK não é compatível com:

* Blecaute de anúncios.
* Movimento lento em truques.
* Buscar e executar truques com conteúdo MP4.
* Inserção de anúncio com conteúdo principal em MP4.
* Procure quando um anúncio está sendo reproduzido.
* Reprodução de anúncios com mídia somente de áudio.

## Problemas conhecidos e limitações {#known-issues-and-limitations}

Essa versão do TVSDK apresenta os seguintes problemas:

* Dispositivo específico (Samsung Galaxy Tab 4) falha VOD DRM LBA com auditude e clique em anúncios
* O anúncio posterior à exibição não é reproduzido para um conteúdo específico.
* A definição de legendas ocultas para idiomas CJK não funciona.
* O vídeo pode sair do modo de truque automaticamente entre VOD e ao vivo.
* VHL - chamadas de heartbeat incorretas são enviadas quando iniciamos um conteúdo de um deslocamento.
* Quando os anúncios VPAID são reproduzidos, as chamadas de heartbeat do VHL para o evento:type:não estão presentes anúncios.
* O anúncio precedente é reproduzido mesmo quando adBreakPolicy SKIP é escolhido.
* Depois de entrar no estado Concluído, o player volta ao estado Reproduzindo com IGNORAR adBreakPolicy para anúncios pós-exibição.

Sem o vídeo, não há dimensão de visor e, sem uma dimensão de visor, não é possível exibir gráficos para legendas.

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
