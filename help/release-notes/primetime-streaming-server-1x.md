---
title: Versões do servidor de transmissão do Primetime
description: Novidades nas versões 1.3 e 1.4 do Servidor de streaming do Primetime.
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 80c4687e-b0ac-48f2-a1c3-8751552da9d1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---

# Versões do servidor de transmissão do Primetime {#primetime-streaming-server-x-releases}

Novidades nas versões 1.3 e 1.4 do Servidor de streaming do Primetime.

## Novo no servidor de transmissão contínua do Primetime 1.4 (versão de dezembro) {#what-s-new-in-primetime-streaming-server-december-release}

**Empacotador offline**

* Fluxos HLS de saída agora contêm metadados ID3 presentes no MPEG-2 TS
* Somente fluxos de áudio HLS agora podem ter uma imagem estática associada
* Suporte para fornecer IV como entrada do usuário para workflows de criptografia AES do HLS
* Suporte para IV de saída para um arquivo quando IV é gerado pelo empacotador offline
* O Playlist Creator agora oferece suporte à associação de grupos de áudio multilíngue e grupos de legendas multilíngues WebVTT a fluxos de mídia

**Servidor de origem**

* A criptografia HLS AES está disponível para fluxos de trabalho Live e VOD. O Primetime Origin pode Just in Time aplicar a criptografia AES HLS a fluxos HLS ou arquivos MP4 recebidos.
* Ele também pode aplicar a criptografia JIT HLS AES quando ela é usada para converter fluxos HDS recebidos em fluxos HLS.
* O Primetime Origin agora é compatível com a lista de permissões de SWF para fluxos PHLS. Anteriormente, era compatível somente com fluxos PHDS

**Primetime Live Packager**

* Suporte para gerar fluxos HLS AES-128 para fluxos RTMP e MPEG-2 TS de entrada

Os certificados PHDS/PHLS foram atualizados. A nova data de vencimento para o mesmo será 01/10/2016.

### **Correções de erros incluídas na versão 1.4** {#bug-fixes-included-in-release}

* PTPUB-282- O manifesto de nível de conjunto HLS criado pelo OfflinePackager 1.3.1 não tem informações de codec e resolução.
* PTPUB-353 - PlayListCreator não oferece suporte à adição de informações de WebVTT no manifesto de nível definido
* PTPUB-583 - A ferramenta PlaylistCreator anexa inesperadamente os URIs do grupo a.
* PTPUB-605 O criador da lista de reprodução não lista o grupo de LEGENDAS em cada fluxo de variante
* PTPUB-634 - O empacotador offline adiciona SpliceInsert ao manifesto.
* PTPUB-635 - Várias tags SpliceOut inseridas para sinalização de anúncio único.

### Problema conhecido na versão 1.4 {#known-issue-in-release}

* PTPUB- 645 DPISimple Mode é forçado mesmo quando o modo DPIScte35 é especificado quando as dicas de linha de comando e as dicas em fluxo são fornecidas na configuração offline do empacotador

## Novidades no Servidor de transmissão contínua do Primetime 1.3.1 (versão de MAIO) {#what-s-new-in-primetime-streaming-server-may-release}

A versão 1.3.1 se refere ao hotfix. Os seguintes aprimoramentos fazem dele uma atualização recomendada para clientes, pois consiste em aprimoramentos importantes de desempenho para casos de uso do JIT MP4:

1. Correção de desempenho para a geração de m3u8 MP4 JIT no Origin com DRM incluindo Rotação de Chaves
1. Adição de uma configuração &quot;CopyQueryParamToJITFragmentURIs&quot; para copiar parâmetros de consulta da solicitação de manifesto JIT para URIs de fragmento gerados para conversão de JIT MP4. Consulte a documentação do Servidor de Origem HTTP para obter informações sobre o uso de exemplo
1. Permitir arquivos MP4 sem extensão para conversão JIT, por meio da configuração Config/MP4Only adicionada ao vod.xml

### Correções de erros incluídas na versão 1.3.1 {#bug-fixes-included-in-release-1}

