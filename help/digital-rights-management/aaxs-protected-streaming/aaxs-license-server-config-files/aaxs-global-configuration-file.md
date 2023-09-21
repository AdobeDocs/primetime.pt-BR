---
title: Arquivo de configuração global
description: Arquivo de configuração global
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Arquivo de configuração global{#global-configuration-file}

O arquivo de configuração flashaccess-global.xml contém definições que se aplicam a todos os locatários do servidor de licenças. Este arquivo deve estar localizado em *LicenseServer.ConfigRoot*. Consulte o diretório de configurações para obter um exemplo de arquivo de configuração global. O arquivo de configuração global inclui o seguinte:

* Armazenamento em cache — Controla o armazenamento em cache de arquivos de configuração na memória. Para obter uma explicação das configurações de armazenamento em cache, consulte &quot;Atualizando arquivos de configuração&quot;.
* Registro — Especifica o nível de registro e a frequência de rollhamento dos arquivos de registro.
* Senha HSM — Necessária somente se um HSM for usado para armazenar credenciais do servidor.

Consulte os comentários no arquivo de configuração global de exemplo localizado em `<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs` para obter mais detalhes.
