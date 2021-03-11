---
title: Versões 2.x do Primetime Offline Packager 2
description: Novidades das versões 2.1 e 2.3.1 do Primetime Offline Packager
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# Versões do Primetime Offline Packager {#primetime-offline-packager-x-releases}

Novidades das versões 2.1 e 2.3.1 do Primetime Offline Packager

## Novidades do Primetime Offline Packager 2.3.1 (outubro de 2016) {#what-s-new-in-primetime-offline-packager-oct}

A versão habilita o Perfil sob demanda para MPEG-DASH, adiciona suporte para a opção `validate` para a ferramenta PlaylistCreator e tem poucas correções importantes para cenários de Multi-DRM listados abaixo.

| **Número da emissão** | **Descrição** |
|---|---|
| PTPUB-985 | HLS AAXS e Sample-AES não funcionam para chave gerada por pacote |
| PTPUB-973 | Correção de um erro no algoritmo de criptografia para um conteúdo específico da Widevine |
| PTPUB-964 | Criptografia CENC corrompida para determinados tipos de mídia em determinado reprodutor - Android TVSDK. |
| PTPUB-954 | A criptografia AES de amostra ignora o DRM AXS por padrão / Erro lançado com o delivery de chave remota habilitado. |
| PTPUB-951 | O empacotador offline não lança exceção quando key_file_path não é especificado com Widevine. Em vez disso, joga o NPE. |

A documentação mais recente dos Pacotes do Primetime está disponível em [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### Problema conhecido na versão 2.3.1 {#known-issue-in-version}

Os seguintes problemas existem nesta versão.

| **Número da emissão** | **Descrição** |
|---|---|
| PTPUB-1005 | O PlaylistCreator não fornece o URL correto para o arquivo .pssh no arquivo .mpd de nível de conjunto final gerado para o DRM AAXS. |
| PTPUB-1001 | O PlaylistCreator deve gerar erro quando o caminho vazio é fornecido por meio do parâmetro in_path |
| PTPUB-990 | Para DASH, o Pacote Offline não grava o empacotador gerado IV no disco quando os parâmetros `log_vi` e `iv_out_path` são especificados. |
| PTPUB-980 | Quando o arquivo de configuração é usado para empacotamento, o uso do parâmetro `key_url` não remove as aspas das entradas fornecidas. |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### Requisitos mínimos do sistema {#minimum-system-requirements}

Sistemas operacionais compatíveis

* Linux CentOS 6.3 de 64 bits

Requisitos de hardware

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se duplo Intel Xeon® ou mais rápido)

* Sistemas operacionais de 64 bits: 4 GB de RAM (8 GB recomendado)

* Disco rígido

(Disk-SAS): Mínimo de 10 GB com 7.500 RPM

(Disk-SSD): Velocidade de leitura/gravação de 400MBps

(NAS): Link dedicado de 1 GB

Requisitos de software

* Oracle Java SE 1.8 ou superior

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. Baixe o software Java SE no [Oracle site](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
1. Extraia o arquivo de arquivo do Adobe Primetime Offline Packager 2.3.1 chamado `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` para o disco.

### Configurar o Pacote Offline 2.3.1 {#configuring-the-offline-packager}

As instruções de configuração estão disponíveis no guia de Introdução do Primetime Offline Packager em [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Novidades do Primetime Offline Packager 2.1 (julho de 2015) {#what-s-new-in-primetime-offline-packager-july}

Suporte para PlayReady BuyDRM (para DASH). Para obter detalhes, consulte a Documentação da Ajuda [disponível aqui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

O seguinte aprimoramento também foi feito ao empacotador offline.

PTPUB-780 Adicionado suporte para a tag EXT-X-START

## Novidades do Primetime Offline Packager 2.0 (junho de 2015) {#what-s-new-in-primetime-offline-packager-june}

Adição do suporte a saída Clear DASH. Consulte a documentação do produto [aqui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) para obter detalhes.

Os seguintes problemas também foram corrigidos nesta versão.

* O PTPUB-783 Offline Packager agora pode manipular arquivos WebVTT vazios.
* PTPUB- 781 Artefatos na saída HLS no Chrome quando determinados ativos MP4 transcodificados são empacotados com empacotador offline para produzir saída MBR.

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### Requisitos mínimos do sistema {#minimum-system-requirements-1}

**Sistemas operacionais compatíveis**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se duplo Intel Xeon® ou mais rápido)

* Sistemas operacionais de 64 bits: 4 GB de RAM (8 GB recomendado)

* Placa Ethernet de 1 Gb recomendada (várias placas de rede e 10 Gb também são suportadas)

* Disco rígido

   * (Disk-SAS): Mínimo de 10 GB com 7.500 RPM
   * (Disk-SSD): Velocidade de leitura/gravação de 400MBps
   * (NAS): Link dedicado de 1 GB

**Requisitos de software**

* Oracle Java SE 1.8 ou superior

### Instalar o Pacote Offline 2.1 {#installing-offline-packager}

1. Baixe o software Java SE no [Oracle site](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
1. Extraia o `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip` para o disco.

### Configurar o Pacote Offline 2.1 {#configuring-the-offline-packager-1}

Consulte o documento Introdução ao Primetime Offline Packager para obter os detalhes de configuração disponíveis aqui [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .