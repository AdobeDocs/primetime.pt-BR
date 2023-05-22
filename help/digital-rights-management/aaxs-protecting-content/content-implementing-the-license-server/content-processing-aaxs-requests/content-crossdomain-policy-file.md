---
title: Arquivo de política entre domínios
description: Arquivo de política entre domínios
copied-description: true
exl-id: dbe16692-cdf7-4a91-9303-8afc2d487112
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Arquivo de política entre domínios {#crossdomain-policy-file}

Se o servidor de licença estiver hospedado em um domínio diferente do SWF de reprodução de vídeo, será necessário um arquivo de política entre domínios (crossdomain.xml) para permitir que o SWF solicite licenças do servidor de licença. Um arquivo de política entre domínios é um arquivo XML que fornece uma maneira para o servidor indicar que seus dados e documentos estão disponíveis para arquivos SWF enviados de outros domínios. Qualquer arquivo SWF veiculado a partir de um domínio especificado no arquivo de política entre domínios do servidor de licenças tem permissão para acessar dados ou ativos desse servidor de licenças.

A Adobe recomenda que os desenvolvedores sigam as práticas recomendadas ao implantar o arquivo de política entre domínios, permitindo somente que domínios confiáveis acessem o servidor de licença e limitando o acesso ao subdiretório de licença no servidor da Web.

Para obter mais informações sobre arquivos de política entre domínios, consulte os seguintes locais:

* Controles de site (arquivos de política)
* Especificação de arquivo de política entre domínios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
