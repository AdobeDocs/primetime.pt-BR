---
title: Notas de versão do PTAI 19.11.1
description: As notas de versão do PTAI 19.11.1 descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos no Primetime Dynamic Ad Insertion em 2019.
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1968'
ht-degree: 0%

---


# Notas de versão do Primetime Dynamic Ad Insertion 19.11.1

As notas de versão do Dynamic Ad Insertion 19.11.1 descrevem o que é novo ou alterado, os problemas resolvidos e os problemas conhecidos no Primetime Dynamic Ad Insertion no ano de 2019.

## Novidades do PTAI 19.11.1

**Quando:** segunda-feira, 4 de novembro de 2019, às 12:01 da manhã às 01:00 da manhã no leste

Atualizações de manutenção.

## O que mudou em versões anteriores

### Versão 19.10.2

**Quando:** quinta-feira, 31 de outubro de 2019, das 01h00 às 03h00 do leste

Atualizações de manutenção.

### Versão 19.10.1

**Quando:**  Terça-feira, 22 de outubro às 01h00 às 02h00 do ORIENTE

Atualizações de manutenção.

### Versão 19.9.1

**Quando:** terça-feira, 10 de setembro de 2019 às 12:30 às 14:00 Hora do Leste

Atualizações de segurança

### Versão 19.8.3

**Quando:** quarta-feira, 28 de agosto de 2019, 12:30 - 01:30

Correção de um bug no qual os players do Chromecast saíam inesperadamente da reprodução quando os segmentos do anúncio eram lançados para fora da janela do DVR.

### Versão 19.8.2

**Quando:** quarta-feira, 21 de agosto de 2019 2:00 às 3:00 Hora do Leste

* Painel SSAI: Seção Estatísticas da sessão. É possível exportar os eventos de sessão por meio da opção Baixar CSV.

* Atualizações de manutenção

### Versão 19.8.1

**Quando:** terça-feira, 6 de agosto de 2019, 2:30, horário do leste até terça-feira, 6 de agosto de 2019, 4:30, horário do leste

* Painel SSAI: Adicionada nova seção, Estatísticas da sessão, ao Painel SSAI
   * Se você tiver a ID da sessão para uma sessão SSAI que teve o modo de depuração ativado (ptdebug=true), poderá procurar a seguinte atividade que ocorreu nessa sessão:
      * Solicitações/respostas de anúncio
      * Anúncios inseridos
      * Beacons ligados (somente rastreamento do lado do servidor)
   * Você pode pesquisar a atividade de uma ID de sessão específica até 30 dias após a sessão SSAI ter ocorrido
   * É possível exportar os eventos
* Banco de dados: Atualizações de segurança

### Versão 19.7.1

**Quando:** quarta-feira, 10 de julho

* SSAI: Para valores de formato de canal que suportam a sinalização EXT-X-CUE-OUT e break em fluxos ao vivo, adicionou uma macro genérica para transmitir dados de atributos na tag EXT-X-ASSET Exemplo: Tag que acompanha a tag #EXT-X-CUE-OUT: #EXT-X-ASSET:CAID=75BCD15,GENRE=Notícias,Programa=NotíciasAt10 Macros: # pode ser usado para passar Notícias (do atributo GENRE) para um URL de chamada de anúncio # pode ser usado para passar NewsAt10 (do atributo do Programa) para uma Exceção de URL de chamada de anúncio: Para compatibilidade com versões anteriores, # e # têm a mesma funcionalidade. Ambas as macros podem ser usadas para passar o valor do atributo CAID, após converter o valor de hex para long O valor long é 123456789 para o valor hex, 75BCD15, no exemplo acima. Ambas as macros seriam usadas para passar 123456789 para um URL de chamada de anúncio A macro sempre start com #. A macro faz distinção entre maiúsculas e minúsculas, mas o atributo na tag EXT-X-ASSET não. Ou seja, PROGRAMA e Programa são permitidos na tag EXT-X-ASSET
* SSAI: Alterações de configuração para um cliente específico para o seguinte:
   * Duração da janela deslizante (lista de reprodução dinâmica) de quatro minutos
   * Se uma exceção de tempo limite de soquete for emitida quando o Manifest Server buscar o conteúdo de origem, o Manifest Server retornará o código de resposta HTTP (404) em vez de 500
* Atualizações de segurança

