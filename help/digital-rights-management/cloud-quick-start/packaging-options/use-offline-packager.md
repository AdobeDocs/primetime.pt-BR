---
title: Usar o Primetime Offline Packager incluído
description: Usar o Primetime Offline Packager incluído
copied-description: true
exl-id: 6a1d0dc3-8906-4de5-8351-890c1cf31efd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Usar o Primetime Offline Packager incluído{#use-the-included-primetime-offline-packager}

Seu Primetime Java Packager vem pré-configurado com a maioria das configurações necessárias para criar pacotes de conteúdo. Há apenas algumas áreas a serem atualizadas para começar.

## Atualizar propriedades do empacotador {#section_99904D35E99944A28FF43D924E516CC2}

Contexto da tarefa atual

* Atualize as seguintes propriedades do empacotador antes de usar o arquivo de configuração para empacotar seu conteúdo:

### Propriedades do Arquivo de Configuração XML Fornecido pelo Usuário

| Nome da propriedade | Descrição |
|---|---|
| `policy_file` | caminho do arquivo de política. O Adobe fornecerá várias políticas pré-configuradas para a escolha. |
| `pkgr_pfx` | Caminho de credenciais do empacotador. Você deve fornecer sua própria credencial de empacotador emitida por Adobe ( [!DNL .pfx]) aqui. |
| `pkgr_pfx_pwd` | Senha das credenciais do empacotador. Você deve fornecer a senha para a credencial do empacotador emitida pelo Adobe aqui. |

## Empacotar usando linha de comando {#section_DFBE462679E34D62963BE201FD3321F9}

Antes de empacotar o conteúdo, verifique se todas as informações necessárias foram fornecidas no arquivo de configuração.

* Para criar um pacote de conteúdo com seu arquivo de configuração, use a seguinte sintaxe na linha de comando:

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

São fornecidos exemplos de arquivos de configuração para empacotar seu conteúdo para o formato HLS ou HDS, chamados de [!DNL config_hds.xml] e [!DNL config.hls.xml].

O conteúdo HDS ou HLS será enviado para o [!DNL /output] pasta no diretório do Kit de proteção. Todos os artefatos gravados nesse diretório devem ser hospedados em um servidor Web HTTP para serem reproduzidos.
