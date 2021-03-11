---
title: Versões do Primetime Streaming Server
description: Novidades das versões 1.3 e 1.4 do Primetime Streaming Server.
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---


# Versões do Primetime Streaming Server {#primetime-streaming-server-x-releases}

Novidades das versões 1.3 e 1.4 do Primetime Streaming Server.

## Novo no Primetime Streaming Server 1.4 (Versão de dezembro) {#what-s-new-in-primetime-streaming-server-december-release}

**Pacote offline**

* Os fluxos de HLS de saída agora contêm metadados ID3 presentes no MPEG-2 TS
* Somente o áudio HLS pode ter uma imagem estática associada
* Suporte para fornecer IV como entrada de usuário para workflows de criptografia AES HLS
* Suporte para saída IV para um arquivo quando IV é gerado pelo empacotador offline
* O Playlist Creator agora oferece suporte à associação de grupos de áudio multilíngue e grupos de subtítulos de VTT da Web multilíngue a fluxos de mídia

**Servidor de Origem**

* A criptografia AES HLS está disponível para fluxos de trabalho Live e VOD. A origem do Primetime pode, no momento, aplicar a criptografia AES HLS a fluxos HLS ou arquivos MP4 de entrada.
* Também pode aplicar a criptografia JIT HLS AES quando usada para converter fluxos HDS recebidos em fluxos HLS.
* A origem do Primetime agora é compatível com a lista de permissões de SWF para fluxos PHLS. Anteriormente, era compatível somente com fluxos PHDS

**Primetime Live Packager**

* Suporte para gerar fluxos HLS AES-128 para fluxos RTMP de entrada e MPEG-2 TS

Os certificados PHDS/PHLS foram atualizados. O novo prazo de validade para o mesmo será 01/10/2016.

### **Correções de erros incluídas na versão 1.4** {#bug-fixes-included-in-release}

* PTPUB-282 - O manifesto de nível de conjunto HLS criado pelo OfflinePackager 1.3.1 não tem informações de codec e resolução.
* PTPUB-353 - PlayListCreator não suporta a adição de informações WebVTT no manifesto de nível de conjunto
* PTPUB-583 - A ferramenta PlaylistCreator prepara inesperadamente URIs de grupo com.
* PTPUB-605 Criador da lista de reprodução que não lista o Grupo SUBTITLE em cada fluxo de variante
* PTPUB-634 -Offline Packager adiciona SpliceInsert ao manifesto.
* PTPUB-635 - Várias tags SpliceOut inseridas para dicas de anúncio único.

### Problema conhecido na versão 1.4 {#known-issue-in-release}

* PTPUB- 645 DPISimple Mode é forçado mesmo quando o modo DPIScte35 é especificado quando as dicas da linha de comando e as dicas em fluxo são fornecidas na configuração offline do empacotador

## Novidades do Primetime Streaming Server 1.3.1 (Versão MAIO) {#what-s-new-in-primetime-streaming-server-may-release}

A versão 1.3.1 se refere ao hotfix. Os seguintes aprimoramentos fazem dele uma atualização recomendada para os clientes, pois consiste em principais melhorias de desempenho para casos de uso de JIT MP4:

1. Correção de desempenho para geração MP4 JIT m3u8 na origem com DRM incluindo rotação de chaves
1. Adição de uma configuração &quot;CopyQueryParamToJITFragmentURIs&quot; para copiar parâmetros de consulta da solicitação de manifesto JIT para URIs de fragmento gerados para conversão MP4 JIT. Consulte a documentação do Servidor de origem HTTP para obter o uso de exemplo
1. Permitir arquivos MP4 sem extensão para conversão JIT , por meio da configuração Config/MP4Only adicionada ao vod.xml

### Correções de erros incluídas na versão 1.3.1 {#bug-fixes-included-in-release-1}

* 3759167 - Nem todas as dicas SCTE35 o fazem no manifesto de saída devido à anomalia de carimbo de data e hora durante o empacotamento. Aplique pts_ajuste no SpliceTime no TimeSignal of SpliceInfoSection na mensagem SCTE35.