### Versão 19.6.1

**Quando:** quarta-feira, 12 de junho de 2019 23:30 PST para quinta-feira, 13 de junho de 2019 12:30 PST

* SIR: Regra de normalização para criativos da RevJet
   * Adicionada a regra de normalização de URL criativo para RevJet, usada por CRS e SSAI
   * TVSDK: Se você serve ou planeja veicular anúncios da RevJet, as regras de normalização terão de ser adicionadas às Regras do SIR JSON para que possam utilizar o SIR com os seus criativos. Entre em contato com seu Gerente de conta técnico para obter assistência
* SIR: Regra de normalização para criativos de Innovid
   * Adicionada a regra de normalização de URL criativo para Innovid, usada pelo SSAI
   * A regra de normalização utilizada pelo SIR foi adicionada numa versão anterior
   * TVSDK: A regra de normalização a ser adicionada nas Regras CRS JSON foi fornecida após uma versão anterior, mas para ser segura, fale com seu Gerente de conta técnico para revisar todas as regras de normalização que você possui.
      >[!NOTE]
      >
      >A maioria dos URLs criativos incólidos serão transcodificados e costurados com êxito sem a regra de normalização. Ocasionalmente, porém, URLs criativos com parâmetros dinâmicos são encontrados. A regra de normalização é necessária para lidar com essas instâncias.

### Versão 19.5.2

**Quando:** quarta-feira, 22 de maio, 22:30, horário do leste até quarta-feira, 22 de maio, 4:30, horário do leste

* Adicionado suporte para CMAF (conteúdo HLS/fMP4)
   * SSAI: Gerenciar manifestos CMAF
   * SSAI: Iniciar solicitações de transcodificação e recuperar ativos CRS dependendo do formato de conteúdo (HLS/ts e HLS/fMP4)
   * SIR: Fluxo de trabalho adicionado para reempacotar anúncios no formato CMAF (HLS/fMP4)
* SSAI: Correção de um problema que impedia a inserção de publicidades sem toque no conteúdo sem muxo, quando o conteúdo e o anúncio não tinham fluxos somente de áudio (EXT-X-STREAM-INF)
* SSAI: Adicionado suporte para tokens de autenticação CDN do Limelight (LLNW) para segmentos de conteúdo
   * Quando `pttoken=limelight` ou `pttoken=llnw` for adicionado ao URL de inicialização, adicionaremos um cabeçalho secreto ao recuperar a lista de reprodução mestre de origem, então anexaremos os parâmetros do query do cabeçalho X-Adobe-Sig da LLNW aos segmentos de conteúdo
* SSAI: Adicionado outro valor de token (`pttoken=centurylink`) para suporte a token de autenticação CenturyLink CDN, lançado em 30 de julho de 2018
   * `pttoken=centurylink` tem o mesmo comportamento `pttoken=level3`e ambos os valores são válidos

### Versão 19.5.1

**Quando:** quinta-feira, 9 de maio, 02:30, horário do leste até quinta-feira, 9 de maio, 4:30, horário do leste

* SSAI: Atualizações de segurança
* Painel CRS: Truncado a sequência &quot;Amostra de FqAdId&quot; para 255 caracteres devido a restrições de armazenamento de dados (8 bits)
   * A sequência de caracteres &quot;Amostra de FqAdId&quot; inclui o Sistema de anúncio e a ID de anúncio de cada resposta XML na cadeia de invólucro do anúncio para inserções de todos os anúncios de CRS com SSAI (seção Estatísticas criativas do Painel CRS)
* Painéis SSAI e CRS: Atualizações de versão de software

### Versão 19.4.1

**Quando:** quarta-feira, 10 de abril, 2:30, horário do leste até quarta-feira, 10 de abril, 4:30, horário do leste

* SIR: A API de reempacotamento do CRS não oferecerá mais suporte aos comandos HTTP POST. A API de reempacotamento do CRS redirecionará automaticamente os comandos HTTP POST (301) para HTTPS
   * A partir de 20 de maio, o redirecionamento HTTP->HTTPS para comandos HTTP POST será desativado
   * Se você usar a CRS Reempacotando API para reempacotar anúncios antecipadamente, mude seus comandos POST para HTTPS até 20 de maio
