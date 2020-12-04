---
title: Versões do Primetime Streaming Server
seo-title: Versões do Primetime Streaming Server 1.x
description: Novidades das versões 1.3 e 1.4 do Primetime Streaming Server.
seo-description: Novidades das versões 1.3 e 1.4 do Primetime Streaming Server.
uuid: be05db6b-713f-4406-940d-9f3a805f967b
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: baec714e-9d41-4e8b-b134-13a736885cbd
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1929'
ht-degree: 0%

---


# Versões do Primetime Streaming Server {#primetime-streaming-server-x-releases}

Novidades das versões 1.3 e 1.4 do Primetime Streaming Server.

## Novo no Primetime Streaming Server 1.4 (versão de dezembro) {#what-s-new-in-primetime-streaming-server-december-release}

**Offline Packager**

* Os fluxos HLS de saída agora contêm metadados ID3 presentes no MPEG-2 TS
* Os fluxos somente de áudio HLS agora podem ter uma imagem estática associada
* Suporte para fornecer IV como entrada de usuário para workflows de criptografia AES HLS
* Suporte para saída IV para um arquivo quando IV é gerado pelo empacotador offline
* O Playlist Creator agora é compatível com a associação de grupos de áudio de vários idiomas e grupos de legendas WebVTT de vários idiomas aos fluxos de mídia

**Servidor origem**

* A encriptação HLS AES está disponível para workflows Live e VOD. A Origem Primetime pode aplicar a criptografia AES HLS a fluxos HLS de entrada ou arquivos MP4.
* Também pode aplicar criptografia JIT HLS AES quando usada para converter fluxos HDS recebidos em fluxos HLS.
* A Origem Primetime agora suporta a listagem de permissão de SWF para fluxos PHLS. Anteriormente, era compatível somente com fluxos PHDS

**Primetime Live Packager**

* Suporte para gerar fluxos HLS AES-128 para fluxos de entrada RTMP e MPEG-2 TS

Os certificados PHDS/PHLS foram atualizados. A nova data de expiração para o mesmo período será 01/10/2016.

### **Correções de erros incluídas na versão 1.4** {#bug-fixes-included-in-release}

* PTPUB-282- O manifesto de nível de conjunto HLS criado pelo OfflinePackager 1.3.1 não tem informações de codec e resolução.
* PTPUB-353 - PlayListCreator não suporta a adição de informações de WebVTT no manifesto de nível de conjunto
* PTPUB-583 - A ferramenta PlaylistCreator prepara inesperadamente URIs de grupo.
* PTPUB-605 Playlist Creator não listando SUBTITLE Group em cada fluxo variante
* PTPUB-634 -Offline Packager adiciona SpliceInsert ao manifesto.
* PTPUB-635 - Várias tags SpliceOut inseridas para uma única dica de anúncio.

### Problema conhecido na versão 1.4 {#known-issue-in-release}

* PTPUB- 645 DPISimple Mode é forçado mesmo quando o modo DPIScte35 é especificado quando as dicas de linha de comando e as dicas em fluxo são fornecidas na configuração offline do empacotador

## Novidades do Primetime Streaming Server 1.3.1 (Versão do MAIO) {#what-s-new-in-primetime-streaming-server-may-release}

A versão 1.3.1 se refere ao hotfix. Os seguintes aprimoramentos fazem dele uma atualização recomendada para os clientes, pois consiste em melhorias de desempenho importantes para casos de uso de JIT MP4:

1. Correção de desempenho para geração MP4 JIT m3u8 em Origem com DRM incluindo rotação de chaves
1. Adicionada uma configuração &quot;CopyQueryParamToJITFragmentURIs&quot; para copiar parâmetros de query da solicitação de manifesto JIT para URIs de fragmento gerados para conversão MP4 JIT. Consulte a documentação do Servidor de Origem HTTP para obter exemplos de uso
1. Permitir arquivos MP4 sem extensão para conversão JIT, pela configuração Config/MP4Only adicionada ao vod.xml

### Correções de erros incluídas na versão 1.3.1 {#bug-fixes-included-in-release-1}

