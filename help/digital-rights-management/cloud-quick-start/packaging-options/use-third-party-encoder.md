---
seo-title: Usar um codificador de terceiros
title: Usar um codificador de terceiros
uuid: 8649303c-b8e6-4c02-a8ad-5734af850bfe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Usar um codificador de terceiros{#use-a-third-party-encoder}

Alguns clientes podem já ter um pipeline de preparação de conteúdo em vigor, usando um codificador de vídeo de hardware ou software (ou Adobe Media Server). Se esse for o caso, qualquer produto que possa criar conteúdo protegido por DRM Primetime pode disponibilizar conteúdo para o DRM da Primetime Cloud usando as mesmas configurações do Kit de proteção DRM da Primetime Cloud. As informações necessárias podem ser obtidas de qualquer um dos arquivos de configuração existentes incluídos no kit: [!DNL config_hls.xml] ou [!DNL config_hds.xml].

Os itens de configuração relevantes são:

* URL do servidor de licenças
* URL do servidor de chaves
* Certificado do servidor de licença
* Certificado de transporte

