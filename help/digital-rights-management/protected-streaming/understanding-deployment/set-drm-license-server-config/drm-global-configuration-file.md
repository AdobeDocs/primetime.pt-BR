---
description: O arquivo de configuração flashaccess-global.xml inclui definições que se aplicam a todos os locatários do servidor de licenças.
title: Arquivo de configuração global
exl-id: 3e74bce6-1634-469f-9d02-1121e9d50687
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Arquivo de configuração global{#global-configuration-file}

O arquivo de configuração flashaccess-global.xml inclui definições que se aplicam a todos os locatários do servidor de licenças.

Você deve colocar o arquivo de configuração no [!DNL LicenseServer.ConfigRoot] diretório.

Consulte a [!DNL configs] para obter um exemplo de um arquivo de configuração global.

O arquivo de configuração global inclui:

* Armazenamento em cache — Controla o armazenamento em cache de arquivos de configuração na memória.

   Consulte *Atualização de arquivos de configuração* para obter informações sobre as configurações de armazenamento em cache.
* Registro — Especifica o nível de registro e a frequência de rollhamento dos arquivos de registro.
* Senha HSM — Necessária somente se um HSM for usado para armazenar credenciais do servidor.

Consulte os comentários no arquivo de configuração global de exemplo localizado no Primetime DRM `<DVD>`\Adobe Primetime DRM Server para Protected Streaming\configs para obter mais detalhes.