* 3759167 - Nem todas as dicas SCTE35 chegam ao manifesto de saída devido a uma anomalia no carimbo de data e hora durante o empacotamento. Aplique pts_adjustment no SpliceTime no TimeSignal de SpliceInfoSection na mensagem SCTE35.

### Problemas conhecidos na versão 1.3.1 {#known-issues-in-release}

* 3717039 - Quando o empacotador está configurado para produzir dicas de modo simples de DPI, ele realmente deve procurar tipos de sinal específicos, como inserção de splice ou oportunidade de posicionamento, e converter somente esses tipos em dicas de modo simples. Ele deve ignorar outros tipos de sinais, como start de programa, start de rede etc.

* 3718598 - Quando o Servidor de Origem está configurado para fornecer conteúdo protegido com acesso HSM ativado, o cliente LunaSA de backend faz uma comunicação frequente com o módulo HSM

## Novidades do Primetime Streaming Server 1.3 (versão de ABRIL) {#what-s-new-in-primetime-streaming-server-april-release}

A versão Primetime 1.3 traz vários novos recursos para o conteúdo Streaming, melhor utilização e segurança.

**Primetime Streaming Server como uma forma unificada do Live Packager e do Origem Server**

O Primetime Live Packager e a Origem Primetime são reunidos para funcionar como um único componente. Esse componente pode ser usado como um Packager ou como uma Origem ou usar os recursos combinados para disponibilizar e hospedar um Live Stream.

Isso fornece uma interface de arquivo unificada para esses servidores, facilitando a execução em uma única máquina. Ele continua a oferecer a flexibilidade de ser configurado como um Packager ou Origem separado.

**Beta MPEG - Suporte DASH**

O Primetime Streaming Server oferece suporte ao empacotamento MPEG-DASH para workflows ao vivo e VOD. O componente do Live Packager converte assimilar fluxos RTMP ou MPEG-2-TS para o formato DASH. O componente de Origem aceita um fluxo DASH.

Para workflows VOD, o componente Offline Packager converte ativos MP4 e TS para o formato MPEG-DASH ISOBFF.

**Conversão ao vivo para VOD**

Um novo servidor de gravação de componente está disponível e oferece suporte à captura de um fluxo ao vivo e ao arquivamento para reprodução VOD. Ele suporta a criação de Reproduções completas de Evento, bem como clipes/realces para parte do evento. Ele pode ser configurado para gravar fluxos somente de áudio, remover anúncios ou slates em conteúdo ao vivo. O Servidor de Gravação funciona com o Primetime Streaming Server, bem como com Origens de terceiros.

**Conversão RTMP para HLS no Primetime Live Packager**

O componente Primetime Live Packager suporta a criação de fluxos HLS de fluxos RTMP. Também permite adicionar o Primetime DRM e o Protected Streaming aos fluxos HLS de saída.

**Autenticação para fluxos RTMP de entrada para o Primetime Live Packager**

Um usermgmt.jar agora é enviado com o Primetime Live Packager para configurar o acesso com credenciais confiáveis ao enviar um fluxo RTMP para o Primetime Live Packager

Agora, os codificadores podem ser configurados para usar um nome de usuário/senha ao enviar fluxos para o Live Packager.

**Ferramenta PlaylistCreator para criar manifestos de nível superior para HDS e HLS**

Um utilitário elegante PlaylistCreator.jar agora está disponível com o Primetime Offline Packager para criar facilmente arquivos manifest de nível superior para ativos HDS e HLS.

**Recurso de segurança adicional para incorporar um módulo de segurança de hardware**

O Primetime Offline Packager agora oferece suporte ao acesso ao Certificado de Credencial do Packager e às Chaves Comuns de um Módulo de Segurança de Hardware.

Um módulo de segurança de hardware fornece proteção adicional a esses ativos confidenciais.

**Desempenho aprimorado para encapsulamento VOD**

Vários aprimoramentos de desempenho foram incorporados para melhorar o tempo de empacotamento dos recursos de mezanino no Primetime Offline Packager

**Desempenho aprimorado para empacotamento JIT MP4**

Vários aprimoramentos de desempenho foram incorporados aos recursos de empacotamento JIT da Origem Primetime para lidar com solicitações de usuários de uma grande biblioteca de ativos VOD.