### Problemas conhecidos na versão 1.3.1 {#known-issues-in-release}

* 3717039 - Quando o empacotador está configurado para produzir dicas de modo simples de DPI, ele realmente deve estar procurando tipos de sinal específicos, como inserção de quebra ou oportunidade de posicionamento, e convertendo apenas aqueles em dicas de modo simples. Deve ignorar outros tipos de sinais, como o início do programa, o início da rede, etc.

* 3718598 - Quando o Servidor de Origem é configurado para servir conteúdo protegido com acesso HSM habilitado, o cliente LunaSA de back-end faz uma comunicação frequente com o módulo HSM

## Novidades do Primetime Streaming Server 1.3 (Versão de ABRIL) {#what-s-new-in-primetime-streaming-server-april-release}

A versão Primetime 1.3 traz vários novos recursos sobre o conteúdo de streaming, melhor usabilidade e segurança.

**Servidor de transmissão do Primetime como uma forma unificada do Live Packager e do Servidor de origem**

O Primetime Live Packager e a Origem do Primetime são reunidos para funcionar como um único componente. Esse componente pode ser usado como um Empacotador ou como uma Origem ou usar os recursos combinados para empacotar e hospedar um Live Stream.

Isso fornece uma interface de arquivo unificada para esses servidores, facilitando a execução em uma única máquina. Ele continua a fornecer a flexibilidade para ser configurado como um Empacotador ou Origem separado.

**Beta MPEG - Suporte a DASH**

O Primetime Streaming Server oferece suporte à empacotamento MPEG-DASH para fluxos de trabalho Live e VOD. O componente do Live Packager converte os fluxos de assimilação RTMP ou MPEG-2-TS para o formato DASH. O componente Origem aceita um fluxo DASH.

Para fluxos de trabalho de VOD, o componente do Pacote Offline converte ativos MP4 e TS para o formato MPEG-DASH ISOBFF.

**Conversão ao vivo para VOD**

Um novo componente Servidor de gravação está disponível e oferece suporte à captura de um fluxo ao vivo e ao arquivamento para reprodução de VOD. Ele suporta a criação de Reproduções completas de eventos, bem como clipes/destaques para parte do evento. Ele pode ser configurado para gravar fluxos somente de áudio, remover anúncios ou slates no conteúdo ao vivo. O Servidor de Gravação funciona com o Servidor de Streaming do Primetime, bem como com Origens de terceiros.

**Conversão RTMP para HLS no Primetime Live Packager**

O componente Primetime Live Packager suporta a criação de fluxos HLS a partir de fluxos RTMP. Também permite adicionar o Primetime DRM e o Protected Streaming aos fluxos HLS de saída.

**Autenticação para fluxos RTMP de entrada para pacotes Primetime Live**

Um usermgmt.jar agora vem com o Primetime Live Packager para configurar o acesso com credenciais confiáveis ao enviar um fluxo RTMP para o Primetime Live Packager

Agora, os codificadores podem ser configurados para usar um nome de usuário/senha ao enviar fluxos para o Live Packager.

**Ferramenta PlaylistCreator para criar manifestos de nível superior para HDS e HLS**

Um utilitário infinito PlaylistCreator.jar agora está disponível com o Primetime Offline Packager para criar facilmente arquivos de manifesto de nível superior para ativos HDS e HLS.

**Recurso de segurança adicional para incorporar um módulo de segurança de hardware**

O Primetime Offline Packager agora oferece suporte ao acesso ao Certificado de Credencial do Packager e às Chaves Comuns de um Módulo de Segurança de Hardware.

Um módulo de segurança de hardware fornece proteção adicional a esses ativos confidenciais.

**Desempenho aprimorado para pacotes de VOD**

Vários aprimoramentos de desempenho foram incorporados para melhorar o tempo de empacotamento dos ativos mezanino no Primetime Offline Packager

**Desempenho aprimorado para empacotamento JIT MP4**

Vários aprimoramentos de desempenho foram incorporados aos recursos de empacotamento JIT da origem do Primetime para lidar com solicitações de usuários de uma grande biblioteca de ativos VOD.

