---
title: Notas de versão do PTAI 19.11.1
description: As notas de versão do PTAI 19.11.1 descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos no Primetime Ad Insertion no ano de 2019.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 0%

---

# Notas de versão do Primetime Ad Insertion 19.11.1

As notas de versão do Primetime Ad Insertion 19.11.1 descrevem o que é novo ou alterado, problemas resolvidos e problemas conhecidos no Primetime Ad Insertion no ano de 2019.

## Novidades na PTAI 19.11.1

**Quando:** Segunda-feira, 4 de novembro de 2019 às 12h01 às 13h00 LESTE

Atualizações de manutenção do.

## O que mudou em versões anteriores

### Versão 19.10.2

**Quando:** Quinta-feira, 31 de outubro de 2019 das 01:00 às 03:00 Leste

Atualizações de manutenção do.

### Versão 19.10.1

**Quando:**  Terça-feira, 22 de outubro às 01:00 às 02:00 LESTE

Atualizações de manutenção do.

### Versão 19.9.1

**Quando:** Terça-feira, 10 de setembro de 2019 às 12h30 às 2h Horário do Leste

Atualizações de segurança

### Versão 19.8.3

**Quando:** Quarta-feira, 28 de agosto de 2019, 12:30 - 01:30 AM LESTE

Correção de um erro em que os reprodutores do Chromecast saíam inesperadamente da reprodução quando os segmentos de anúncio eram implantados fora da janela do DVR.

### Versão 19.8.2

**Quando:** Quarta-feira, 21 de agosto de 2019 2:00 às 3:00 Horário do Leste

* Painel SAI: Seção de estatísticas da sessão. Você pode exportar os eventos de sessão por meio da opção Baixar CSV.

* Atualizações de manutenção

### Versão 19.8.1

**Quando:** Terça-feira, 6 de agosto de 2019 2h30 Horário do Leste até Terça-feira, 6 de agosto de 2019 4h30 Horário do Leste

* Painel SSAI: Nova seção adicionada, Estatísticas da sessão, ao Painel SSAI
   * Se você tiver a ID de sessão para uma sessão SSAI que tinha o modo de depuração ativado (ptdebug=true), será possível pesquisar a seguinte atividade que ocorreu nessa sessão:
      * Adicionar solicitações/respostas
      * Anúncios inseridos
      * Sinais disparados (somente rastreamento do lado do servidor)

   * Você pode pesquisar atividades de uma ID de sessão específica até 30 dias após a realização da sessão SAI
   * Você pode exportar os eventos
* Banco de dados: atualizações de segurança

### Versão 19.7.1

**Quando:** Quarta-feira, 10 de julho

* SSAI: Para valores ptcueformat que oferecem suporte à sinalização de ad break EXT-X-CUE-OUT em fluxos ao vivo, foi adicionada uma macro genérica para transmitir dados de atributos na tag EXT-X-ASSET Exemplo: Tag que acompanha a tag #EXT-X-CUE-OUT: #EXT-X-ASSET:CAID=75BCD15,GENRE=News,Program=NewsAt10 Macros: # pode ser usado para transmitir notícias (do atributo GENRE) para uma URL de chamada de anúncio # pode ser usado para transmitir notíciasAt10 (do atributo Programa) para uma URL de chamada de anúncio Exceção: For compatibilidade com wards, # e # têm a mesma funcionalidade. Ambas as macros podem ser usadas para passar o valor do atributo CAID, após converter o valor de hex para long. O valor longo é 123456789 para o valor hex, 75BCD15, no exemplo acima. Ambas as macros seriam usadas para passar 123456789 para um URL de chamada de anúncio. A macro sempre começa com #. A macro diferencia maiúsculas de minúsculas, mas o atributo na tag EXT-X-ASSET não. Ou seja, PROGRAMA e Programa são permitidos na tag EXT-X-ASSET
* SSAI: Alterações de configuração de um cliente específico para o seguinte:
   * Duração da janela deslizante (lista de reprodução ao vivo) de quatro minutos
   * Se uma exceção de tempo limite de soquete for acionada quando o Servidor de manifesto buscar o conteúdo de origem, o Servidor de manifesto retornará o código de resposta HTTP (404) em vez de 500
* Atualizações de segurança

### Versão 19.6.1

