---
description: O arquivo de configuração flashaccess-global.xml inclui configurações que se aplicam a todos os locatários do servidor de licenças.
seo-description: O arquivo de configuração flashaccess-global.xml inclui configurações que se aplicam a todos os locatários do servidor de licenças.
seo-title: Arquivo de configuração global
title: Arquivo de configuração global
uuid: 294d6cff-be07-4b4b-8aa6-943044a1c56f
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Arquivo de configuração global{#global-configuration-file}

O arquivo de configuração flashaccess-global.xml inclui configurações que se aplicam a todos os locatários do servidor de licenças.

Você deve colocar o arquivo de configuração no [!DNL LicenseServer.ConfigRoot] diretório.

Consulte o [!DNL configs] diretório para obter um exemplo de um arquivo de configuração global.

O arquivo de configuração global inclui:

* Cache — Controla o cache de arquivos de configuração na memória.

   Consulte *Atualização de arquivos* de configuração para obter informações sobre as configurações de cache.
* Registro — Especifica o nível de registro e a frequência de rolagem dos arquivos de registro.
* Senha HSM — Necessário somente se um HSM for usado para armazenar credenciais de servidor.

Consulte os comentários no arquivo de configuração global de exemplo que está localizado no Primetime DRM `<DVD>`\Adobe Primetime DRM Server for Protected Streaming\configs para obter mais detalhes.
