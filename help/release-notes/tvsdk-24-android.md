---
title: Notas de versão do TVSDK 2.4.1 para Android
description: TVSDK 2.4.1 para Notas de versão do Android descreve os recursos novos e compatíveis e os problemas conhecidos e limitações no TVSDK Android 2.4.1.
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 3de09048-ae32-43b4-a019-34b217931a4c
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 0%

---

# Notas de versão do TVSDK 2.4.1 para Android {#tvsdk-for-android-release-notes}

TVSDK 2.4.1 para Notas de versão do Android descreve os recursos novos e compatíveis e os problemas conhecidos e limitações no TVSDK Android 2.4.1.

## TVSDK Android 2.4.1 {#tvsdk-android}

O Adobe está lançando o TVSDK 2.4.1 para Android.

Para usar essa versão do TVSDK, verifique se o sistema atende aos requisitos descritos em [Requisitos do sistema](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

Aqui está a documentação:

・ Sistema de ajuda online TVSDK 2.4 para Ajuda do Android

・ ・ [Javadocs TVSDK 2.4 para API Java do Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Os Javadocs são a autoridade mais avançada, pois são gerados automaticamente diretamente do código fonte do TVSDK.

・ ・ [Documentação da API C++ TVSDK 2.4 para API C++ do Android](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

Cada classe Java tem uma classe C++ correspondente, e a documentação C++ contém mais material explicativo do que os Javadocs, portanto, consulte a documentação C++ para obter uma compreensão mais profunda da API Java.

・ Guia de migração ([Guia de migração do TVSDK 2.4 para Android](../migration-guides/tvsdk-14-25-android.md))

Este guia explica o que você precisa modificar para migrar um aplicativo com base em TVSDK 1.4 para um com base em TVSDK 2.4.

## Novos recursos {#new-features}

O TVSDK 2.4.1 para Android fornece muitas melhorias de desempenho em relação às versões anteriores. Ele fornece uma experiência de exibição de alta qualidade.

Esta versão inclui todos os recursos das versões 2.4 e 2.4.1, e nenhum recurso foi descontinuado.

Estes são os principais novos recursos da versão 2.4.1:

* Recursos da versão 4 do HLS

   * **Reprodução de vídeo** (reproduzir, pausar, buscar) com controle de player para fluxos ao vivo, linear e VOD.
   * **Legendas ocultas.** O TVSDK pode exibir legendas ocultas 608/708 com uma seleção de fontes, tamanhos de fonte, cores e plano de fundo. Ele também pode oferecer suporte a vídeos com legendas de roll-up e alternar entre faixas de idioma, se estiverem disponíveis.
   * **Modo de reprodução de truque** O suporta avanço rápido e retrocesso para fluxos HLS que usam I-Frames. Todos os controles de reprodução de vídeo funcionam no conteúdo. O movimento lento (para a frente) está disponível para o modo de reprodução de vídeo externo com taxas entre 0 e 1.
   * **Taxa de bits adaptável (ABR)** permite que o reprodutor selecione dinamicamente qual das várias versões do mesmo fluxo de conteúdo deve ser reproduzido, com base na rede e em outras condições. Você pode definir parâmetros dinamicamente ou no arquivo de manifesto para selecionar entre políticas de seleção agressivas, moderadas e conservadoras.
   * **Intervalos de bytes** permitir que um único arquivo TS contenha vários segmentos TS.
   * **Representações de áudio alternativas** habilite o reprodutor a alternar entre as faixas de áudio disponíveis.
   * **Suporte para ID3.** O TVSDK pode reproduzir fluxos de áudio e vídeo HLS que contêm metadados de áudio ID3, como nome do artista, título e álbum.
   * **Failover. **O TVSDK usa estratégias para continuar a reprodução ininterrupta, apesar das falhas de servidores de host, arquivos de lista de reprodução e segmentos.
   * **Passagem de áudio multicanal (DD+).** O TVSDK pode transmitir dados de áudio Dolby Digital Plus (E-AC3) para o hardware de suporte.

* Recursos de proteção de conteúdo

   * **DRM para HLS.** Todas as APIs de reprodução de vídeo funcionam com conteúdo de vídeo criptografado protegido pelo Acesso ao Adobe. Os seguintes recursos de DRM são suportados:

      * Rotação de licença
      * Rotação de chaves
      * Armazenamento em cache de licenças
      * Hora da política
      * Rotação IV

* **Reprodução AES 128.** O TVSDK pode reproduzir conteúdo HLS padrão de criptografia avançada (AES) com tamanho de chave de 128 bits.
* **HLS protegido (PHLS)** O fornece um conjunto limitado de políticas de DRM pré-criadas, um subconjunto do que o Adobe Access fornece, para habilitar o DRM leve sobre HLS para fluxos dinâmicos e de VOD.

* Conteúdo de publicidade/alternativo e recursos de monetização

   * **Rastreamento de anúncios inseridos no servidor.** O TVSDK pode rastrear anúncios inseridos pelo serviço de inserção de anúncios da Adobe Cloud. Ele suporta anúncios lineares nos formatos VAST2, VAST3 e VMAP para fluxos VOD e live/lineares.
   * **Tags HLS personalizadas.** O TVSDK usa `MediaPlayerConfig` classe para habilitar a notificação do aplicativo do player quando tags HLS personalizadas forem exibidas no fluxo.
   * **Inserção de anúncio no lado do cliente.** A biblioteca Auditude e inserção funciona com servidores da Adobe Auditude para resolver anúncios para inserção dinamicamente em conteúdo ativo, linear e VOD, em posições precedentes, intermediárias ou posteriores.
   * **Resolvedores de anúncios personalizados.** O `ContentResolver, OpportunityGenerator,` e `MediaPlayerClientFactory` as interfaces permitem implementar um resolvedor de conteúdo de anúncio/alternativo personalizado e registrar um detector de oportunidade personalizado para trabalhar com o TVSDK. O `TestAdResolver` e `AuditudeResolver` As classes fornecem exemplos de C++ da implementação de um resolvedor de conteúdo. Você pode encontrar um exemplo de Javascript em `samples/jspsdk/testapp/psdk.js`.
   * **Comportamento consistente do anúncio.** Use o `AdPolicySelector` para permitir um comportamento consistente em todos os players para operações como busca e truques de reprodução quando anúncios estão presentes no conteúdo. Se você não implementar o seu próprio, o TVSDK usará `DefaultAdPolicySelector`.
   * **Remova/substitua anúncios C3.** Use a API TVSDK apropriada para remover intervalos de conteúdo personalizados e inserir dinamicamente novos anúncios sem trabalho de preparação adicional. Isso é útil quando o conteúdo ao vivo/linear é transmitido e imediatamente disponibilizado sob demanda sem limpeza.

Estes são os principais novos recursos da versão 2.4:

* **Instantâneo para VOD e ao vivo** Quando você ativa o instantâneo, o TVSDK inicializa e armazena em buffer a mídia antes do início da reprodução. Porque você pode iniciar vários `MediaPlayerItemLoader` instâncias simultaneamente em segundo plano, é possível fazer o buffer de vários fluxos. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, a reprodução no novo canal é iniciada imediatamente. O TVSDK 2.4 também é compatível com o Instant On para fluxos ao vivo. Os fluxos ao vivo são rearmazenados em buffer quando a janela ao vivo se move.

* **Melhorias de desempenho **A nova arquitetura TVSDK 2.4 traz várias melhorias de desempenho:

   * **Subsegmentação** - O TVSDK reduz ainda mais o tamanho de cada fragmento para iniciar a reprodução o mais rápido possível.
   * **Downloads de anúncios paralelos** - O TVSDK busca previamente anúncios em paralelo à reprodução do conteúdo antes de clicar nas quebras de anúncio, permitindo uma reprodução contínua de anúncios e conteúdo.
   * **Resolução de anúncio preguiçosa** - Com esse recurso, não esperamos a resolução de anúncios não pré-realizáveis antes de iniciar a reprodução, diminuindo assim o tempo de inicialização. As APIs como busca e trick-play ainda não são permitidas até que todos os anúncios sejam resolvidos.

* **Reprodução de conteúdo MP4**

Esta versão do TVSDK é compatível com a reprodução do MP4 como conteúdo principal.

* **Conexões de rede persistentes**

O TVSDK mantém um conjunto de conexões de rede reutilizáveis, de modo que não incorre na sobrecarga da criação e destruição de uma conexão de rede para cada solicitação de rede.

* **Proteção de saída baseada em resolução**

Esse recurso vincula as restrições de reprodução a resoluções específicas, fornecendo controles de DRM mais refinados.

* **Trick play com a taxa de bits adaptável (ABR)**

Esse recurso permite que o TVSDK alterne entre fluxos do iFrame no modo de reprodução de truques. Você pode usar perfis que não sejam iFrame para fazer reprodução de truques em velocidades mais baixas.

* **Jogo de truques mais suave**

Essas melhorias aprimoram a experiência do usuário:

・ Seleção adaptável da taxa de bits e da taxa de quadros durante a reprodução do truque, com base na largura de banda e no perfil do buffer

・ Use o fluxo principal em vez do fluxo IDR para obter uma reprodução rápida de até 30 fps.

* **Lógica de ABR aprimorada**

A nova lógica ABR é baseada no comprimento do buffer, na taxa de alteração do comprimento do buffer e na largura de banda medida. Isso garante que o ABR escolha a taxa de bits correta quando a largura de banda flutuar e também otimiza o número de vezes em que a mudança da taxa de bits realmente acontece, monitorando a taxa em que o comprimento do buffer muda.

* **Faturamento**

O TVSDK coleta automaticamente métricas, de acordo com o contrato de vendas do cliente, para gerar relatórios de uso periódicos necessários para fins de faturamento. Em cada evento de início de fluxo, o TVSDK usa a API de inserção de dados do Adobe Analytics para enviar métricas de faturamento, como tipo de conteúdo, sinalizadores ativados para inserção de anúncio e sinalizadores habilitados para drm - com base na duração do fluxo faturável - para o conjunto de relatórios pertencente ao Adobe Analytics Primetime. Isso não interfere ou é incluído nos próprios conjuntos de relatórios ou chamadas de servidor do Adobe Analytics do cliente. Mediante solicitação, esse relatório de uso de faturamento é enviado periodicamente aos clientes. Esta é a primeira fase do recurso de faturamento que suporta somente cobrança de uso. Ele pode ser configurado com base no contrato de vendas usando as APIs descritas na documentação.

## Recursos suportados {#supported-features}

O TVSDK para Android 2.4 é compatível com diversos recursos que podem ser implementados para adicionar funcionalidade aos seus aplicativos de vídeo.

>[!NOTE]
>
>Nas tabelas da matriz de recursos abaixo, um √ significa que o recurso é suportado na versão atual.

### Recursos principais da reprodução {#core-playback-features}

| **Recurso** | **Tipo de conteúdo** | **HLS** | **PASH** |
|---|---|---|---|
| Reprodução geral (Reproduzir, Pausar, Buscar) | VOD + Ao vivo | éc | Ö (apenas VOD) |
| FER - Reprodução geral (Reproduzir, Pausar, Buscar) | FER VOD | éc | Não suportado |
| MP3 | VOD | Não suportado | Não suportado |
| Reprodução de conteúdo MP4 | VOD | éc | éc |
| Lógica de switching da taxa de bits adaptável | VOD + Ao vivo | éc | Não suportado |
| Reprodução Apenas Áudio | VOD + Ao vivo | éc | Não suportado |
| Legendas ocultas - 608/708 | VOD + Ao vivo | éc | Ö (apenas VOD) |
| Legendas ocultas - WebVTT | VOD + Ao vivo | éc | Ö (apenas VOD) |
| Failover Manifest | VOD + Ao vivo | éc | Ö (apenas VOD) |
| Failover avançado | VOD + Ao vivo | éc | Ö (apenas VOD) |
| Notificações de QoS e player | VOD + Ao vivo | éc | Ö (apenas VOD) |
| Suporte para cabeçalhos de cookies | VOD + Ao vivo | éc | Ö (apenas VOD) |
| Suporte para cabeçalhos personalizados | VOD + Ao vivo | Não suportado | Não suportado |
| Definir parâmetros de controle de buffer | VOD + Ao vivo | éc | Ö (apenas VOD) |
| Definir controles adaptáveis da taxa de bits | VOD + Ao vivo | éc | Ö (apenas VOD) |
| Tags de manifesto personalizadas (HLS) / Fluxos de evento (DASH) | VOD + Ao vivo | éc | Ö (apenas VOD) |
| Áudio com limite tardio | VOD + Ao vivo | éc | Ö (apenas VOD) |
| 302 Redirecionamento | VOD + Ao vivo | éc | Ö (apenas VOD) |

### Recursos avançados de reprodução {#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>Recurso</strong></td> 
   <td><strong>Tipo de conteúdo</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>PASH</strong></td> 
  </tr>
  <tr>
   <td>Reprodução com deslocamento</td> 
   <td>Ao vivo</td> 
   <td>éc</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Reprodução Apenas Áudio</td> 
   <td>VOD + Ao vivo</td> 
   <td>éc</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Trick Play </td> 
   <td>VOD + Ao vivo</td> 
   <td>éc</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Play suave de truques (com ABR)</td> 
   <td>VOD + Ao vivo</td> 
   <td>éc</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Análise de ID3 (HLS) / Metadados cronometrados (DASH)</td> 
   <td>VOD + Ao vivo</td> 
   <td>éc</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Blackouts </td> 
   <td>VOD + Ao vivo</td> 
   <td>Não suportado</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Instantâneo ativado</td> 
   <td>VOD + Ao vivo</td> 
   <td>éc</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Suporte a marcador de descontinuidade (HLS) </li> 
     <li>Período múltiplo (DASH)</li> 
    </ul> </td> 
   <td>VOD + Ao vivo</td> 
   <td>éc</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>302 Redirecionar adesão</td> 
   <td>VOD + Ao vivo</td> 
   <td>éc</td> 
   <td>Ö (apenas VOD)</td> 
  </tr>
  <tr>
   <td>Depuração em miniatura (Iframe e JPEG)</td> 
   <td>VOD + Ao vivo</td> 
   <td>Não suportado</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Integridade de fluxo </td> 
   <td>VOD + Ao vivo</td> 
   <td>éc</td> 
   <td>Não suportado</td> 
  </tr>
 </tbody>
</table>

### Recursos do Ad Insertion principal (CSAI) {#core-ad-insertion-features-csai}

| **Recurso** | **Tipo de conteúdo** | **HLS** | **PASH** |
|---|---|---|---|
| Reprodução geral, anúncios ativados | VOD + Ao vivo | éc | √ (apenas VOD) |
| CONSULTE o conteúdo dos anúncios ativados | VOD | éc | Não suportado |
| Comportamentos de publicidade padrão | VOD + Ao vivo | éc | √ (apenas VOD) |
| VAST 2.0/3.0 | VOD + Ao vivo | éc | √ (apenas VOD) |
| VMAP 1.0 | VOD + Ao vivo | éc | √ (apenas VOD) |
| Anúncios MP4 | VOD + Ao vivo | Ö (do SIR) | Ö (do SIR, apenas em pré-rolos) |

### Recursos avançados do Ad Insertion (CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>Recurso</strong></td> 
   <td><strong>Tipo de conteúdo</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>PASH</strong></td> 
  </tr>
  <tr>
   <td>Trick Play com anúncios ativados</td> 
   <td>VOD + Ao vivo</td> 
   <td>éc</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Somente publicidade </td> 
   <td>VOD</td> 
   <td>Não suportado</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Parâmetros de direcionamento</td> 
   <td>VOD + Ao vivo</td> 
   <td>éc</td> 
   <td>√ (apenas VOD)</td> 
  </tr>
  <tr>
   <td>Parâmetros personalizados</td> 
   <td>VOD + Ao vivo</td> 
   <td>éc</td> 
   <td>√ (apenas VOD)</td> 
  </tr>
  <tr>
   <td>Comportamentos de anúncio personalizados</td> 
   <td>VOD + Ao vivo</td> 
   <td>éc</td> 
   <td>√ (apenas VOD)</td> 
  </tr>
  <tr>
   <td>Tags de anúncio personalizadas</td> 
   <td>Ao vivo</td> 
   <td>éc </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Resolvedores de anúncios personalizados</td> 
   <td>VOD + Ao vivo</td> 
   <td>éc </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Resolvedor de anúncio personalizado do Freewheel</td> 
   <td>VOD</td> 
   <td>Não suportado</td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Substituição de anúncio C3 </td> 
   <td>VOD + Ao vivo</td> 
   <td>éc </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Carregamento de anúncio lento</td> 
   <td>VOD</td> 
   <td>éc </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Suporte a marcador de descontinuidade - SSAI (HLS) </li> 
     <li>Período múltiplo (DASH)</li> 
    </ul> </td> 
   <td>VOD + Ao vivo</td> 
   <td>éc </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>Anúncios complementares, anúncios em banners e anúncios clicáveis</td> 
   <td>VOD + Ao vivo</td> 
   <td>éc </td> 
   <td>√ (apenas VOD)</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + Ao vivo</td> 
   <td>Ö (JS) </td> 
   <td>√ (apenas VOD)</td> 
  </tr>
  <tr>
   <td>Saída do anúncio antecipado</td> 
   <td>Ao vivo</td> 
   <td>éc </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Creative VOD com base em regras + Priorização ao vivo</td> 
   <td>VOD + Ao vivo</td> 
   <td>éc </td> 
   <td>Não suportado</td> 
  </tr>
  <tr>
   <td>Regras CRS </td> 
   <td>VOD + Ao vivo</td> 
   <td>éc </td> 
   <td>Não suportado</td> 
  </tr>
 </tbody>
</table>

## Recursos da proteção de conteúdo {#content-protection-features}

| **Recurso** | **Tipo de conteúdo** | **HLS** | **PASH** |
|---|---|---|---|
| Criptografia AES | VOD + Ao vivo | éc | Ö (apenas VOD) |
| Criptografia AES de amostra | VOD + Ao vivo | éc |  |
| Fluxos Tokenized | VOD + Ao vivo | éc |  |
| DRM | VOD + Ao vivo | Somente DRM do Primetime (Futuro: Widevine) | Somente viúva |
| Reprodução externa (RBOP) | VOD + Ao vivo | Somente DRM do Primetime | Não suportado |
| Rotação de licença | VOD + Ao vivo | Somente DRM do Primetime | Não suportado |
| Rotação da Chave | VOD + Ao vivo | Somente DRM do Primetime | Não suportado |

### Recursos da integração {#integration-features}

| **Recurso** | **Tipo de conteúdo** | **HLS** | **PASH** |
|---|---|---|---|
| Integração do Adobe Analytics VHL | VOD + Ao vivo | éc | éc |
| Faturamento | VOD + Ao vivo | éc | Não suportado |

## Recursos não suportados {#features-not-supported}

Esta versão do TVSDK não é compatível com:

* Blecaute de anúncios.
* Movimento lento na peça.
* Buscar e jogar com conteúdo MP4.
* Inserção de anúncio com conteúdo principal MP4.
* Procure quando um anúncio está sendo reproduzido.
* Reprodução de anúncios com mídia somente de áudio.

## Problemas conhecidos e limitações {#known-issues-and-limitations}

Essa versão do TVSDK apresenta os seguintes problemas:

* Específico do dispositivo (Samsung Galaxy Tab 4) falha VOD DRM LBA com auditude e clica nos anúncios
* O anúncio posterior não é reproduzido para um conteúdo específico.
* A configuração da legenda de fechamento para idiomas CJK não funciona.
* O vídeo pode sair do modo de truque automaticamente entre VOD e live.
* VHL - chamadas de pulsação incorretas são enviadas quando iniciamos um conteúdo de um deslocamento.
* Quando anúncios VPAID são reproduzidos, as chamadas de pulsação VHL são para o evento:type:o anúncio de reprodução está ausente.
* O anúncio precedente é reproduzido mesmo quando o SKIP adBreakPolicy é escolhido.
* Depois de entrar no player de estado completo, retorna ao estado Reprodução com SKIP adBreakPolicy para anúncios pós-rolagem.

Sem vídeo, não há dimensão do visor e sem uma dimensão do visor, não é possível exibir gráficos de legendas.

## Recursos úteis {#helpful-resources}

* Consulte a documentação completa de ajuda em [Aprendizagem e suporte do Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
