---
title: Notas de versão do TVSDK 2.7 para Android™
description: Notas de versão do TVSDK 2.7 para Android™ descrevem as novidades ou alterações, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK Android™ 2.7
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: d64f0ef2-60a9-43a1-b2f9-44764a570538
source-git-commit: d2c8133f126db44b9c505dc0a21ba208fd6c01c8
workflow-type: tm+mt
source-wordcount: '4072'
ht-degree: 0%

---

# Notas de versão do TVSDK 2.7 para Android™ {#tvsdk-for-android-release-notes}

Notas de versão do TVSDK 2.7 para Android™ descrevem as novidades ou alterações, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK Android™ 2.7

## TVSDK Android™ 2.7 {#tvsdk-android}

O reprodutor de referência Android™ está incluído com Android™ TVSDK nas amostras/diretórios de sua distribuição. O arquivo README&lt;.md associado explica como criar o reprodutor de referência.

>[!NOTE]
>
>Para criar com êxito o reprodutor de referência, conforme descrito em README.md distribuído com a versão, faça o seguinte:
>
>1. Baixe o VideoHeartbeat.jar de [https://github.com/Adobe-Marketing-Cloud/media-sdks/releases](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) (Biblioteca VideoHeartbeat para Android™ v2.0.0)
>1. Extraia VideoHeartbeat.jar para a pasta libs/ .

>


## Novos recursos {#new-features}

O TVSDK 2.7 para Android™ inclui todos os recursos da versão 1.4, exceto os recursos não suportados listados em [Matriz de recursos](#feature-matrix).

**Android™ TVSDK 2.7**

* **Suporte para resolução de anúncio paralelo**

O TVSDK 2.7 é compatível com a resolução simultânea de todas as solicitações de anúncio em um Ad break, em vez da resolução sequencial.

### Novos recursos das versões anteriores {#new-features-previous-releases}

**Versão 2.5.6**

* **O TVSDK 2.5 é compatível com Android™ P**
* **Ativar áudio em segundo plano**

   Para ativar a reprodução de áudio quando o aplicativo se move de primeiro para segundo plano, o aplicativo deve chamar a API enableAudioPlaybackInBackground do MediaPlayer com o argumento true quando o player estiver no estado PREPARED.

* **alwaysUseAudioOutputLatency(boolean val) na classe MediaPlayer**

Quando definido, use a latência de saída no cálculo do carimbo de data e hora de áudio.
Parâmetros booleanos val - True usa a latência de saída de áudio no cálculo de carimbo de data e hora de áudio.

* **Otimizado para obter a melhor experiência de reprodução mesmo se a velocidade da largura de banda cair de repente.**
O TVSDK agora cancela o download do segmento em andamento, se necessário, e alterna dinamicamente para a representação apropriada. Isso é feito alternando facilmente entre as taxas de bits sem interrupções.

**Versão 2.5.5**

* **Inserção parcial de ad-break**

   Experiência semelhante à da TV de participar do meio de um anúncio sem acionar o rastreamento do anúncio parcialmente assistido.\
   Exemplo**: **O usuário entra no meio (em 40 segundos) de um ad break de 90 segundos que consiste em três anúncios de 30 segundos. Isso é de 10 segundos no segundo anúncio no intervalo.
   * O segundo anúncio é reproduzido pela duração restante (20 segundos) seguido do terceiro anúncio.
   * Os rastreadores de anúncios do anúncio parcial reproduzido (segundo anúncio) não são acionados. Os rastreadores somente do terceiro anúncio são disparados.

* **Carregamento de anúncio seguro por HTTPS**

   A Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios do Primetime e o CRS por https.

* **AdSystem e Creative Id adicionados às solicitações CRS**

   * Agora, incluindo &quot;AdSystem&quot; e &quot;CreativeId&quot; como novos parâmetros nas solicitações 1401 e 1403.

* **API setEncodeUrlForTracking na classe NetworkConfiguration removida** como os caracteres não seguros em um URL devem ser codificados.

**Versão 2.5.4**

O Android™ TVSDK v2.5.4 oferece as seguintes atualizações e alterações da API:

* Alterações no valor padrão de `WebViewDebbuging`

   `WebViewDebbuging` por padrão, os valores são definidos como False. Para habilitá-lo, chame setWebCon`tentsDebuggingEnabled(true) no aplicativo.
* Atualização de versão do OpenSSL e do Curl atualizada `libcurl` para v7.57.0 e OpenSSL para v1.0.2k.
* Acesso no nível do aplicativo para o objeto de resposta VAST Introduziu uma nova API NetworkAdInfo::getVastXml() que fornece acesso ao objeto de resposta VAST para o aplicativo.

**Versão 2.5.3**

O Android™ TVSDK v2.5.3 oferece as seguintes atualizações e alterações da API.

* Todos os clientes TVSDK que usam CRS são incentivados a atualizar seus aplicativos com TVSDK 2.5.3.85 ou posterior no Android™. Esta é uma substituição direta da implementação do aplicativo existente. Após a atualização do TVSDK, verifique as solicitações de URL criativo do CRS em uma ferramenta proxy (por exemplo: Charles) e confirme se o nome do host e a versão no caminho refletem como na estrutura de URL de amostra abaixo.

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* Agente do usuário do TVSDK personalizável: adicionamos novas APIs para personalizar os agentes do usuário.

   * `setCustomUserAgent`(Valor da string)
   * `getCustomUserAgent`(2)

* Compartilhe cookies entre o aplicativo Android™ e o TVSDK: O Android™ TVSDK agora oferece suporte ao acesso de cookies entre a camada Java™ (armazenada no CookieStore do aplicativo Android™) e a camada C++ TVSDK. Agora, é possível definir e/ou modificar os cookies na camada C++ nativa, pois são expostos à Loja de Cookies Java™.
* Alterações na API:

   * Um novo Event CookiesUpdatedEvent é adicionado. Ele é enviado pelo reprodutor de mídia quando seu cookie é atualizado.
   * Uma nova API é adicionada a `NetworkConfiguration::set/ getCustomUserAgent()` para usar um agente de usuário personalizado.
   * Uma nova API é adicionada a `NetworkConfiguration::set/ getEncodedUrlForTracking` para forçar a codificação de caracteres não seguros.
   * Uma nova API é adicionada a `NetworkConfiguration::getNetworkDownVerificationUrl()` para definir um URL de verificação de rede se houver um failover.
   * Uma nova propriedade é adicionada a TextFormat::tratSpaceAsAlphaNum, que define se o espaço deve ser tratado como alfanumérico ao exibir legendas.

* Alterações na `SizeAvailableEvent`: Anteriormente, os métodos getHeight() e getWidth() de `SizeAvailableEvent` na versão 2.5.2, usada para retornar a altura e a largura do quadro, que foi retornada pelo formato de mídia. Agora, retorna a altura de saída e a largura de saída respectivamente retornadas pelo decodificador.
* Alterações no comportamento do buffer: O comportamento do buffer é alterado. Fica à disposição do desenvolvedor de aplicativos no que ele deseja fazer se houver buffer vazio. 2.5.3 usa o tamanho do buffer de reprodução em uma situação vazia do buffer.

**Versão 2.5.2**

O Android™ TVSDK v2.5.2 oferece correções de erros importantes e algumas alterações na API.

**Versão 2.5.1**

Os novos recursos importantes lançados no Android™ 2.5.1.

* **Melhorias de desempenho** A nova arquitetura TVSDK 2.5.1 traz várias melhorias de desempenho. Com base em estatísticas de um estudo de avaliação de desempenho de terceiros, a nova arquitetura oferece uma redução de 5 vezes no tempo de inicialização e 3,8 vezes menos quadros ignorados em comparação à média do setor:

   * **Instantâneo para VOD e ao vivo -** Quando você ativa o instantâneo, o TVSDK inicializa e armazena em buffer a mídia antes do início da reprodução. Como você pode iniciar várias instâncias MediaPlayerItemLoader simultaneamente em segundo plano, é possível fazer o buffer de vários fluxos. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, a reprodução no novo canal é iniciada imediatamente. O TVSDK 2.5.1 também é compatível com o Instant On para **live** também. Os fluxos ao vivo são rearmazenados em buffer quando a janela ao vivo se move.

      * **Lógica de ABR aprimorada -** A nova lógica ABR é baseada no comprimento do buffer, na taxa de alteração do comprimento do buffer e na largura de banda medida. Isso garante que o ABR escolha a taxa de bits correta quando a largura de banda flutuar e também otimiza o número de vezes em que a mudança da taxa de bits realmente acontece, monitorando a taxa em que o comprimento do buffer muda.
      * **Download/subsegmentação parcial do segmento -** O TVSDK reduz ainda mais o tamanho de cada fragmento, para iniciar a reprodução o mais rápido possível. O fragmento ts deve ter um quadro chave a cada dois segundos.
      * **Resolução de anúncios preguiçosa -** O TVSDK não espera pela resolução de anúncios não pré-implantados antes de iniciar a reprodução, diminuindo assim o tempo de inicialização. As APIs como busca e trick-play ainda não são permitidas até que todos os anúncios sejam resolvidos. Isso é aplicável a fluxos VOD usados com CSAI. Operações como buscar e avançar rapidamente não são permitidas até que a resolução do anúncio seja concluída. Para fluxos ao vivo, esse recurso não pode ser ativado para resolução de anúncios durante um evento ao vivo.
      * **Conexões de rede persistentes -** Esse recurso permite que o TVSDK crie e armazene uma lista interna de conexões de rede persistentes. Essas conexões são reutilizadas para várias solicitações, em vez de abrir uma nova conexão para cada solicitação de rede e depois destruí-la. Isso aumenta a eficiência e diminui a latência no código de rede, resultando em um desempenho de reprodução mais rápido.
Quando o TVSDK abre uma conexão, ele solicita ao servidor uma *keep-alive* conexão. Alguns servidores podem não oferecer suporte a esse tipo de conexão, nesse caso, o TVSDK retorna para fazer uma conexão para cada solicitação novamente. Além disso, embora as conexões persistentes estejam ativadas por padrão, o TVSDK agora tem uma opção de configuração para que os aplicativos possam desativar as conexões persistentes, se desejado.
      * **Download paralelo -** Baixar vídeo e áudio em paralelo, em vez de em série, reduz os atrasos na inicialização. Esse recurso permite que arquivos HLS Live e VOD sejam reproduzidos, otimiza o uso da largura de banda disponível de um servidor, diminui a probabilidade de entrar em situações de buffer em execução insuficiente e minimiza o atraso entre o download e a reprodução.
      * **Downloads de anúncios paralelos -** O TVSDK busca previamente anúncios em paralelo à reprodução do conteúdo antes de pressionar o anúncio, permitindo uma reprodução contínua de anúncios e conteúdo.

* **Reprodução**

   * **Reprodução de conteúdo MP4 -** Os clipes curtos de MP4 não precisam ser retranscodificados para serem reproduzidos no TVSDK.
Observação: A alternância ABR, a reprodução de truques, a inserção de anúncios, a vinculação de áudio tardia e a subsegmentação não são compatíveis com a reprodução MP4.
   * **Trick play com a taxa de bits adaptável (ABR) -** Esse recurso permite que o TVSDK alterne entre fluxos do iFrame no modo de reprodução de truques. Você pode usar perfis que não sejam iFrame para fazer reprodução de truques em velocidades mais baixas.
   * **Peça de truque mais suave -** Essas melhorias aprimoram a experiência do usuário:

          * Seleção adaptável da taxa de bits e da taxa de quadros durante a reprodução do truque, com base na largura de banda e no perfil do buffer
          * Use o fluxo principal em vez do fluxo IDR para obter uma reprodução rápida de até 30 fps.
      
* **Proteção de conteúdo**

   * **Proteção de saída baseada em resolução -** Esse recurso vincula as restrições de reprodução a resoluções específicas, fornecendo controles de DRM mais refinados.

* **Suporte a workflow**

   * **Integração de Faturamento Direto -** Isso envia métricas de faturamento para o back-end do Adobe Analytics, que é certificado pelo Adobe Primetime para fluxos usados pelo cliente.
O TVSDK coleta automaticamente métricas, de acordo com o contrato de vendas do cliente, para gerar relatórios de uso periódicos necessários para fins de faturamento. Em cada evento de início de fluxo, o TVSDK usa a API de inserção de dados do Adobe Analytics para enviar métricas de faturamento, como tipo de conteúdo, sinalizadores ativados para inserção de anúncio e sinalizadores habilitados para drm - com base na duração do fluxo faturável - para o conjunto de relatórios pertencente ao Adobe Analytics Primetime. Isso não interfere ou é incluído nos próprios conjuntos de relatórios ou chamadas de servidor do Adobe Analytics do cliente. Mediante solicitação, esse relatório de uso de faturamento é enviado periodicamente aos clientes. Esta é a primeira fase do recurso de faturamento que suporta somente cobrança de uso. Ele pode ser configurado com base no contrato de vendas usando as APIs descritas na documentação. Esse recurso é ativado por padrão. Para desativar esse recurso, consulte a amostra do reprodutor de referência.
   * **Suporte a Failover Aprimorado -** Estratégias adicionais implementadas para continuar a reprodução ininterrupta, apesar das falhas de servidores de host, arquivos de lista de reprodução e segmentos.

* **Publicidade**

   * **Integração de Moat -** Suporte para medição da visualização de anúncios do Mat.
   * **Banners de companheiro -** Os banners complementares são exibidos ao lado de um anúncio linear e geralmente continuam sendo exibidos na visualização após o fim do anúncio. Esses banners podem ser do tipo html (um trecho de HTML) ou do tipo iframe (um URL para uma página de iframe).

* **Analytics**

   * **VHL 2.0 -** Essa é a integração mais recente da Biblioteca otimizada de pulsações de vídeo (VHL) para coleta automática de dados de uso do Adobe Analytics. A complexidade das APIs foi reduzida para facilitar a implementação. Baixar a biblioteca do VHL [v2.0.0 para Android™](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) e extraia o arquivo JAR na pasta libs.

* **SizeDisponableEventListener**
   * Os métodos getHeight() e getWidth() de SizeAvailableEvent agora retornarão a saída em altura e largura respectivamente. A taxa de proporção de exibição pode ser calculada da seguinte maneira:

      ```
      SizeAvailableEvent e;
      
      DAR = e.getWidth()/ e.getHeight();
      
      Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:
      
      SAR = e.getSarWidth()/e.getSarHeight();
      
      frameHeight = e.getHeight();
      
      frameWidth = e.getWidth()/SAR;    
      ```

* **Cookies**

   * O Android™ TVSDK agora oferece suporte ao acesso a cookies Java™ armazenados no CookieStore do aplicativo Android™. Uma API de retorno de chamada (onCookiesUpdated) é fornecida para gravar sempre que um novo cookie vem como parte do cabeçalho de resposta &quot;Set-Cookie&quot;. Esses cookies estão disponíveis como uma Lista de HttpCookie(s) usada(s) para um URI/domínio diferente(s) ao definir esses valores de cookie nesse URI/domínio específico usando CookieStore. Da mesma forma, os valores de cookie no TVSDK são atualizados usando a API de adição do CookieStore.

## Matriz de recursos {#feature-matrix}

O TVSDK para Android™ é compatível com vários recursos que você pode implementar para adicionar funcionalidade aos seus aplicativos de vídeo.

Nas tabelas de recursos abaixo, um &quot;Y&quot; indica que o recurso é compatível na versão atual.

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Reprodução geral (Reproduzir, Pausar, Buscar) | VOD + Ao vivo | Y |
| FER - Reprodução geral (Reproduzir, Pausar, Buscar) | FER VOD | Y |
| Buscar quando um anúncio está sendo reproduzido | VOD + Ao vivo | Não suportado |
| AC3 | VOD + Ao vivo | Não suportado |
| MP3 | VOD | Não suportado |
| Reprodução de conteúdo MP4 | VOD | Y |
| Lógica de switching da taxa de bits adaptável | VOD + Ao vivo | Y |
| Reprodução Apenas Áudio | VOD + Ao vivo | Y |
| Suporte a vários CDNs | VOD + Ao vivo | Não suportado |
| Reprodução de anúncios com mídia somente de áudio | VOD + Ao vivo | Não suportado |
| Legendas ocultas - 608/708 | VOD + Ao vivo | Y |
| Legendas ocultas - WebVTT | VOD + Ao vivo | Y |
| Failover Manifest | VOD + Ao vivo | Y |
| Failover avançado | VOD + Ao vivo | Y |
| Notificações de QoS e player | VOD + Ao vivo | Y |
| Suporte para cabeçalhos de cookies | VOD + Ao vivo | Y |
| Suporte para cabeçalhos HTTP personalizados | VOD + Ao vivo | Y (lista de permissões necessária) |
| Definir parâmetros de controle de buffer | VOD + Ao vivo | Y |
| Definir controles adaptáveis da taxa de bits | VOD + Ao vivo | Y |
| Tags de manifesto personalizadas | VOD + Ao vivo | Y |
| Vínculo de áudio atrasado | VOD + Ao vivo | Y |
| 302 Redirecionamento | VOD + Ao vivo | Y |
| Reprodução com deslocamento | VOD + Ao vivo | Y |
| Reproduzir somente áudio | VOD + Ao vivo | Y |
| Trick Play | VOD + Ao vivo | Y |
| Movimento lento na reprodução do truque | VOD + Ao vivo | Não suportado |
| Play suave de truques (com ABR) | VOD + Ao vivo | Y |
| Análise do ID3 | VOD + Ao vivo | Y |
| Blecaute de anúncios | VOD + Ao vivo | Não suportado |
| Instantâneo ativado | VOD + Ao vivo | Não suportado |
| Suporte ao marcador de descontinuidade | VOD + Ao vivo | Y |
| 302 Redirecionar adesão | VOD + Ao vivo | Y |

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Reprodução geral, anúncios ativados | VOD + Ao vivo | Y |
| CONSULTE o conteúdo dos anúncios ativados | VOD | Y |
| Comportamentos de publicidade padrão | VOD + Ao vivo | Y |
| VAST 2.0/3.0 | VOD + Ao vivo | Y |
| VMAP 1.0 | VOD + Ao vivo | Y |
| Anúncios MP4 | VOD + Ao vivo | Y (do SIR) |
| Trick Play com anúncios ativados | VOD + Ao vivo | Y |
| Somente publicidade | VOD | Y |
| Parâmetros de direcionamento | VOD + Ao vivo | Y |
| Parâmetros personalizados | VOD + Ao vivo | Y |
| Comportamentos de anúncio personalizados | VOD + Ao vivo | Y |
| Tags de anúncio personalizadas | Ao vivo | Y |
| Resolvedores de anúncios personalizados | VOD + Ao vivo | Y |
| Resolvedor de anúncio personalizado do Freewheel | VOD | Y |
| C3 | VOD + Ao vivo | Não suportado |
| Resolver anúncio lento | VOD | Y |
| Suporte a marcador de descontinuidade - SSAI | VOD + Ao vivo | Y |
| Anúncios complementares, anúncios em banners e anúncios clicáveis | VOD + Ao vivo | Y |
| VPAID 2.0 | VOD + Ao vivo | Y (JS) |
| Saída do anúncio antecipado | Ao vivo | Y |
| Priorização criativa baseada em regras | VOD + Ao vivo | Y |
| Regras CRS | VOD + Ao vivo | Y |
| Resolvedor de anúncios JSON | VOD + Ao vivo | Não suportado |
| Integração de moat | VOD + Ao vivo | Y |

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Criptografia AES | VOD + Ao vivo | Y |
| Criptografia AES de amostra | VOD + Ao vivo | Y |
| Fluxos Tokenized | VOD + Ao vivo | Y |
| DRM | VOD + Ao vivo | Somente DRM do Primetime (Futuro: Widevine) |
| Reprodução externa (RBOP) | VOD + Ao vivo | Somente DRM do Primetime |
| Rotação de licença | VOD + Ao vivo | Somente DRM do Primetime |
| Rotação da Chave | VOD + Ao vivo | Somente DRM do Primetime |

| Recurso | Tipo de conteúdo | HLS |
|---|---|---|
| Integração do Adobe Analytics VHL | VOD + Ao vivo | Y |
| Faturamento | VOD + Ao vivo | Y |

## Problemas resolvidos {#resolved-issues}

Sempre que a resolução estiver associada a um problema reportado, uma referência do Zendesk será exibida, por exemplo, ZD#xxxxx

**Android™ TVSDK 2.7**

Esta seção fornece um resumo do problema resolvido na versão do TVSDK 2.7.

* ZD#37166 - A chamada de rastreamento de erros é acionada mesmo quando o anúncio é reproduzido corretamente.
* ZD#37134 - IDs de anúncio incorretas são retornadas, caso o anúncio wrapper (3P) esteja presente com vários anúncios na resposta VMAP.

**Android™ TVSDK 2.5.6**

* ZD #34992 - O idioma está vazio na legenda oculta.
   * Correção de um caso em que TVSDK não estava analisando #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS do manifesto principal para obter os detalhes de rastreamento da legenda.
* ZD #35078 - Validação de P do Android.
   * O TVSDK 2.5.6 foi validado com as últimas builds beta do Android™ P. Nenhum problema encontrado devido ao novo sistema operacional Android™.
* ZD #34149 - O reprodutor continua a solicitar manifestos mesmo que o erro seja encontrado.
   * Correção do caso em que o TVSDK fazia chamadas repetitivas mesmo quando todos os perfis estavam inativos (erro 404).
* ZD #31533 - Reproduzindo áudio no Android™ após o aplicativo ser enviado para o segundo plano.
   * Adicionado `enableAudioPlaybackInBackground` A API do MediaPlayer, que deve ser chamada com &quot;True&quot; como argumento (quando o player está no estado PREPARED) para habilitar a reprodução de áudio quando o aplicativo está em segundo plano.

**Android™ TVSDK 2.5.5**

* ZD #21647 - Android TVSDK notifica 640x368 quando o tamanho real do vídeo é 640x360.
   * Devido à variável m_nOutputHeight (dentro de AndroidMCVideoDecoder) sendo atualizada com a altura do quadro em vez da altura de saída real. Alterações relevantes na função getVideoFrame para calcular m_nOutputHeight corretamente.
* ZD #26614 - Urgente — serviço de anúncios de terceiros/programático — falha ao fornecer impressões.
   * Aprimoramento da correção anterior, manipulando as letras maiúsculas e minúsculas na análise XML, em que o problema era reproduzível quando o &quot;espaço&quot; estava antes do sinal de &quot;igual&quot;, como &lt;vast version=&quot;2.0&quot;>
* ZD #29296 - Android: Adicione AdSystem e Creative id a solicitações CRS.
   * Agora, incluindo &quot;AdSystem&quot; e &quot;CreativeId&quot; como novos parâmetros nas solicitações 1401 e 1403.
* ZD #33062 - O TVSDK falha na ocorrência de caracteres de barra vertical na resposta VAST no nó CDATA
   * API setEncodeUrlForTracking na classe NetworkConfiguration removida como os caracteres não seguros em um URL a ser codificado.
* ZD #33063 - A lógica de seleção de arquivo CRS foi quebrada - TVSDK não estava enviando solicitação CRS para formato Web, mas enviando-a para arquivos 3gpp.
   * Correção da lógica agora. Ao usar arquivos de mídia com formato webm e 3gpp, a solicitação do CRS é enviada para webm. E ao usar ambos os arquivos de mídia com formato 3gpp, a solicitação do CRS é enviada para o arquivo 3gpp com maior taxa de bits.
* ZD #33125 - O aplicativo Android falha com uma tag DoubleClick específica no VMAP.
   * Correção do cenário para evitar a falha.
* ZD #32256 - Problema de rotação de licença e rotação de chave - Acesso ao Adobe.
   * Correção da inicialização de segmentos com metadados DRM para conteúdo AES de amostra. Funciona bem com conteúdo AES128.
* ZD #33619 - Encaminhamento rápido de um conteúdo de lista de reprodução crescente preso no estado de buffer próximo ao ponto ativo.
   * Manipulado o caso ao atravessar o ponto de entrada em modo de peça.
* ZD #34151 - objetos TimedMetadata fora de ordem.
   * Dois eventos TimedMetadata apareciam em ordem aleatória se pertencessem ao mesmo tempo na linha do tempo. Mantiveram sua ordem original em manifesto.
* ZD #34189 - Problema ao tentar iniciar o ad break.
   * O problema foi com anúncios SSAI que são compilados usando descontinuidade. E a causa era um comportamento quando procuramos o início de tais anúncios, procuramos por um quadro-chave e não o encontramos. O motivo era o carimbo de data e hora do áudio principal do anúncio ser anterior ao carimbo de data e hora do vídeo principal. Portanto, acabamos procurando um quadro principal em um fragmentDump incorreto. Corrigido agora.
* ZD #34528 - Resolução de vídeo não atualizando além de 640x360 no dongle de terceira geração do FireTV.
   * A correção foi aprimorada para incluir as atualizações mais recentes de firmware.
* ZD #34793 - TVSDK 2.5.x usado para travar com o resolvedor de conteúdo personalizado, às vezes, quando o VideoEngine presumia que as auditudeSettings estavam disponíveis e não estavam.
   * A falha ocorria devido a uma chamada de função em um ponteiro compartilhado Nulo (auditudeSettings). Adição de uma verificação condicional em VideoEngineTimeline::placeToSourceTimeline() para garantir que auditudeSettings esteja disponível antes de chamar algo nesse objeto.
* ZD #32584 - Não é possível acessar informações completas presentes no &lt;extensions> nó de uma resposta VAST.
   * Correção do problema em torno da análise XML e agora NetworkAdInfo fornece as informações completas presentes na &lt;extensions> nó .
* ZD #35086 - Não obtendo dados de extensão completos do reprodutor se houver respostas VMAP específicas.
   * O problema era específico para o xml de extensão, pois a análise XML não funcionava se o xml de extensão tivesse aspas duplas no valor do atributo. Correção do problema.

**Android™ TVSDK 2.5.4**

* ZenDesk#33659 - Sessão de reprodução que permite a depuração remota do webview.
   * WebViewDebbuging está definido como Falso por padrão. Para habilitar a depuração, defina como true pelo aplicativo, usando setWebContentsDebuggingEnabled(true).
* ZenDesk#33011 - A linha do tempo do anúncio não será resolvida se houver uma solicitação de CRS com falha.
   * Quando uma solicitação CRS para um anúncio falha, a linha do tempo é resolvida e os anúncios restantes são reproduzidos.
* ZenDesk#34528 - A resolução de vídeo não atualiza além de 640x360 no dongle de terceira geração do FireTV.
   * A resolução do vídeo é alternada como interruptores da taxa de bits.
* ZenDesk#33192 - AudioTrack tem nome nulo quando a faixa é recuperada por meio de AudioUpdatedEventListener::onAudioUpdated.
   * Em alguns cenários no FireTV Stick, o evento onAudioUpdate era disparado quando não havia atualização de áudio. Isso foi corrigido agora.

**Android™ TVSDK 2.5.3**

* Zendesk#32216 - A assinatura de tag personalizada TimedMetadata não está funcionando.
   * Estamos retornando dados ID3 como um array de bytes (para suportar dados APIC ou genéricos) para o cliente, enquanto em uma sequência de caracteres de retorno 1.4. A matriz de bytes não trata o próprio caractere finalizado nulo, portanto, estava mostrando um caractere especial para o cliente. Esse problema foi corrigido agora.
* Zendesk#32670 - Player Not Failing to Redundant Playlist
   * Isso está funcionando bem agora e setNetworkDownCheckUrl está funcionando como esperado.
* Zendesk#32369 - Closed caption mostra lixo ou artefato de cores diferentes.
   * O problema com falhas de CC foi corrigido na build mais recente
* Zendesk#25590 - Aprimoramento: Armazenamento de cookies TVSDK (C++ para Java™)
   * O Android™ TVSDK agora oferece suporte ao acesso de cookies entre a camada Java™ (armazenada no CookieStore do aplicativo Android™) e a camada C++ TVSDK.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 parece não ter a correção para PTPLAY-20269 Esse problema foi corrigido e integrado à ramificação 2.5.2.
* Zendesk#31806 - paus de Auditude no Player PREPARING estava preso no estado Preparando porque o xml de resposta tinha uma tag vazia. Agora o problema foi corrigido.
* Zendesk#31727 - Os caracteres de legenda fechada do TVSDK 2.5 são soltos ou com erro ortográfico.
   * O problema foi corrigido e não soltamos/corrigimos nenhum caractere.
* Zendesk#31485 - DrmManager em 2.5
   * Houve algum problema em Criar DrmManager por meio do novo DrmManager (Contexto). Implementação da classe DRMService que fornecia o DRMManager.
* O fluxo de resolução Zendesk#32794-1080P não está sendo reproduzido no Android™.
   * Alteramos SizeAvailableEvent. Anteriormente, `getHeight()` e `getWidth()` métodos de SizeAvailableEvent em 2.5 usados para retornar a altura e a largura do quadro do quadro, retornados pelo formato de mídia. Agora retorna a altura de saída e a largura de saída respectivamente retornadas pelo decodificador.
* O Flash Player do Zendesk #19359 falha devido à posição do atributo #EXT-X-FAXS-CM no manifesto de nível de conjunto.
   * A tag #EXT-X-FAXS-CM deve sempre aparecer na lista de reprodução superior antes que a taxa de bits individual ou os segmentos sejam exibidos na lista de reprodução.

**Android™ TVSDK 2.5.2**

* Zendesk#17305 Artefatos em legendas ocultas com fundo não opaco.
A propriedade setTreatSpaceAsAlphaNum em TextFormat é exposta. Por padrão, a propriedade é False. Defina a propriedade como True em um cliente para resolver o problema de espaço escuro.

* A tela do Zendesk#25097 CC possui artefatos visuais com configurações CC.
A propriedade setTreatSpaceAsAlphaNum em TextFormat é exposta. Por padrão, a propriedade é False. Defina a propriedade como True em um cliente para resolver o problema de espaço escuro.

* O Zendesk #31620 User agent string que sai do reprodutor TVSDK está truncado.
A sequência de agente do usuário não será mais truncada após 128 caracteres.
A string da versão do Adobe Primetime é adicionada ao agente do usuário do sistema.

* O evento Zendesk #30809 Missing SEEK_END impede que o aplicativo transfira para um estado de reprodução.
* A cor &#39;ciano&#39; da legenda oculta do Zendesk #30415 agora é uma matiz mais escura de azul (turquesa), em comparação com as versões anteriores do Primetime TVSDK.

   A cor é alterada de DarkCyan para Cyan.

* Os anúncios VOD do Zendesk nº 30727 não estão sendo baixados/resolvidos.

   No VMAP XML, se houver uma tag VAST vazia sem uma tag de fechamento explícita (&quot;&lt;/vast>&#39;) e sem um caractere de nova linha depois dele, o XML do VMAP não é analisado corretamente e os anúncios podem não ser reproduzidos.

**Android™ TVSDK 2.5.1**

* Travamento específico do dispositivo (Samsung Galaxy Tab 4); VOD DRM LBA com Auditude e clique nos anúncios.
* VHL - Chamadas de pulsação incorretas são enviadas ao iniciar o conteúdo de um deslocamento.
* Quando anúncios VPAID são reproduzidos, a pulsação do VHL chama o evento:type:o anúncio de reprodução está ausente.
* Depois de entrar no status COMPLETE, o reprodutor volta para o status PLAYING com SKIP adBreakPolicy para anúncios posteriores.
* Os cookies não estão sendo anexados a retornos de chamada de anúncio de saída.
* Os pontos de sinalização dos anúncios não estão visíveis.
* O HLS com uma faixa EAC3 SAP separada não será carregado.
* O reprodutor falha enquanto o TVSDK recebe uma Tela On intent (Ativada) depois que o reprodutor de mídia é restaurado.

## Problemas conhecidos e limitações {#known-issues-and-limitations}

**Android™ TVSDK 2.7**

* O TVSDK 2.7 oferece suporte à resolução simultânea de até cinco anúncios.
* No caso de uma resposta VMAP, as chamadas de anúncio em um único Ad break são simultâneas, e as quebras de anúncio são resolvidas sequencialmente.
* No caso de um FER, as chamadas de anúncio em cada oportunidade são resolvidas simultaneamente.

### Problemas conhecidos e limitações das versões anteriores{#known-issues-limitations-previous-releases}

**Android™ TVSDK 2.5.6**

* Várias quebras de anúncios VMAP ao mesmo tempo não são compatíveis.

**Android™ TVSDK 2.5.3**

Esta versão tem os seguintes problemas:

* A reprodução de vídeo ao vivo pode ter problemas de sincronização de áudio-vídeo em dispositivos de baixa definição ou condições de rede inadequadas.
* Para fluxos FER, virtualTime e localTime podem ser diferentes. Também FER com deslocamento não funciona.
* A reprodução pode ficar travada quando o conteúdo de áudio de vinculação tardia for buscado.
* Intermitentemente, as legendas da WebVTT podem ficar fora de sincronia para o conteúdo LIVE.
* Intermitentemente, uma reprodução rápida de alguns quadros pode ser vista após sair de um ad break.
* Às vezes, o erro 303 é lançado para o Triple Wrapper Ad Breaks (Quebras de anúncios de invólucro triplas), mesmo quando os anúncios são reproduzidos.

**Android™ TVSDK 2.5.2**

Esta versão tem os seguintes problemas:

* A reprodução de vídeo ao vivo pode ter problemas de sincronização de áudio-vídeo em dispositivos de baixa definição.
* A reprodução pode ser interrompida às vezes em que a busca é realizada até o fim da mídia VOD.
* Para fluxos FER, virtualTime e localTime podem ser diferentes. Além disso, FER com deslocamento não funciona.

**Android™ TVSDK 2.5.1**

Essa versão do TVSDK apresenta os seguintes problemas:

* A reprodução de vídeo ao vivo pode ter problemas de sincronização de áudio-vídeo em dispositivos de baixa definição.
* Para fluxos FER, virtualTime e localTime podem ser diferentes. Além disso, FER com deslocamento não funciona.
* No XML VMAP, se houver uma tag VAST vazia sem uma tag de fechamento explícita (&lt;/vast>) e sem uma nova linha depois, o XML do VMAP não é analisado corretamente e os anúncios podem não ser reproduzidos.
* Não há suporte para VPAID posterior à exibição.

## Recursos úteis {#helpful-resources}

* [Requisitos do sistema](https://experienceleague.adobe.com/docs/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2.7-requirements.html?lang=en)
* [Guia do programador TVSDK 2.7 para Android™](https://experienceleague.adobe.com/docs/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2.7-overview-prod-audience-guide.html?lang=en)
* [TVSDK Android™ Javadoc para referência de API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html)
* [Documento da API TVSDK Android™ C++](https://help.adobe.com/en_US/primetime/api/psdk/cpp/namespaces.html) - Cada classe Java™ tem uma classe C++ correspondente e a documentação C++ contém mais material explicativo do que os documentos Java™, portanto, consulte a documentação C++ para obter uma compreensão mais profunda da API Java™.
* [TVSDK 1.4 para 2.5 para Guia de migração do Android™ (Java™)](https://experienceleague.adobe.com/docs/primetime/migration/tvsdk-14-25-android.html?lang=en)
* Para lidar com cenários de ativação/desativação da tela, consulte a seção `Application_Changes_for_Screen_On_Off.pdf` arquivo incluído na build.
* Consulte a documentação completa de ajuda em [Aprendizagem e suporte do Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