* SIR: Reprojetou a arquitetura e o fluxo de trabalho para fazer upload dos ativos CRS para as origens CDN dos clientes
   * Os processos de trabalho por origem CDN são separados, portanto, os gargalos de upload de uma origem CDN não afetarão os uploads para outras origens CDN
   * Outras prestações: O tempo de processamento de tarefas do CRS e as taxas de carregamento para as origens CDN dos clientes foram aprimorados
* SSAI: Adicionados os URLs ClickThrough e ClickTracking para anúncios de vídeo ao formato JSON v2 auxiliar
   * Uma nova propriedade de matriz JSON, &quot;videoClicks&quot;, seguirá a propriedade &quot;trackingURLs&quot;
   * Os nomes de valor &quot;evento&quot; serão &quot;clickThrough&quot; e &quot;clickTracking&quot;, e não terão um valor startTime
* SSAI: Para os ativos CRS, adição de funcionalidade para estender a expiração do registro de pesquisa de um ativo CRS por 30 dias sempre que for inserido
   * Comportamento anterior: Os registros de pesquisa de ativos do CRS são armazenados no cache de memória em cada pod. Os registros de pesquisa de ativos CRS são removidos automaticamente 30 dias após serem adicionados ao cache de memória. Para repreencher o registro de pesquisa de ativos CRS de um anúncio em um pod depois de removê-lo do cache de memória, esse anúncio precisa ser encontrado 3 vezes nesse pod
   * Novo comportamento: Quando um pod acessa um registro de pesquisa de ativos do CRS para inserir o ativo do CRS, a expiração do registro de pesquisa de ativos do CRS será estendida em 30 dias nesse pod. Como resultado, os ativos CRS que são usados com frequência não serão removidos do cache de memória de um pod até 30 dias após sua última utilização
   * O novo comportamento é do sistema inteiro e pode ser desativado se uma queda de desempenho for detectada
* SSAI: Comportamento de manipulação de manifesto WebVTT atualizado somente para fluxos ao vivo
   * Comportamento anterior: Somente no manifesto WebVTT, remova as tags EXT-X-DISCONTINUITY que seriam inseridas antes de cada anúncio inserido e depois do último segmento do intervalo de anúncio inserido
   * Novo comportamento: Adicionado um novo parâmetro, vttdisc, com valores aceitos como true e false, ao URL de inicialização do SSAI
      * vttdisc=true: As tags EXT-X-DISCONTINUITY serão inseridas no manifesto WebVTT antes de cada anúncio inserido e depois do último segmento da quebra de anúncio inserida, correspondendo ao comportamento dos manifestos somente de áudio/vídeo e áudio
      * vttdisc=false (o mesmo que o comportamento anterior): Somente no manifesto WebVTT, remova as tags EXT-X-DISCONTINUITY que seriam inseridas antes de cada anúncio inserido e depois do último segmento do intervalo de anúncio inserido
      * Se o parâmetro vttdisc for omitido ou tiver um valor diferente de true/false, o padrão vttdisc será true
* SSAI: Atualizações de segurança e atualizações de versão de software
   * Java: Atualização da versão Java para oferecer suporte a conjuntos de cifras adicionais para chamadas de anúncio lançadas por TLS 1.2 (HTTPS)

### Versão 19.2.1

**Quando:** quarta-feira, 20 de fevereiro de 2019 13:30 Hora do Leste para quarta-feira, 20 de fevereiro de 2019 3:30 Hora do Leste

* SSAI: Adicionados os URLs ClickThrough e ClickTracking para anúncios de vídeo ao formato JSON v2 auxiliar
   * Na propriedade &quot;trackingURLs&quot;, os nomes de valores de &quot;evento&quot; serão &quot;clickthrough&quot; e &quot;clickTracking&quot;
   * Seus valores startTime serão o início do anúncio
* SSAI: Para os ativos CRS, adição de funcionalidade para estender a expiração do registro de pesquisa de um ativo CRS por 30 dias sempre que for inserido
   * Comportamento anterior: Os registros de pesquisa de ativos do CRS são armazenados no cache de memória em cada pod. Os registros de pesquisa de ativos CRS são removidos automaticamente 30 dias após serem adicionados ao cache de memória. Para repreencher o registro de pesquisa de ativos CRS de um anúncio em um pod depois de removê-lo do cache de memória, esse anúncio precisa ser encontrado 3 vezes nesse pod
   * Novo comportamento: Quando um pod acessa um registro de pesquisa de ativos do CRS para inserir o ativo do CRS, a expiração do registro de pesquisa de ativos do CRS será estendida em 30 dias nesse pod. Como resultado, os ativos CRS que são usados com frequência não serão removidos do cache de memória de um pod até 30 dias após sua última utilização
   * O novo comportamento é do sistema inteiro e pode ser desativado se uma queda de desempenho for detectada