**Quando:** Quarta-feira, 12 de junho de 2019 11h30 PST para quinta-feira, 13 de junho de 2019 12h30 PST

* CRS: Regra de normalização para criações de RevJet
   * Adição da regra de normalização da URL criativa para RevJet, usada pelo CRS e SSAI
   * TVSDK: se você fornecer ou planejar fornecer anúncios da RevJet, as regras de normalização precisarão ser adicionadas ao JSON de regras do CRS para usar o CRS com seus criadores. Entre em contato com seu Gerente técnico de conta para obter assistência
* CRS: Regra de normalização para criativos do Innovid
   * Adição da regra de normalização do URL criativo para o Innovid, usada pelo SSAI
   * A regra de normalização usada pelo CRS foi adicionada em uma versão anterior
   * TVSDK: a regra de normalização para adicionar às Regras CRS JSON foi fornecida após um lançamento anterior, mas, para ter segurança, entre em contato com seu Gerente técnico de conta para revisar todas as regras de normalização existentes.
     >[!NOTE]
     >
     >A maioria dos URLs criativos da Innovid será transcodificada e compilada com êxito sem a regra de normalização. Ocasionalmente, no entanto, URLs criativos da Innovid com parâmetros dinâmicos são encontrados. A regra de normalização é necessária para lidar com essas instâncias.

### Versão 19.5.2

**Quando:** Quarta-feira, maio 22:30 Horário do Leste até Quarta-feira, maio 22 4:30 Horário do Leste

* Suporte adicionado para CMAF (conteúdo HLS/fMP4)
   * SSAI: Manipular manifestos CMAF
   * SSAI: inicie solicitações de transcodificação e recupere ativos do CRS dependendo do formato de conteúdo (HLS/ts e HLS/fMP4)
   * CRS: Fluxo de trabalho adicionado para reempacotar leituras no formato CMAF (HLS/fMP4)
* SSAI: correção de um problema que impedia a inserção de anúncios não muxados em conteúdo não muxado, quando o conteúdo e o anúncio não tinham fluxos somente de áudio (EXT-X-STREAM-INF)
* SSAI: adição de suporte para tokens de autenticação CDN do Limelight (LLNW) para segmentos de conteúdo
   * Quando `pttoken=limelight` ou `pttoken=llnw` for adicionado ao URL de inicialização, adicionaremos um cabeçalho secreto ao recuperar a lista de reprodução mestre de origem e anexaremos os parâmetros de consulta do cabeçalho X-Adobe-Sig do LLNW aos segmentos de conteúdo
* SSAI: Adição de outro valor de pttoken (`pttoken=centurylink`) para suporte ao token de autenticação CDN do CenturyLink, lançado em 30 de julho de 2018
   * `pttoken=centurylink` tem o mesmo comportamento que `pttoken=level3`, e ambos os valores são válidos

### Versão 19.5.1

**Quando:** Quinta-feira, maio 9 2:30 Horário do Leste até Quinta-feira, maio 9 4:30 Horário do Leste

* SSAI: Atualizações de segurança
* Painel CRS: Truncado a string &quot;FqAdId Sample&quot; para 255 caracteres devido a restrições de armazenamento de dados (8 bits)
   * A string &quot;FqAdId Sample&quot; inclui o Sistema de publicidade e a ID de publicidade de cada resposta XML na cadeia de invólucro do anúncio para inserções de todos os anúncios CRS com SSAI (seção Estatísticas criativas do painel CRS)
* Painéis SSAI e CRS: Atualizações de versão de software

### Versão 19.4.1

**Quando:** Quarta-feira, abril 10 2:30 Horário do Leste até Quarta-feira, abril 10 4:30 Horário do Leste

* CRS: A API de reempacotamento do CRS não oferecerá mais suporte a comandos POST HTTP. A API de reempacotamento do CRS redirecionará automaticamente (301) comandos HTTP POST para HTTPS
   * A partir de 20 de maio, o redirecionamento HTTP->HTTPS para comandos HTTP POST será desativado
   * Se você usar a API de reempacotamento do CRS para reempacotar anúncios com antecedência, alterne seus comandos POST para HTTPS até 20 de maio
