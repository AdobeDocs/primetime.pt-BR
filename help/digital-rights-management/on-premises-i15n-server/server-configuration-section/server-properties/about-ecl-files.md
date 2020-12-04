---
seo-title: Sobre arquivos ECI
title: Sobre arquivos ECI
uuid: 124d8ab1-933b-4a1b-992a-919f3d799460
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Sobre os arquivos ECI{#about-eci-files}

Além das CRLs, também é necessário atualizar periodicamente os arquivos ECI (Embedded Common Interface, interface comum incorporada). Sempre que o Adobe adicionar suporte para uma nova plataforma de cliente Primetime DRM (por exemplo: iOS, Android, Windows Flash Player, etc.), um novo registro ECI é criado. Para suportar a individualização deste cliente, é necessário que exista um registro ECI correspondente no servidor de individualização.

Como o lançamento de novos clientes Primetime DRM não é muito frequente, o Adobe lançará dados ECI atualizados conforme necessário. Periodicamente, o Adobe coletará arquivos ECI e os hospedará no local abaixo para distribuição:

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

O arquivo zip será renomeado para conter a data de arquivamento e o resumo SHA-256:

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

Por exemplo:

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

Você deve verificar periodicamente o local acima para ver os arquivos ECI atualizados.

Execute o seguinte processo de instalação após o download:

1. Observe o resumo SHA-256 e recalcule-o usando o OpenSSL ou uma ferramenta equivalente.
1. Compare-o com o especificado no nome do arquivo.
1. Renomeie o arquivo para [!DNL ECI.zip].
1. Descompacte o diretório [!DNL ECI].
1. Substitua o diretório ECI antigo pelo novo.
1. Reinicie o servidor de individualização.

