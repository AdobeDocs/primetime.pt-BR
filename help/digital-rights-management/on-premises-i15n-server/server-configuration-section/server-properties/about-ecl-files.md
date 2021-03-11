---
title: Sobre arquivos ECI
description: Sobre arquivos ECI
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Sobre arquivos ECI{#about-eci-files}

Além das CRLs, você também precisa atualizar periodicamente os arquivos ECI (Embedded Common Interface, interface comum incorporada). Sempre que o Adobe adiciona suporte para uma nova plataforma de cliente Primetime DRM (por exemplo: iOS, Android, Windows FlashPlayer etc.), um novo registro ECI é criado. Para dar suporte à individualização desse cliente, é necessário que um registro de ECI correspondente esteja presente no servidor de individualização.

Como o lançamento de novos clientes DRM do Primetime não é muito frequente, o Adobe lançará dados ECI atualizados conforme necessário. Periodicamente, o Adobe coletará arquivos ECI e os hospedará no local abaixo para distribuição:

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

O arquivo [!DNL Latest.txt] conterá o URL para o arquivo de distribuição CRL mais recente.

O Adobe criará o arquivo zip ECI da maneira descrita abaixo:

Estrutura da pasta:

```
ECI\*
```

O conteúdo da pasta será compactado recursivamente:

```
zip -R ECI ECI.zip
```

Um resumo OpenSSL SHA-256 será calculado do arquivo zip:

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

Você deve verificar periodicamente o local acima para arquivos ECI atualizados.

Execute o seguinte processo de instalação após download:

1. Observe o resumo SHA-256 e recalcule-o usando OpenSSL ou uma ferramenta equivalente.
1. Compare-o com o especificado no nome do arquivo.
1. Renomeie o arquivo para [!DNL ECI.zip].
1. Descompacte o diretório [!DNL ECI].
1. Substitua o diretório ECI antigo pelo novo.
1. Reinicie o servidor de individualização.