* CRS: reprojetou a arquitetura e o fluxo de trabalho para fazer upload de ativos CRS para as origens de CDN dos clientes
   * Os processos de trabalho por origem de CDN são separados, portanto, os gargalos de upload para uma origem de CDN não afetarão os uploads para outras origens de CDN
   * Outros benefícios: os tempos de processamento de trabalho dos CRS e as taxas de upload para as origens de CDN dos clientes são aprimorados
* SSAI: Adição de URLs ClickThrough e ClickTracking para anúncios de vídeo no formato JSON v2 do sidecar
   * Uma nova propriedade de matriz JSON, &quot;videoClicks&quot;, seguirá a propriedade &quot;trackingURLs&quot;
   * Os nomes dos valores de &quot;evento&quot; serão &quot;clickThrough&quot; e &quot;clickTracking&quot; e não terão um valor de startTime
* SSAI: Para ativos CRS, adição de funcionalidade para estender a expiração do registro de pesquisa de um ativo CRS por 30 dias sempre que ele for inserido
   * Comportamento anterior: os registros de pesquisa de ativos do CRS são armazenados no memcache em cada pod. Os registros de pesquisa de ativo CRS são removidos automaticamente 30 dias após serem adicionados ao memcache. Para preencher novamente o registro de pesquisa de ativos CRS de um criativo em um pod após sua remoção do memcache, esse criativo precisa ser encontrado três vezes nesse pod
   * Novo comportamento: quando um pod acessa um registro de pesquisa de ativo do CRS para inserir o ativo do CRS, a expiração do registro de pesquisa de ativo do CRS é estendida em 30 dias nesse pod. Como resultado, os ativos do CRS usados com frequência não serão removidos do memcache de um pod até 30 dias depois de seu uso mais recente
   * O novo comportamento é válido em todo o sistema e pode ser desativado se for detectada uma queda no desempenho
* SSAI: comportamento de manipulação de manifesto WebVTT atualizado somente para fluxos ao vivo
   * Comportamento anterior: somente no manifesto WebVTT, remova as tags EXT-X-DISCONTINUITY que seriam inseridas antes de cada anúncio inserido e depois do último segmento do ad break inserido
   * Novo comportamento: adição de um novo parâmetro, vttdisc, com valores aceitos de true e false, ao URL de inicialização do SSAI
      * vttdisc=true: as tags EXT-X-DISCONTINUITY serão inseridas no manifesto WebVTT antes de cada anúncio inserido e após o último segmento do ad break inserido, correspondendo ao comportamento para áudio/vídeo e manifestos somente de áudio
      * vttdisc=false (igual ao comportamento anterior): somente no manifesto WebVTT, remova as tags EXT-X-DISCONTINUITY que seriam inseridas antes de cada anúncio inserido e depois do último segmento do ad break inserido
      * Se o parâmetro vttdisc for omitido ou tiver um valor diferente de true/false, o padrão de vttdisc será true
* SSAI: Atualizações de segurança e de versão de software
   * Java: versão atualizada do Java para oferecer suporte a conjuntos de cifras adicionais para chamadas de anúncio acionadas por TLS 1.2 (HTTPS)

### Versão 19.2.1

**Quando:** Quarta-feira, 20 de fevereiro de 2019 1:30 Horário do Leste até Quarta-feira, 20 de fevereiro de 2019 3:30 Horário do Leste

* SSAI: Adição de URLs ClickThrough e ClickTracking para anúncios de vídeo no formato JSON v2 do sidecar
   * Na propriedade &quot;trackingURLs&quot;, os nomes dos valores do &quot;evento&quot; serão &quot;clickthrough&quot; e &quot;clickTracking&quot;
   * Os valores startTime serão o início do anúncio
* SSAI: Para ativos CRS, adição de funcionalidade para estender a expiração do registro de pesquisa de um ativo CRS por 30 dias sempre que ele for inserido
   * Comportamento anterior: os registros de pesquisa de ativos do CRS são armazenados no memcache em cada pod. Os registros de pesquisa de ativo CRS são removidos automaticamente 30 dias após serem adicionados ao memcache. Para preencher novamente o registro de pesquisa de ativos CRS de um criativo em um pod após sua remoção do memcache, esse criativo precisa ser encontrado três vezes nesse pod
   * Novo comportamento: quando um pod acessa um registro de pesquisa de ativo do CRS para inserir o ativo do CRS, a expiração do registro de pesquisa de ativo do CRS é estendida em 30 dias nesse pod. Como resultado, os ativos do CRS usados com frequência não serão removidos do memcache de um pod até 30 dias depois de seu uso mais recente
   * O novo comportamento é válido em todo o sistema e pode ser desativado se for detectada uma queda no desempenho

