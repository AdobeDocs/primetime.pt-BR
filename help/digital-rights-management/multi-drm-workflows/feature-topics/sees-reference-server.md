---
description: Uma maneira de coordenar o licenciamento e a aplicação de políticas é criar essas funções em um servidor de direito. A Adobe fornece o servidor de direito de referência SEES com o qual você pode trabalhar para criar seu próprio servidor.
seo-description: Uma maneira de coordenar o licenciamento e a aplicação de políticas é criar essas funções em um servidor de direito. A Adobe fornece o servidor de direito de referência SEES com o qual você pode trabalhar para criar seu próprio servidor.
seo-title: Servidor de referência Servidor de direito ExpressPlay (SEES) de amostra
title: Servidor de referência Servidor de direito ExpressPlay (SEES) de amostra
uuid: 99e42f76-7730-42fc-a9a9-f6396ac12c02
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Servidor de referência: Servidor de direito ExpressPlay de amostra (SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

Uma maneira de coordenar o licenciamento e a aplicação de políticas é criar essas funções em um servidor de direito. A Adobe fornece o servidor de direito de referência SEES com o qual você pode trabalhar para criar seu próprio servidor.

O servidor de referência SEES demonstra o ExpressPlay Entitlement Service, mostrando dois serviços: direito básico baseado em tempo e direito de vinculação de dispositivo.

O SEES foi desenvolvido sobre dois serviços ExpressPlay Fairplay:

1. Serviço de Solicitação de Token de Expressplay
1. Serviço de Recuperação de Registros Expressplay

O formato de URL para a solicitação do ExpressPlay Token utiliza dois formulários, um para produção, outro para o ambiente de teste:

**Produção**:<span></span>https://fp-gen.{prod_domain}/hms/fp/token

**Teste**:<span></span>https://fp-gen.test.expressplay.com/hms/fp/token

O formato de URL para a recuperação do ExpressPlay Record tem dois formulários, um para produção, outro para o ambiente de teste:

**Produção**:<span></span>https://api.{prod_domain}/cmiapi/getrecord/

**Teste**:<span></span>https://api.test.expressplay.com/cmiapi/getrecord/
