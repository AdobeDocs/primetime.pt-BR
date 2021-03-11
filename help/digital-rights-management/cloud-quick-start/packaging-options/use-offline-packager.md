---
title: Use o Primetime Offline Packager incluído
description: Use o Primetime Offline Packager incluído
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Use o Primetime Offline Packager incluído{#use-the-included-primetime-offline-packager}

O Primetime Java Packager vem pré-configurado com a maioria das configurações necessárias para empacotar conteúdo. Há apenas algumas áreas a serem atualizadas para começar.

## Atualizar propriedades do empacotador {#section_99904D35E99944A28FF43D924E516CC2}

Contexto para a tarefa atual

* Atualize as seguintes propriedades do empacotador antes de usar o arquivo de configuração para empacotar seu conteúdo:

### Propriedades do arquivo de configuração XML fornecido pelo usuário

| Nome da propriedade | Descrição |
|---|---|
| `policy_file` | caminho do arquivo de política. O Adobe deve fornecer várias políticas pré-configuradas para escolher. |
| `pkgr_pfx` | Caminho das credenciais do pacote. Você deve fornecer sua própria credencial do empacotador emitida pelo Adobe ( [!DNL .pfx]) aqui. |
| `pkgr_pfx_pwd` | Senha de credenciais do pacote. Você deve fornecer a senha para sua credencial do empacotador emitida pelo Adobe aqui. |

## Pacote usando linha de comando {#section_DFBE462679E34D62963BE201FD3321F9}

Antes de empacotar o conteúdo, verifique se você tem todas as informações necessárias fornecidas no arquivo de configuração.

* Para empacotar o conteúdo com seu arquivo de configuração, use a seguinte sintaxe na linha de comando:

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

São fornecidos arquivos de configuração de amostra para empacotar seu conteúdo para o formato HLS ou HDS, chamados de [!DNL config_hds.xml] e [!DNL config.hls.xml].

O conteúdo HDS ou HLS será enviado para a pasta [!DNL /output] no diretório do Kit de Proteção. Todos os artefatos gravados nesse diretório devem ser hospedados em um servidor da Web HTTP para serem reproduzidos.