* 3759167 - Nem todas as dicas SCTE35 chegam ao manifesto de saída devido a uma anomalia no carimbo de data e hora durante a embalagem. Aplique pts_adjustment na mensagem SpliceTime no TimeSignal of SpliceInfoSection no SCTE35.

### Problemas conhecidos na versão 1.3.1 {#known-issues-in-release}

* 3717039 - Quando o empacotador é configurado para produzir dicas de modo simples de DPI, ele realmente deve estar procurando tipos de sinal específicos, como inserção de splice ou oportunidade de posicionamento, e convertendo apenas esses sinais em dicas de modo simples. Ele deve ignorar outros tipos de sinais, como início de programa, início de rede etc.

* 3718598 - Quando o Servidor de Origem é configurado para fornecer conteúdo protegido com acesso HSM ativado, o cliente LunaSA de back-end faz uma comunicação frequente com o módulo HSM

## Novidades no Servidor de transmissão contínua do Primetime 1.3 (versão de ABRIL) {#what-s-new-in-primetime-streaming-server-april-release}

A versão do Primetime 1.3 traz vários novos recursos sobre Streaming de conteúdo, melhor Usabilidade e Segurança.

**Servidor de streaming do Primetime como uma forma unificada de Live Packager e Servidor de origem**

O Primetime Live Packager e o Primetime Origin são reunidos para funcionar como um único componente. Esse componente pode ser usado como um Packager ou como uma Origem, ou usar os recursos combinados para empacotar e hospedar um Live Stream.

Isso fornece uma interface de arquivos unificada para esses servidores, facilitando sua execução em uma única máquina. Ele continua a fornecer a flexibilidade para ser configurado como um Packager ou Origin separado.

**Suporte para Beta MPEG- DASH**

O servidor de transmissão Primetime é compatível com pacotes MPEG-DASH para fluxos de trabalho Live e VOD. O componente Live Packager converte fluxos de assimilação RTMP ou MPEG-2-TS para o formato DASH. O componente Origin aceita um fluxo DASH.

Para fluxos de trabalho de VOD, o componente Empacotador offline converte ativos MP4 e TS para o formato MPEG-DASH ISOBFF.

**Conversão de Live to VOD**

Um novo componente Servidor de gravação agora está disponível e oferece suporte à captura de um Live Stream e ao arquivamento para reprodução de VOD. Ele suporta a criação de Repetições completas de evento, bem como clipes/destaques para parte do evento. Ele pode ser configurado para gravar fluxos somente de áudio, remover anúncios ou slates no conteúdo ao vivo. O servidor de gravação funciona com o servidor de streaming Primetime, bem como com origens de terceiros.

**Conversão de RTMP para HLS no Primetime Live Packager**

O componente Primetime Live Packager oferece suporte à criação de fluxos HLS de fluxos RTMP. Ele também permite adicionar o Primetime DRM e o Protected Streaming aos fluxos HLS de saída.

**Autenticação para fluxos RTMP de entrada para o Primetime Live Packager**

Um usermgmt.jar agora é enviado com o Primetime Live Packager para configurar o acesso com credenciais confiáveis ao enviar um fluxo RTMP para o Primetime Live Packager

Agora, os codificadores podem ser configurados para usar um nome de usuário/senha ao enviar fluxos para o Live Packager.

**Ferramenta PlaylistCreator para criar manifestos de nível superior para HDS e HLS**

Um utilitário sofisticado PlaylistCreator.jar agora está disponível com o Primetime Offline Packager para criar facilmente arquivos manifest de nível superior para ativos HDS e HLS.

**Recurso de segurança adicional para incorporar um módulo de segurança de hardware**

O Empacotador offline do Primetime agora oferece suporte ao acesso ao Certificado de credencial do empacotador e às chaves comuns de um Módulo de segurança de hardware.

Um módulo de Segurança de hardware fornece proteção adicional a esses ativos confidenciais.

**Desempenho aprimorado para empacotamento de VOD**

Várias melhorias de desempenho foram incorporadas para melhorar o tempo de empacotamento de ativos mezanino no Primetime Offline Packager

**Desempenho aprimorado para o empacotamento JIT MP4**

