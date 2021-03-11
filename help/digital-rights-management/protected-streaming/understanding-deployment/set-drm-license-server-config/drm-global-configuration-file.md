---
description: O arquivo de configuração flashaccess-global.xml inclui configurações que se aplicam a todos os locatários do servidor de licenças.
title: Arquivo de configuração global
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# Arquivo de configuração global{#global-configuration-file}

O arquivo de configuração flashaccess-global.xml inclui configurações que se aplicam a todos os locatários do servidor de licenças.

Você deve colocar o arquivo de configuração no diretório [!DNL LicenseServer.ConfigRoot].

Consulte o diretório [!DNL configs] para obter um exemplo de um arquivo de configuração global.

O arquivo de configuração global inclui:

* Armazenamento em cache — Controla o armazenamento em cache de arquivos de configuração na memória.

   Consulte *Atualizando arquivos de configuração* para obter informações sobre as configurações de armazenamento em cache.
* Registro — Especifica o nível de registro e a frequência com que os arquivos de log são rolados.
* Senha do HSM — Obrigatório somente se um HSM for usado para armazenar credenciais do servidor.

Consulte os comentários no arquivo de configuração global de exemplo localizado no Primetime DRM `<DVD>`\Adobe Primetime DRM Server for Protected Streaming\configs para obter mais detalhes.
