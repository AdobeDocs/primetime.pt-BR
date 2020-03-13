---
title: Versões do Primetime Offline Packager 2.x
seo-title: Versões do Primetime Offline Packager 2.x
description: Novidades das versões 2.1 e 2.3.1 do Primetime Offline Packager
seo-description: Novidades das versões 2.1 e 2.3.1 do Primetime Offline Packager
uuid: 01926a10-890d-477d-b832-e22847d957e0
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: 933a0711-846a-4bb7-bf51-b300822a93d4
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Versões do Primetime Offline Packager {#primetime-offline-packager-x-releases}

Novidades das versões 2.1 e 2.3.1 do Primetime Offline Packager

## Novidades do Primetime Offline Packager 2.3.1 (Out. 2016) {#what-s-new-in-primetime-offline-packager-oct}

A versão habilita o Perfil sob demanda para MPEG-DASH, adiciona suporte para a `validate` opção da ferramenta PlaylistCreator e tem poucas correções importantes para os cenários Multi-DRM listados abaixo.

| **Número do problema** | **Descrição** |
|---|---|
| PTPUB-985 | HLS AAXS e Sample-AES não funcionam para chave gerada pelo empacotador |
| PTPUB-973 | Corrigido o erro no algoritmo de criptografia para algum conteúdo específico do Widevine |
| PTPUB-964 | Criptografia CENC interrompida para certos tipos de mídia em determinado player - Android TVSDK. |
| PTPUB-954 | A criptografia AES de amostra ignora o DRM AXS por padrão / Erro lançado com a entrega de chave remota ativada. |
| PTPUB-951 | O empacotador offline não gera exceção quando key_file_path não é especificado com o Widevine. Em vez disso, joga o NPE. |

A documentação mais recente do Primetime Packagers está disponível em [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### Problema conhecido na versão 2.3.1 {#known-issue-in-version}

Os seguintes problemas existem nesta versão.

| **Número do problema** | **Descrição** |
|---|---|
| PTPUB-1005 | O PlaylistCreator não fornece o URL correto para o arquivo .pssh no arquivo .mpd de nível de conjunto final gerado para o DRM AXS. |
| PTPUB-1001 | O PlaylistCreator deve gerar um erro quando um caminho vazio é fornecido através do parâmetro in_path |
| PTPUB-990 | Para DASH, o Offline Packager não grava o empacotador gerado por IV em disco quando os parâmetros `log_vi` e `iv_out_path` são especificados. |
| PTPUB-980 | Quando o arquivo de configuração é usado para empacotamento, o uso do parâmetro `key_url` não remove as aspas das entradas fornecidas. |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### Requisitos mínimos do sistema {#minimum-system-requirements}

Sistemas operacionais suportados

* Linux CentOS 6.3 64 bits

Requisitos de hardware

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se Intel Xeon® dual ou mais veloz)

* Sistemas operacionais de 64 bits: 4 GB de RAM (8 GB recomendado)

* Disco rígido

(Disco-SAS): Mínimo de 10 GB com 7,5 K RPM

(Disco-SSD): Velocidade de leitura/gravação de 400 MBps

(NAS): Link dedicado de 1 GB

Requisitos de software

* Oracle Java SE 1.8 ou superior

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. Baixe o software Java SE do site [](https://www.oracle.com/technetwork/java/javase/downloads/index.html) Oracle e siga as instruções de instalação.
1. Extraia o arquivo de arquivo do Adobe Primetime Offline Packager 2.3.1 nomeado `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` para o disco.

### Configuração do Offline Packager 2.3.1 {#configuring-the-offline-packager}

As instruções de configuração estão disponíveis no guia de Introdução do Primetime Offline Packager em [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Novidades do Primetime Offline Packager 2.1 (julho de 2015) {#what-s-new-in-primetime-offline-packager-july}

Suporte para PlayReady BuyDRM (para DASH). Para obter detalhes, consulte a Documentação de ajuda [disponível aqui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

As melhorias a seguir também foram feitas no empacotador offline.

PTPUB-780 Adicionado suporte para a tag EXT-X-START

## Novidades do Primetime Offline Packager 2.0 (junho de 2015) {#what-s-new-in-primetime-offline-packager-june}

Foi adicionado o suporte de saída Clear DASH. Consulte a documentação do produto [aqui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) para obter detalhes.

Os seguintes problemas também foram corrigidos nesta versão.

* O PTPUB-783 Offline Packager agora pode lidar com arquivos WebVTT vazios.
* PTPUB- 781 Artefatos na saída HLS no Chrome quando determinados ativos MP4 transcodificados são empacotados com empacotador offline para produzir saída MBR.

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### Requisitos mínimos do sistema {#minimum-system-requirements-1}

**Sistemas operacionais suportados**

* Linux CentOS 6.3 64 bits

**Requisitos de hardware**

* Processador Intel® Pentium® 4 de 3,2 GHz (recomenda-se Intel Xeon® dual ou mais veloz)

* Sistemas operacionais de 64 bits: 4 GB de RAM (8 GB recomendado)

* Placa Ethernet de 1 Gb recomendada (várias placas de rede e 10 Gb também são suportadas)

* Disco rígido

   * (Disco-SAS): Mínimo de 10 GB com 7,5 K RPM
   * (Disco-SSD): Velocidade de leitura/gravação de 400 MBps
   * (NAS): Link dedicado de 1 GB

**Requisitos de software**

* Oracle Java SE 1.8 ou superior

### Instalação do Offline Packager 2.1 {#installing-offline-packager}

1. Baixe o software Java SE do site [](https://www.oracle.com/technetwork/java/javase/downloads/index.html) Oracle e siga as instruções de instalação.
1. Extraia o `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`, para o seu disco.

### Configuração do Offline Packager 2.1 {#configuring-the-offline-packager-1}

Consulte o documento Introdução do Primetime Offline Packager para obter os detalhes de configuração disponíveis em [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página Aprendizagem e suporte [do](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.