## Adobe Primetime Streaming Server 1.4 {#adobe-primetime-streaming-server}

### Requisitos mínimos do sistema {#minimum-system-requirements}

**Requisitos de rede**

* A rede deve ser Multicast ativada para enviar o fluxo MPEG-TS de um codificador para o Live Packager. O Live Packager também aceita um fluxo RTMP de um codificador que não requer uma rede multicast.

**Sistemas operacionais compatíveis**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se duplo Intel Xeon® ou mais rápido)
* Sistemas operacionais de 64 bits: 4 GB de RAM (8 GB recomendado)
* Placa Ethernet de 1 Gb recomendada (várias placas de rede e 10 Gb também são suportadas)
* Disco:

   * (Disk-SAS) : Mínimo de 10 GB com 7.500 RPM
   * (Disk-SSD) : Leitura/gravação de 400MBps
   * (NAS) : Link dedicado de 1 GB

**Requisitos de software**

* Java JRE 1.7 do Oracle (Recomendado: Sun/Oracle Hotspot JVM). O JDK é necessário para o acesso do JConsole às APIs JMX

### Instalar e configurar o Primetime Streaming Server {#install-and-configure-primetime-streaming-server}

**Instalar o servidor de transmissão**

1. Baixe o software Java SE e JDK do [Oracle site](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
2. Extraia o arquivo de arquivamento do Adobe Primetime-Streaming Server 1.4, `Primetime- StreamingServer-1-4-0-b206-12042014.zip` para o disco.

**Inicie o servidor de transmissão do Primetime**

Para iniciar o Streaming Server, execute o seguinte comando da linha de comando no diretório raiz do Streaming Server:\
`$./pss_start.sh`

**Configurar o servidor de transmissão do Primetime como Live Packager ou Servidor de origem HTTP**

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

Para interromper o Servidor de transmissão, execute o seguinte comando no diretório raiz do Servidor de transmissão:\
`$./pss_stop.sh`

**Reinicie o servidor de transmissão do Primetime**

Para reiniciar o Servidor de transmissão, pare e inicie o Servidor de transmissão.

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**Desinstalação do servidor de streaming do Primetime**

Para desinstalar o Servidor de transmissão, pare o Servidor de transmissão e remova o diretório pss do Servidor de transmissão no diretório Primetime

## Trabalhar com o Live Packager e o Servidor de Origem 1.4 {#working-with-live-packager-and-origin-server}

Esta seção se aplica quando o Primetime Streaming Server não é usado e, em vez disso, o Primetime Live packager AND/OR Primetime Origin Server está sendo implantado

### Requisitos mínimos do sistema {#minimum-system-requirements-1}

**Requisitos de rede**

* A rede deve ser Multicast ativada para enviar o fluxo MPEG-TS de um codificador para o Live Packager. O Live Packager também aceita um fluxo RTMP de um codificador que não requer uma rede multicast.

**Sistemas operacionais compatíveis**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se duplo Intel Xeon® ou mais rápido)
* Sistemas operacionais de 64 bits: 4 GB de RAM (8 GB recomendado)
* Placa Ethernet de 1 Gb recomendada (várias placas de rede e 10 Gb também são suportadas)
* Disco:

   * (Disk-SAS) : Mínimo de 10 GB com 7.500 RPM
   * (Disk-SSD) : Leitura/gravação de 400MBps
   * (NAS) : Link dedicado de 1 GB

**Requisitos de software**

* Java JRE 1.7 do Oracle (Recomendado: Sun/Oracle Hotspot JVM). O JDK é necessário para o acesso do JConsole às APIs JMX

Os requisitos mínimos do sistema acima são verdadeiros para o Servidor de Origem e para o Live Packager.

### Instale e configure o Live Packager {#install-and-configure-the-live-packager}

**Instalar o Live Packager**