Várias melhorias de desempenho foram incorporadas aos recursos de empacotamento JIT do Primetime Origin para lidar com solicitações de usuários de uma grande biblioteca de ativos de VOD.

## Adobe Primetime Streaming Server 1.4 {#adobe-primetime-streaming-server}

### Requisitos mínimos do sistema {#minimum-system-requirements}

**Requisitos de rede**

* A rede deve ser habilitada para Multicast para enviar o fluxo MPEG-TS de um codificador para o Live Packager. O Live Packager também aceita um fluxo RTMP de um codificador que não requer uma rede multicast.

**Sistemas operacionais compatíveis**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se Intel Xeon® duplo ou mais rápido)
* Sistemas operacionais de 64 bits: 4 GB de RAM (recomenda-se 8 GB)
* Placa Ethernet de 1 Gbit recomendada (várias placas de rede e 10 Gbit também são compatíveis)
* Disco:

   * (Disco-SAS) : mínimo de 10 GB com 7.500 RPM
   * (Disco-SSD) : leitura/gravação de 400 MBps
   * (NAS) : link dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 (recomendado: Sun/Oracle Hotspot JVM). O JDK é necessário para o acesso do JConsole às APIs JMX

### Instalar e configurar o servidor de transmissão do Primetime {#install-and-configure-primetime-streaming-server}

**Instalar servidor de streaming**

1. Baixe o software Java SE e JDK do [site do Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
2. Extraia o arquivo morto do Adobe Primetime-Streaming Server 1.4, `Primetime- StreamingServer-1-4-0-b206-12042014.zip` no disco.

**Iniciar o servidor de transmissão do Primetime**

Para iniciar o servidor de streaming, execute o seguinte comando na linha de comando no diretório raiz do servidor de streaming:\
`$./pss_start.sh`

**Configure o servidor de streaming do Primetime como um Live Packager ou um servidor de origem HTTP**

Para configurar o Servidor de Streaming como Live Packager ou Servidor de Origem, atualize o arquivo de configuração pss.xml colocado no diretório conf no diretório raiz do Servidor de Streaming:

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**Parar o servidor de transmissão do Primetime**

Para interromper o servidor de streaming, execute o seguinte comando no diretório raiz do servidor de streaming:\
`$./pss_stop.sh`

**Reinicie o servidor de transmissão do Primetime**

Para reiniciar o servidor de streaming, pare e inicie o servidor de streaming.

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**Desinstalar o servidor de streaming do Primetime**

Para desinstalar o servidor de streaming, pare o servidor de streaming e remova o diretório pss do servidor de streaming no diretório Primetime

## Trabalhando com o Live Packager e o Servidor de Origem 1.4 {#working-with-live-packager-and-origin-server}

Esta seção se aplica quando o Servidor de transmissão do Primetime não é usado e, em vez disso, o Pacote Primetime Live E/OU o Servidor de origem do Primetime está sendo implantado

### Requisitos mínimos do sistema {#minimum-system-requirements-1}

**Requisitos de rede**

* A rede deve ser habilitada para Multicast para enviar o fluxo MPEG-TS de um codificador para o Live Packager. O Live Packager também aceita um fluxo RTMP de um codificador que não requer uma rede multicast.

**Sistemas operacionais compatíveis**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se Intel Xeon® duplo ou mais rápido)
* Sistemas operacionais de 64 bits: 4 GB de RAM (recomenda-se 8 GB)
* Placa Ethernet de 1 Gbit recomendada (várias placas de rede e 10 Gbit também são compatíveis)
* Disco:

   * (Disco-SAS) : mínimo de 10 GB com 7.500 RPM
   * (Disco-SSD) : leitura/gravação de 400 MBps
   * (NAS) : link dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 (recomendado: Sun/Oracle Hotspot JVM). O JDK é necessário para o acesso do JConsole às APIs JMX

Os requisitos mínimos de sistema acima se aplicam ao Servidor de Origem e ao Live Packager.

### Instalar e configurar o Live Packager {#install-and-configure-the-live-packager}

**Instalação do Live Packager**

