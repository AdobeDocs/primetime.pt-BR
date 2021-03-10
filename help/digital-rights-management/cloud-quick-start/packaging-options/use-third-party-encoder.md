---
title: Usar um codificador de terceiros
description: Usar um codificador de terceiros
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Usar um codificador de terceiros{#use-a-third-party-encoder}

Alguns clientes podem já ter um pipeline de preparação de conteúdo em vigor, usando um codificador de vídeo de hardware ou software (ou Adobe Medium Server). Se esse for o caso, qualquer produto que possa criar conteúdo protegido por DRM do Primetime pode empacotar conteúdo para DRM da Primetime Cloud usando as mesmas configurações que o Kit de proteção DRM da Primetime Cloud. As informações necessárias podem ser obtidas de qualquer um dos arquivos de configuração existentes incluídos no kit: [!DNL config_hls.xml] ou [!DNL config_hds.xml].

Os itens de configuração relevantes são:

* URL do Servidor de Licenças
* URL do servidor-chave
* Certificado do Servidor de Licenças
* Certificado de transporte