* SSAI: Atualizações de versão de software para NGINX e Kafka
   * NGINX e Kafka são usados para acionar e rastrear URLs do lado do servidor e enviar dados para os Painéis SSAI e CRS
* SIR: Melhorias no desempenho do Painel CRS

### Versão da interface do usuário da Web

**Quando:** quarta-feira, 13 de fevereiro, 4:00 - 4:30 AM Pacífico

**O que:** Componente da interface do usuário da Web do Primetime e de decisão

* Correção do problema da interface do usuário do calendário em que o usuário não pôde selecionar uma data além de 31 de dezembro de 2018 no componente do calendário ao traçar uma campanha ou extrair um relatório.

### Versão 19.1.2

**Quando:** quarta-feira, 30 de janeiro de 2019 13:30 Hora do leste até quarta-feira, 30 de janeiro 30:30 Hora do leste

* SSAI: Atualização da estrutura da chave de pesquisa que a SSAI usa para armazenar e recuperar ativos CRS, a fim de lidar com situações nas quais os provedores de anúncios têm uma ID de anúncio dinâmica ou uma ID criativa para o mesmo anúncio
   * Nova estrutura de chave de pesquisa: Zona, URL criativo e parâmetros de formato (duração do público alvo, formato de saída, CDN de destino)
   * Estrutura antiga da chave de pesquisa: Zona, Sistema de publicidade, ID de anúncio, ID criativa, URL criativo e parâmetros de formato (duração do público alvo, formato de saída, CDN de destino)
   * As chaves de pesquisa dos ativos CRS existentes serão atualizadas para corresponder à nova estrutura antes da versão de produção, mas observe que novos ativos transcodificados entre a atualização das chaves de pesquisa e a versão de produção podem ser perdidos. Em caso afirmativo, iniciarão uma nova solicitação de SIR na próxima vez que forem encontrados após a versão

* SIR: Adicionada a capacidade de bloquear/permitir solicitações CRS de sistemas de anúncios específicos, IDs de anúncios, IDs criativas, URLs criativos e/ou formato criativo

   >Nota
   >
   >A Adobe adicionará regras de lista de bloqueio quando os provedores de publicidade com valores dinâmicos (por exemplo, parâmetro dinâmico em URL) para o mesmo anúncio forem encontrados. Essas regras de lista de bloqueio serão desativadas depois que o componente dinâmico for resolvido, pelo provedor ou por meio de uma regra de normalização.

   * Se você quiser adicionar uma lista de bloqueios ou uma regra de lista de permissões para sua região, fale com seu Gerente de conta técnico para obter assistência.

### Versão 19.1.1

**Quando:** quarta-feira, 9 de janeiro de 2019 13:30 Hora do leste até quarta-feira, 9 de janeiro, 3:30 Hora do leste

* Correção de um problema em que a interpretação incorreta de cabeçalhos HTTP keep-live pode resultar em um erro ao validar ativos criativos de entrada hospedados no total-stream.net.
* Correção de um problema em que aspas simples (&#39;) e aspas de duplo (&quot;) na ID da publicidade, na ID da criação e em outros campos de uma solicitação de reempacotamento resultavam em falha da solicitação de reempacotamento.
* Alternada para Java long (tipo de dados) para resolver um problema em que atingir o limite de Java int de 2.147.483.647 em valores de ID de trabalho de transcodificação resultaria em falha de todas as solicitações de reempacotamento.
* Otimizações do banco de dados.

## Problemas resolvidos

Quando a resolução estiver associada a um problema reportado, uma referência do Zendesk será exibida. Por exemplo, ZD#xxxxx.

**PTAI 19.7.1**

ZD#37503 - As respostas Json para as regras do CRS são armazenadas em cache para evitar solicitações de duplicado.

## Problemas conhecidos e limitações

**PTAI 19.7.1**

Nenhuma nova limitação foi adicionada.