1. Baixe o software Java SE e JDK do [Oracle site](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
1. Extraia o arquivo de arquivo Adobe Primetime - Live Packager 1.4 `Primetime-LivePackager-1-4-0-b206-12042014.zip` para o disco.

**Instalar o Servidor de Origem HTTP**

1. Baixe o Java JRE e o software JDK do [Oracle site](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
1. Extraia o arquivo de arquivo Adobe Primetime - Servidor de Origem HTTP 1.4, `Primetime-HttpOrigin-1-4-0-b206-12042014.zip`, para o disco.

**Para iniciar o Live** PackagerPara iniciar o empacotador, execute o seguinte comando a partir do diretório raiz do empacotador:\
`$packager_start.sh`

**Para iniciar o Servidor de Origem HTTP**

Para iniciar o Servidor de Origem HTTP, execute o seguinte comando da linha de comando no diretório raiz do Servidor de Origem:\
`$./origin_start.sh`

**Pare o Live Packager**

Para interromper o empacotador, execute o seguinte comando do diretório raiz do empacotador:\
`$packager_stop.sh`

**Parar o Servidor de Origem HTTP**

Para interromper o Servidor de Origem HTTP, execute o seguinte comando no diretório raiz do Servidor de Origem:\
`$./origin_stop.sh`

**Reinicie o Live Packager**

Para reiniciar o empacotador, pare e inicie o empacotador.

**Observação**: Quando o empacotador é iniciado, ele tenta inicializar as informações do bootstrap do destino do fragmento no diretório temporário. Se as informações do bootstrap forem encontradas no destino do fragmento, isso significa que o empacotador foi reiniciado. Em caso de reinicialização, o empacotador aguarda até o próximo limite do fragmento e inicia a embalagem. O empacotador insere uma entrada de espaço no bootstrap para indicar que há fragmentos ausentes.

**Reinicie o servidor de origem HTTP**

Para reiniciar o Servidor de Origem HTTP, pare e inicie o Servidor de Origem HTTP.

**Configuração do Live Packager**

O arquivo de distribuição contém uma configuração de amostra que pode ser usada para testar o empacotador.

Depois de extrair o arquivo Adobe Primetime - Live Packager 1.4, altere os diretórios para o diretório packager e execute o script packager_start.sh. A configuração de amostra escuta o endereço multicast 239.235.0.3:14000 e executa o servidor de origem local na porta 8080. A saída está configurada para ser gravada no `packager/webroot/_default_/_default_/ directory`.

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**Configurar o servidor de origem HTTP**

Consulte o documento Introdução ao servidor de origem HTTP do Primetime para obter os detalhes de configuração disponíveis aqui.

**Desinstalação do Live Packager**

Para desinstalar o empacotador, pare o empacotador e remova o diretório do empacotador do diretório Primetime.

**Desinstalação do Servidor de Origem HTTP**

Para desinstalar o Servidor de Origem HTTP, pare o Servidor de Origem HTTP e remova o diretório httporigin do Servidor de Origem HTTP no diretório Primetime.

## Adobe Primetime Offline Packager 1.4 {#adobe-primetime-offline-packager}

### Requisitos mínimos do sistema {#minimum-system-requirements-2}

**Sistemas operacionais compatíveis**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se duplo Intel Xeon® ou mais rápido)
* Sistemas operacionais de 64 bits: 4 GB de RAM (8 GB recomendado)
* Placa Ethernet de 1 Gb recomendada (várias placas de rede e 10 Gb também são suportadas)
* Disco:

   * (Disk-SAS) : Mínimo de 10 GB com 7.500 RPM
   * (Disk-SSD) : Leitura/gravação de 400MBps
   * (NAS) : Link dedicado de 1 GB

**Requisitos de software**

* Java JRE 1.7 ou posterior do Oracle.

### Instalar e configurar o Pacote Offline {#install-and-configure-offline-packager}

Para instalar o Offline Packager, siga estas etapas:

1. Baixe o software Java SE no [Oracle site](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
1. Extraia o arquivo de arquivo Adobe Primetime - Offline Packager 1.4, `Primetime- OfflinePackager-1-4-0-b206-12042014.zip`, para o disco.

Consulte o documento Introdução ao Pacote Offline do Primetime para obter os detalhes de configuração disponíveis [aqui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .