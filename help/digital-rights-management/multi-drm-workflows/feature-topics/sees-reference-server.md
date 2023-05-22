---
description: Uma maneira de coordenar o licenciamento e a aplicação de políticas é incorporar essas funções a um servidor de direitos. O Adobe fornece o servidor de direitos de referência do SEES com o qual você pode trabalhar para criar seu próprio servidor.
title: Servidor de Referência - Exemplo de ExpressPlay Entitlement Server (SEES)
exl-id: aa5b63f4-dffc-4808-8aa6-6b8f63df592c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Servidor de Referência: Exemplo de Servidor de Direitos ExpressPlay (SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

Uma maneira de coordenar o licenciamento e a aplicação de políticas é incorporar essas funções a um servidor de direitos. O Adobe fornece o servidor de direitos de referência do SEES com o qual você pode trabalhar para criar seu próprio servidor.

O servidor de referência SEES demonstra o ExpressPlay Entitlement Service, mostrando dois serviços: direito baseado em tempo básico e direito de ligação de dispositivo.

O SEES é construído sobre dois ExpressPlay Fairplay Services:

1. Serviço de solicitação de token do Expressplay
1. Serviço de Recuperação de Registro de Expressão

O formato do URL para a solicitação do token ExpressPlay assume dois formatos, um para produção e outro para o ambiente de teste:

**Produção**: ht<span></span>tps://fp-gen.{prod_domain}/hms/fp/token

**Teste**: ht<span></span>tps://fp-gen.test.expressplay.com/hms/fp/token

O formato de URL para recuperação de Registro ExpressPlay assume dois formatos, um para produção e um para o ambiente de teste:

**Produção**: ht<span></span>tps://api.{prod_domain}/cmiapi/getrecord/

**Teste**: ht<span></span>tps://api.test.expressplay.com/cmiapi/getrecord/
