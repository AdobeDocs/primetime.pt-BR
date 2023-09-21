---
description: Há algumas considerações de segurança que devem ser levadas em conta no TVSDK do navegador.
title: Considerações de segurança
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Considerações de segurança{#security-considerations}

Há algumas considerações de segurança que devem ser levadas em conta no TVSDK do navegador.

* **Flash Player Adobe**

   * O Flash Player não permite acesso a dados que residem fora do domínio do qual o SWF se originou.

     Para permitir o acesso, hospede um arquivo de política entre domínios com permissões apropriadas na raiz do servidor que está hospedando os dados. No modo Flash Fallback, no TVSDK do navegador (Flash Player versão 23 e superior), é necessário o token de autorização para o seu domínio. Para gerar o token, entre em contato com o representante da Adobe.

* **JavaScript**

   * O JavaScript segue a mesma política de origem e impede o acesso a recursos entre limites de domínio.

     Para permitir o acesso a esses recursos, o cabeçalho CORS (Access-Control-Allow-Origin) deve ser definido nos recursos que estão hospedados em origens diferentes do reprodutor. Opcionalmente, se o conteúdo for especificado usando intervalos de bytes, a solicitação de opções de pré-voo do CORS deve indicar que essas solicitações são permitidas pela origem.

* **Navegadores e conteúdo misto**

   * Os navegadores exigem que o conteúdo criptografado AES-128 seja hospedado no Origin seguro (por exemplo, HTTPS).

     Como a maioria dos navegadores não permite conteúdo misto, recomendamos que o reprodutor, o conteúdo e os ativos associados, como arquivos Key/ WebVTT, também sejam hospedados no Origin seguro.

     >[!IMPORTANT]
     >
     >A partir da versão 2.4.5, se o reprodutor estiver hospedado por HTTPS, o TVSDK do navegador converterá as chamadas HTTP em HTTPS ao usar a tecnologia MSE.
