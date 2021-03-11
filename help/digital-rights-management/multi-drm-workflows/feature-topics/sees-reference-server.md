---
description: Uma maneira de coordenar o licenciamento e a aplicação de políticas é criar essas funções em um servidor de direito. O Adobe fornece o servidor de direito de referência SEES com o qual você pode trabalhar para criar seu próprio servidor.
title: Servidor de referência Servidor de exemplo do ExpressPlay Entitlement Server (SEES)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Servidor de referência: Exemplo de SEES (ExpressPlay Entitlement Server) {#reference-server-sample-expressplay-entitlement-server-sees}

Uma maneira de coordenar o licenciamento e a aplicação de políticas é criar essas funções em um servidor de direito. O Adobe fornece o servidor de direito de referência SEES com o qual você pode trabalhar para criar seu próprio servidor.

O SEES do servidor de referência demonstra o ExpressPlay Entitlement Service, mostrando dois serviços: direito básico baseado em tempo e direito de vinculação de dispositivo.

O SEES é criado sobre dois serviços de reprodução de linha ExpressPlay:

1. Expressar serviço de solicitação de token
1. Exprimir Serviço de Recuperação de Registros

O formato do URL para a solicitação do ExpressPlay Token assume dois formulários, um para produção, um para o ambiente de teste:

**Produção**: <span></span>https://fp-gen.{prod_domain}/hms/fp/token

**Teste**: <span></span>https://fp-gen.test.expressplay.com/hms/fp/token

O formato do URL para a recuperação do Registro do ExpressPlay tem dois formulários, um para produção, um para o ambiente de teste:

**Produção**: <span></span>https://api.{prod_domain}/cmiapi/getrecord/

**Teste**: <span></span>https://api.test.expressplay.com/cmiapi/getrecord/
