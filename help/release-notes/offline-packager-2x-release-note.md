---
title: Versões do Primetime Offline Packager 2.x
description: Novidades dos pacotes offline do Primetime 2.1 e 2.3.1
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 911549b4-45b3-400a-b903-fa1479ee862b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Versões do Primetime Offline Packager {#primetime-offline-packager-x-releases}

Novidades dos pacotes offline do Primetime 2.1 e 2.3.1

## Novidades no Primetime Offline Packager 2.3.1 (outubro de 2016)  {#what-s-new-in-primetime-offline-packager-oct}

A versão habilita o Perfil sob demanda para MPEG-DASH, adiciona suporte para o `validate` opção para a ferramenta PlaylistCreator e tem algumas correções principais para cenários Multi-DRM listados abaixo.

| **Número do problema** | **Descrição** |
|---|---|
| PTPUB-985 | AXS HLS e Amostra-AES não funcionam para a chave gerada pelo empacotador |
| PTPUB-973 | Correção de um erro no algoritmo de criptografia para algum conteúdo Widevine específico |
| PTPUB-964 | Criptografia CENC interrompida para determinados tipos de mídia em determinado player - Android TVSDK. |
| PTPUB-954 | A criptografia AES de amostra ignora o AAXS DRM por padrão/Erro lançado com a entrega de chave remota ativada. |
| PTPUB-951 | O empacotador offline não gera uma exceção quando key_file_path não é especificado com Widevine. Em vez disso, ele joga NPE. |

A documentação mais recente do Primetime Packagers está disponível em [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### Problema conhecido na versão 2.3.1 {#known-issue-in-version}

Existem os seguintes problemas nesta versão.

| **Número do problema** | **Descrição** |
|---|---|
| PTPUB-1005 | PlaylistCreator não fornece o URL correto para o arquivo .pssh no arquivo .mpd de nível de conjunto final gerado para o AXS DRM. |
| PTPUB-1001 | O PlaylistCreator deve gerar erro quando o caminho vazio é fornecido pelo parâmetro in_path |
| PTPUB-990 | Para DASH, o Packager Off-line não grava o Packager gerado IV no disco quando os parâmetros `log_vi` &amp; `iv_out_path` são especificados. |
| PTPUB-980 | Quando o arquivo de configuração é usado para empacotamento, usando o parâmetro `key_url` não remove as aspas das entradas fornecidas. |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### Requisitos mínimos do sistema {#minimum-system-requirements}

Sistemas operacionais compatíveis

* Linux CentOS 6.3 de 64 bits

Requisitos de hardware

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se Intel Xeon® duplo ou mais rápido)

* Sistemas operacionais de 64 bits: 4 GB de RAM (recomenda-se 8 GB)

* Disco rígido

(Disco-SAS): mínimo de 10 GB com 7.500 RPM

(Disco-SSD): velocidade de leitura/gravação de 400 MBps

(NAS): link dedicado de 1 GB

Requisitos de software

* Oracle Java SE 1.8 ou superior

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. Baixe o software Java SE na [site do Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
1. Extraia o arquivo morto do Adobe Primetime Offline Packager 2.3.1 chamado `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` ao disco.

### Configuração do empacotador offline 2.3.1 {#configuring-the-offline-packager}

As instruções de configuração estão disponíveis no guia de introdução do Primetime Offline Packager em [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Novidades no Primetime Offline Packager 2.1 (julho de 2015) {#what-s-new-in-primetime-offline-packager-july}

Suporte para PlayReady BuyDRM (para DASH). Para obter detalhes, consulte a Documentação de ajuda [disponível aqui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

O aprimoramento a seguir também foi feito no empacotador offline.

PTPUB-780 Adição de suporte para tag EXT-X-START

## Novidades no Primetime Offline Packager 2.0 (junho de 2015) {#what-s-new-in-primetime-offline-packager-june}

O suporte à saída de Clear DASH foi adicionado. Consulte a documentação do produto [aqui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) para obter detalhes.

Os seguintes problemas também foram corrigidos nesta versão.

* O empacotador offline PTPUB-783 agora pode manipular arquivos WebVTT vazios.
* PTPUB- 781 Artefatos na saída HLS no Chrome quando determinados ativos MP4 transcodificados são empacotados com empacotador offline para produzir saída MBR.

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### Requisitos mínimos do sistema {#minimum-system-requirements-1}

**Sistemas operacionais compatíveis**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se Intel Xeon® duplo ou mais rápido)

* Sistemas operacionais de 64 bits: 4 GB de RAM (recomenda-se 8 GB)

* Placa Ethernet de 1 Gbit recomendada (várias placas de rede e 10 Gbit também são compatíveis)

* Disco rígido

   * (Disco-SAS): mínimo de 10 GB com 7.500 RPM
   * (Disco-SSD): velocidade de leitura/gravação de 400 MBps
   * (NAS): link dedicado de 1 GB

**Requisitos de software**

* Oracle Java SE 1.8 ou superior

### Instalando o empacotador offline 2.1 {#installing-offline-packager}

1. Baixe o software Java SE na [site do Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e siga as instruções de instalação.
1. Extraia o `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`, para o disco.

### Configuração do empacotador off-line 2.1 {#configuring-the-offline-packager-1}

Consulte o documento Introdução ao Primetime Offline Packager para obter os detalhes de configuração disponíveis aqui [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