## Adobe Primetime Streaming Server 1.4 {#adobe-primetime-streaming-server}

### Requisitos mínimos do sistema {#minimum-system-requirements}

**Requisitos de rede**

* A rede deve estar habilitada para Multicast para enviar fluxo MPEG-TS de um codificador para o Live Packager. O Live Packager também aceita um fluxo RTMP de um codificador que não requer uma rede multicast.

**Sistemas operacionais suportados**

* Linux CentOS 6.3 64 bits

**Requisitos de hardware**

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se Intel Xeon® dual ou mais veloz)
* Sistemas operacionais de 64 bits: 4 GB de RAM (8 GB recomendado)
* Placa Ethernet de 1 Gb recomendada (várias placas de rede e 10 Gb também são suportadas)
* Disco:

   * (Disco-SAS): Mínimo de 10 GB com 7,5 K RPM
   * (Disco-SSD): Leitura/gravação de 400 MBps
   * (NAS) : Link dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 (Recomendado: Sun/Oracle Hotspot JVM). O JDK é necessário para acesso do JConsole às APIs JMX

### Instalar e configurar o Primetime Streaming Server {#install-and-configure-primetime-streaming-server}

**Instale o servidor de streaming**

1. Baixe o software Java SE e JDK do [site da Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
2. Extraia o arquivo de arquivamento do Adobe Primetime-Streaming Server 1.4, `Primetime- StreamingServer-1-4-0-b206-12042014.zip` para o disco.

**Start do Primetime Streaming Server**

Para start do Servidor de Streaming, execute o seguinte comando da linha de comando no diretório raiz do Servidor de Streaming:\
`$./pss_start.sh`

**Configure o Primetime Streaming Server como Live Packager ou HTTP Origem Server**

Para configurar o Servidor de Streaming como Live Packager ou Origem Server, atualize o arquivo de configuração pss.xml colocado no diretório conf no diretório raiz do Servidor de Streaming:

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**Parar o servidor de streaming Primetime**

Para parar o Servidor de Streaming, execute o seguinte comando no diretório raiz do Servidor de Streaming:\
`$./pss_stop.sh`

**Reinicie o servidor de streaming Primetime**

Para reiniciar o Servidor de transmissão, pare e start o Servidor de transmissão.

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**Desinstalação do Primetime Streaming Server**

Para desinstalar o Servidor de Streaming, pare o Servidor de Streaming e remova o diretório pss do Servidor de Streaming no diretório Primetime

## Trabalhar com o Live Packager e o Origem Server 1.4 {#working-with-live-packager-and-origin-server}

Esta seção se aplica quando o Primetime Streaming Server não é usado e, em vez disso, o Primetime Live Packager AND/OR Primetime Origem Server está sendo implantado

### Requisitos mínimos do sistema {#minimum-system-requirements-1}

**Requisitos de rede**

* A rede deve estar habilitada para Multicast para enviar fluxo MPEG-TS de um codificador para o Live Packager. O Live Packager também aceita um fluxo RTMP de um codificador que não requer uma rede multicast.

**Sistemas operacionais suportados**

* Linux CentOS 6.3 64 bits

**Requisitos de hardware**

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se Intel Xeon® dual ou mais veloz)
* Sistemas operacionais de 64 bits: 4 GB de RAM (8 GB recomendado)
* Placa Ethernet de 1 Gb recomendada (várias placas de rede e 10 Gb também são suportadas)
* Disco:

   * (Disco-SAS): Mínimo de 10 GB com 7,5 K RPM
   * (Disco-SSD): Leitura/gravação de 400 MBps
   * (NAS) : Link dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 (Recomendado: Sun/Oracle Hotspot JVM). O JDK é necessário para acesso do JConsole às APIs JMX

Os requisitos mínimos de sistema acima são válidos para o Origem Server e para o Live Packager.

### Instalar e configurar o Live Packager {#install-and-configure-the-live-packager}

**Instalação do Live Packager**

