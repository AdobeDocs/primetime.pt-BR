---
title: Sobre os arquivos ECI
description: Sobre os arquivos ECI
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Sobre os arquivos ECI{#about-eci-files}

Além das CRLs, você também precisa atualizar periodicamente os arquivos ECI (Embedded Common Interface). Sempre que o Adobe adiciona suporte para uma nova plataforma de cliente DRM do Primetime (por exemplo: iOS, Android, Windows FlashPlayer etc.), um novo registro ECI é criado. Para dar suporte à individualização desse cliente, um registro ECI correspondente precisa estar presente no Servidor de individualização.

Como o lançamento de novos clientes DRM do Primetime não é muito frequente, o Adobe lançará dados ECI atualizados conforme necessário. Periodicamente, o Adobe coletará arquivos ECI e os hospedará no local abaixo para distribuição:

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

A variável [!DNL Latest.txt] arquivo conterá o URL para o arquivo de distribuição CRL mais recente.

O Adobe criará o arquivo zip ECI da maneira descrita abaixo:

Estrutura da pasta:

```
ECI\*
```

O conteúdo da pasta será compactado recursivamente:

```
zip -R ECI ECI.zip
```

Um resumo do OpenSSL SHA-256 será calculado sobre o arquivo zip:

```
openssl dgst -sha256 -hex ECI.zip
```

O arquivo zip será renomeado para conter a data de arquivamento, bem como o resumo SHA-256:

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

Por exemplo:

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

Você deve verificar periodicamente se há arquivos ECI atualizados no local acima.

Execute o seguinte processo para instalação após o download:

1. Observe o resumo SHA-256 e recalcule-o usando o OpenSSL ou uma ferramenta equivalente.
1. Comparar com o especificado no nome do arquivo.
1. Renomeie o arquivo para [!DNL ECI.zip].
1. Descompacte o [!DNL ECI] diretório.
1. Substitua o diretório ECI antigo pelo novo.
1. Reinicie o servidor de Individualização.
