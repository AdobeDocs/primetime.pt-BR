---
seo-title: Usar o Primetime Offline Packager incluído
title: Usar o Primetime Offline Packager incluído
uuid: 16b535a9-81b5-43bc-9e42-a64eb6649d9a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Usar o Primetime Offline Packager incluído{#use-the-included-primetime-offline-packager}

Seu Primetime Java Packager vem pré-configurado com a maioria das configurações necessárias para disponibilizar conteúdo. Há apenas algumas áreas a serem atualizadas para começar.

## Atualizar propriedades do Packager {#section_99904D35E99944A28FF43D924E516CC2}

Contexto para a tarefa atual

* Atualize as seguintes propriedades do empacotador antes de usar o arquivo de configuração para empacotar seu conteúdo:

### Propriedades do arquivo de configuração XML fornecido pelo usuário

| Nome da propriedade | Descrição |
|---|---|
| `policy_file` | caminho do arquivo de política. A Adobe fornecerá várias políticas pré-configuradas para escolha. |
| `pkgr_pfx` | Caminho das credenciais do Packager. Você deve fornecer sua própria credencial de empacotador ( [!DNL .pfx]) emitida pela Adobe aqui. |
| `pkgr_pfx_pwd` | Senha de credenciais do Packager. Você deve fornecer a senha para sua credencial do empacotador emitida pela Adobe aqui. |

## Pacote usando linha de comando {#section_DFBE462679E34D62963BE201FD3321F9}

Antes de empacotar o conteúdo, verifique se você tem todas as informações necessárias fornecidas no arquivo de configuração.

* Para empacotar o conteúdo com o arquivo de configuração, use a seguinte sintaxe na linha de comando:

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

Os arquivos de configuração de amostra para disponibilizar o conteúdo no formato HLS ou HDS são fornecidos, nomeados [!DNL config_hds.xml] e [!DNL config.hls.xml].

O conteúdo HDS ou HLS será enviado para a [!DNL /output] pasta no diretório do Kit de proteção. Todos os artefatos gravados neste diretório devem ser hospedados em um servidor da Web HTTP para serem reproduzidos.
