---
description: Há algumas considerações de segurança que devem ser levadas em consideração para o TVSDK do navegador.
title: Considerações de segurança
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# Considerações de segurança{#security-considerations}

Há algumas considerações de segurança que devem ser levadas em consideração para o TVSDK do navegador.

* **Flash Player Adobe**

   * O Flash Player não permite acesso a dados que estão fora do domínio do qual o SWF se originou.

      Para permitir acesso, hospede um arquivo de política entre domínios com permissões apropriadas na raiz do servidor que está hospedando os dados. No modo Fallback do Flash no Browser TVSDK (Flash Player versão 23 e superior), você precisa do token de autorização para o seu domínio. Para gerar o token, entre em contato com seu representante de Adobe.

* **JavaScript**

   * O JavaScript segue a mesma política de origem e impede o acesso a recursos nos limites do domínio.

      Para permitir o acesso a esses recursos, o cabeçalho Controle de acesso com permissão de origem (CORS) deve ser definido nos recursos hospedados em origens diferentes do reprodutor. Opcionalmente, se o conteúdo for especificado usando intervalos de bytes, a solicitação de opções de pré-comprovação do CORS deverá indicar que essas solicitações são permitidas pela origem.

* **Navegadores e conteúdo misto**

   * Os navegadores exigem que o conteúdo criptografado AES-128 seja hospedado em Origem segura (por exemplo, HTTPS).

      Como a maioria dos navegadores não permite conteúdo misto, recomendamos que o reprodutor, o conteúdo e os ativos associados, como arquivos Key/WebVTT, também sejam hospedados sobre a Origem segura.

      >[!IMPORTANT]
      >
      >A partir da versão 2.4.5, se o reprodutor estiver hospedado por HTTPS, o TVSDK do navegador converterá as chamadas HTTP para HTTPS ao usar a tecnologia MSE.

