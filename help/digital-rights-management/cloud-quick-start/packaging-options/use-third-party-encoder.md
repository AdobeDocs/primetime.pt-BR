---
title: Usar um codificador de terceiros
description: Usar um codificador de terceiros
copied-description: true
exl-id: 565f69db-8595-4f78-b1e6-26f277a3784a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Usar um codificador de terceiros{#use-a-third-party-encoder}

Alguns clientes podem já ter um pipeline de preparação de conteúdo em vigor, usando um codificador de vídeo de hardware ou software (ou servidor Adobe Medium). Se esse for o caso, qualquer produto que possa criar conteúdo protegido por DRM do Primetime poderá empacotar conteúdo para o DRM da Primetime Cloud usando as mesmas configurações que o Kit de proteção DRM da Primetime Cloud. As informações necessárias podem ser obtidas em qualquer um dos arquivos de configuração existentes incluídos no kit: [!DNL config_hls.xml] ou [!DNL config_hds.xml].

Os itens de configuração relevantes são:

* URL do Servidor de Licença
* URL do servidor de chave
* Certificado do servidor de licenças
* Certificado de transporte