1. Baixe o software Java SE e JDK do [site do Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
1. Extraia o arquivo do Adobe Primetime - Live Packager 1.4 `Primetime-LivePackager-1-4-0-b206-12042014.zip` no disco.

**Instalar o Servidor de Origem HTTP**

1. Baixe o Java JRE e o software JDK do [site do Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
1. Extraia o arquivo Adobe Primetime - HTTP Origin Server 1.4, `Primetime-HttpOrigin-1-4-0-b206-12042014.zip`, para o disco.

**Para iniciar o Live Packager** Para iniciar o empacotador, execute o seguinte comando no diretório raiz do empacotador:\
`$packager_start.sh`

**Para iniciar o Servidor de Origem HTTP**

Para iniciar o Servidor de Origem HTTP, execute o seguinte comando a partir da linha de comando no diretório raiz do Servidor de Origem:\
`$./origin_start.sh`

**Interromper o Live Packager**

Para interromper o empacotador, execute o seguinte comando no diretório raiz do empacotador:\
`$packager_stop.sh`

**Interromper o Servidor de Origem HTTP**

Para interromper o Servidor de Origem HTTP, execute o seguinte comando no diretório raiz do Servidor de Origem:\
`$./origin_stop.sh`

**Reinicie o Live Packager**

Para reiniciar o empacotador, pare-o e inicie-o.

**Nota**: Quando o empacotador é iniciado, ele tenta inicializar as informações de inicialização do destino do fragmento no diretório temporário. Se as informações de inicialização forem encontradas no destino do fragmento, isso implica que o empacotador foi reiniciado. No caso de reinicialização, o empacotador aguarda até o próximo limite de fragmento e, em seguida, inicia o empacotamento. O empacotador insere uma entrada de intervalo na inicialização para indicar que há fragmentos ausentes.

**Reiniciar o Servidor de Origem HTTP**

Para reiniciar o Servidor de Origem HTTP, pare e inicie o Servidor de Origem HTTP.

**Configuração do Live Packager**

O arquivo de distribuição contém uma configuração de exemplo que pode ser usada para testar o empacotador.

Após extrair o arquivo Adobe Primetime - Live Packager 1.4, altere os diretórios para o diretório packager e execute o script packager_start.sh. A configuração de amostra escuta no endereço de multicast 239.235.0.3:14000 e executa o servidor de origem local na porta 8080. A saída é configurada para ser gravada na variável `packager/webroot/_default_/_default_/ directory`.

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**Configurar o Servidor de Origem HTTP**

Consulte o documento de Introdução do Servidor de Origem HTTP do Primetime para obter os detalhes de configuração disponíveis aqui.

**Desinstalação do Live Packager**

Para desinstalar o empacotador, pare-o e remova-o do diretório do Primetime.

**Desinstalando o Servidor de Origem HTTP**

Para desinstalar o Servidor de Origem HTTP, interrompa o Servidor de Origem HTTP e remova o diretório httporigin do Servidor de Origem HTTP no diretório Primetime.

## Adobe Primetime Offline Packager 1.4 {#adobe-primetime-offline-packager}

### Requisitos mínimos do sistema {#minimum-system-requirements-2}

**Sistemas operacionais compatíveis**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se Intel Xeon® duplo ou mais rápido)
* Sistemas operacionais de 64 bits: 4 GB de RAM (recomenda-se 8 GB)
* Placa Ethernet de 1 Gbit recomendada (várias placas de rede e 10 Gbit também são compatíveis)
* Disco:

   * (Disco-SAS) : mínimo de 10 GB com 7.500 RPM
   * (Disco-SSD) : leitura/gravação de 400 MBps
   * (NAS) : link dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 ou posterior.

### Instalar e configurar o Packager Offline {#install-and-configure-offline-packager}

Para instalar o Offline Packager, siga estas etapas:

1. Baixe o software Java SE na [site do Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
1. Extraia o arquivo Adobe Primetime - Offline Packager 1.4, `Primetime- OfflinePackager-1-4-0-b206-12042014.zip`, para o disco.

Consulte o documento Introdução ao Primetime Offline Packager para obter os detalhes de configuração disponíveis [aqui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