1. Baixe o software Java SE e JDK do [site da Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
1. Extraia o arquivo de arquivamento Adobe Primetime - Live Packager 1.4 `Primetime-LivePackager-1-4-0-b206-12042014.zip` para o disco.

**Instalação do Servidor de Origem HTTP**

1. Baixe o Java JRE e o software JDK do [site da Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
1. Extraia o arquivo de arquivamento Adobe Primetime - HTTP Origem Server 1.4, `Primetime-HttpOrigin-1-4-0-b206-12042014.zip`, para o disco.

**Para start do Live** PackagerTo start o Packager, execute o seguinte comando do diretório raiz do Packager:\
`$packager_start.sh`

**Para start do Servidor de Origem HTTP**

Para start do Servidor de Origem HTTP, execute o seguinte comando da linha de comando no diretório raiz do Origem Server:\
`$./origin_start.sh`

**Parar o Live Packager**

Para interromper o empacotador, execute o seguinte comando do diretório raiz do empacotador:\
`$packager_stop.sh`

**Parar o Servidor de Origem HTTP**

Para interromper o Servidor de Origem HTTP, execute o seguinte comando no diretório raiz do Servidor de Origem:\
`$./origin_stop.sh`

**Reinicie o Live Packager**

Para reiniciar o empacotador, pare e start o empacotador.

**Observação**: Quando o empacotador é start, ele tenta inicializar as informações de inicialização do público alvo do fragmento no diretório temporário. Se as informações do bootstrap forem encontradas no público alvo do fragmento, isso significa que o empacotador foi reiniciado. Em caso de reinicialização, o empacotador aguarda até o próximo limite do fragmento e, em seguida, start o empacotamento. O empacotador insere uma entrada de espaço no bootstrap para indicar que há fragmentos ausentes.

**Reinicie o servidor de Origem HTTP**

Para reiniciar o Servidor de Origem HTTP, pare e start o Servidor de Origem HTTP.

**Configuração do Live Packager**

O arquivo de distribuição contém uma configuração de amostra que pode ser usada para testar o empacotador.

Depois de extrair o arquivo Adobe Primetime - Live Packager 1.4, altere os diretórios para o diretório Packager e execute o script packager_start.sh. A configuração de amostra escuta o endereço multicast 239.235.0.3:14000 e executa o servidor de origem local na porta 8080. A saída está configurada para ser gravada em `packager/webroot/_default_/_default_/ directory`.

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**Configuração do Servidor de Origem HTTP**

Consulte o documento Introdução do Primetime HTTP Origem Server para obter os detalhes de configuração disponíveis aqui.

**Desinstalação do Live Packager**

Para desinstalar o empacotador, pare o empacotador e remova o diretório do empacotador do diretório Primetime.

**Desinstalação do Servidor de Origem HTTP**

Para desinstalar o Servidor de Origem HTTP, pare o Servidor de Origem HTTP e remova o diretório httporigin do Servidor de Origem HTTP no diretório Primetime.

## Adobe Primetime Offline Packager 1.4 {#adobe-primetime-offline-packager}

### Requisitos mínimos do sistema {#minimum-system-requirements-2}

**Sistemas operacionais suportados**

* Linux CentOS 6.3 64 bits

**Requisitos de hardware**

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se Intel Xeon® dual ou mais veloz)
* Sistemas operacionais de 64 bits: 4 GB de RAM (8 GB recomendado)
* Placa Ethernet de 1 Gb recomendada (várias placas de rede e 10 Gb também são suportadas)
* Disco:

   * (Disco-SAS): Mínimo de 10 GB com 7,5 K RPM
   * (Disco-SSD): Leitura/gravação de 400 MBps
   * (NAS) : Link dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 ou posterior.

### Instalar e configurar o Offline Packager {#install-and-configure-offline-packager}

Para instalar o Offline Packager, siga estas etapas:

1. Baixe o software Java SE do [site da Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
1. Extraia o arquivo de arquivamento Adobe Primetime - Offline Packager 1.4, `Primetime- OfflinePackager-1-4-0-b206-12042014.zip`, para o disco.

Consulte o documento de Introdução do Primetime Offline Packager para obter os detalhes de configuração disponíveis [aqui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página [Aprendizagem e suporte da Adobe Primetime](https://helpx.adobe.com/support/primetime.html).