---
description: Há algumas considerações de segurança que devem ser observadas para o TVSDK do navegador.
seo-description: Há algumas considerações de segurança que devem ser observadas para o TVSDK do navegador.
seo-title: Considerações de segurança
title: Considerações de segurança
uuid: 78edf2b0-363c-4ab6-b588-ab4748ee6096
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Considerações de segurança{#security-considerations}

Há algumas considerações de segurança que devem ser observadas para o TVSDK do navegador.

* **Flash Player Adobe**

   * O Flash Player não permite acesso a dados que residem fora do domínio de onde o SWF se originou.

      Para permitir acesso, hospede um arquivo de política entre domínios com permissões apropriadas na raiz do servidor que está hospedando os dados. No modo Fallback de Flash no TVSDK do navegador (Flash Player versão 23 e superior), você precisa do token de autorização para seu domínio. Para gerar o token, entre em contato com seu representante de Adobe.

* **JavaScript**

   * O JavaScript segue a mesma política de origem e impede o acesso aos recursos pelos limites do domínio.

      Para permitir o acesso a esses recursos, o cabeçalho Access-Control-Allow-Origem (CORS) deve ser definido nos recursos hospedados em origens diferentes do player. Como opção, se o conteúdo for especificado usando intervalos de bytes, a solicitação de opções de pré-voo do CORS deverá indicar que essas solicitações são permitidas pela origem.

* **Navegadores e conteúdo misto**

   * Os navegadores exigem que o conteúdo criptografado AES-128 seja hospedado em Origem segura (por exemplo, HTTPS).

      Como a maioria dos navegadores não permite conteúdo misto, recomendamos que o player, o conteúdo e os ativos associados, como os arquivos Key/WebVTT, também sejam hospedados em Origem segura.

      >[!IMPORTANT]
      >
      >A partir da versão 2.4.5, se o player estiver hospedado em HTTPS, o TVSDK do navegador converterá as chamadas HTTP em HTTPS ao usar a tecnologia MSE.