* SSAI: Atualizações de versão de software para NGINX e Kafka
   * O NGINX e o Kafka são usados para acionar URLs de rastreamento de anúncios no lado do servidor e enviar dados para os painéis SSAI e CRS
* CRS: Melhorias de desempenho no painel CRS

### Versão da interface do usuário da Web

**Quando:** Quarta-feira, 13 de fevereiro, 4:00 - 4:30 Pacífico

**O que:** Componente da interface do usuário da Web do Primetime e Decisioning

* Correção do problema de interface do usuário do calendário em que o usuário não podia selecionar uma data além de 31 de dezembro de 2018 no componente do calendário enquanto traficava uma campanha ou obtinha um relatório.

### Versão 19.1.2

**Quando:** Quarta-feira, 30 de janeiro de 2019 1:30 Horário do Leste até Quarta-feira, 30 de janeiro 3:30 Horário do Leste

* SSAI: atualização da estrutura da chave de pesquisa que o SSAI usa para armazenar e recuperar ativos CRS, a fim de lidar com cenários em que os provedores de anúncios têm uma ID de anúncio dinâmica ou ID de criação para o mesmo anúncio
   * Nova estrutura de chave de pesquisa: Zona, URL de criação e parâmetros de formato (duração de destino, formato de saída, CDN de destino)
   * Estrutura antiga da chave de pesquisa: Zona, Sistema de publicidade, ID do anúncio, ID criativa, URL de criação e parâmetros de formato (duração do destino, formato de saída, CDN de destino)
   * As chaves de pesquisa para ativos CRS existentes serão atualizadas para corresponder à nova estrutura antes da versão de produção, mas observe que novos ativos transcodificados entre a atualização de chaves de pesquisa e a versão de produção podem ser perdidos. Em caso afirmativo, eles iniciariam uma nova solicitação de CRS na próxima vez que forem encontrados após o lançamento

* CRS: adição da capacidade de lista de bloqueios/lista de permissões solicitações de CRS de sistemas de anúncios específicos, IDs de anúncio, IDs criativas, URLs criativas e/ou formato criativo

  >Nota
  >
  >O Adobe adicionará regras de lista de bloqueios quando provedores de anúncios com valores dinâmicos (por exemplo, parâmetro dinâmico em URL) para o mesmo anúncio forem encontrados. Essas regras de lista de bloqueios serão desativadas após a resolução do componente dinâmico, pelo provedor ou por meio de uma regra de normalização.

   * Se quiser adicionar uma regra de lista de bloqueios ou lista de permissões para sua zona, entre em contato com o Gerente técnico de conta para obter assistência.

### Versão 19.1.1

**Quando:** Quarta-feira, 9 de janeiro de 2019 1:30 Horário do Leste até Quarta-feira, 9 de janeiro 3:30 Horário do Leste

* Correção de um problema em que uma interpretação incorreta de cabeçalhos HTTP keep-alive pode resultar em um erro ao validar ativos de criação de entrada hospedados em total-stream.net.
* Correção de um problema em que aspas simples (&#39;) e aspas duplas (&quot;) na ID do anúncio, ID criativa e outros campos para uma solicitação de reempacotamento fazem com que a solicitação de reempacotamento falhe.
* Alternado para Java long (tipo de dados) para solucionar um problema em que atingir o limite de int do Java de 2.147.483.647 em valores de ID de trabalho de transcodificação causaria a falha de todas as solicitações de reempacotamento.
* Otimizações de banco de dados.

## Problemas resolvidos

Quando a resolução está associada a um problema relatado, uma referência do Zendesk é exibida. Por exemplo, ZD#xxxxx.

**PTAI 19.7.1**

ZD#37503 - As respostas Json para as regras CRS são armazenadas em cache para evitar as solicitações duplicadas.

## Problemas conhecidos e limitações

**PTAI 19.7.1**

Nenhuma limitação nova adicionada.
