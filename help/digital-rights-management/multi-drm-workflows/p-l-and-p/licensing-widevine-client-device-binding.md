---
description: Em alguns casos, você pode querer restringir a reprodução de conteúdo em vários dispositivos quando o conteúdo for comprado ou alugado. Se o cliente estiver usando o Expressplay, isso pode ser feito usando as APIs do Express para vincular o token do Expressplay do usuário à máquina do usuário.
seo-description: Em alguns casos, você pode querer restringir a reprodução de conteúdo em vários dispositivos quando o conteúdo for comprado ou alugado. Se o cliente estiver usando o Expressplay, isso pode ser feito usando as APIs do Express para vincular o token do Expressplay do usuário à máquina do usuário.
seo-title: Vínculo de dispositivo
title: Vínculo de dispositivo
uuid: 351fa33c-4226-4ed5-829c-56b563166fec
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Vínculo de dispositivo{#device-binding}

Em alguns casos, você pode querer restringir a reprodução de conteúdo em vários dispositivos quando o conteúdo for comprado ou alugado. Se o cliente estiver usando o Expressplay, isso pode ser feito usando as APIs do Express para vincular o token do Expressplay do usuário à máquina do usuário.

Você pode usar as APIs da seguinte maneira.

1. Gerar um cookie.
1. Envie uma solicitação de geração de token de teste com o cookie gerado anexado como uma sequência de query (cookie=`<cookie>`) ou como cabeçalhos.
1. Solicite ao computador do usuário que envie uma solicitação de licença para o servidor de licença do Express usando o token acima, por exemplo, reproduzindo um conteúdo fictício.

   Esta solicitação de licença fictícia, quando bem-sucedida, associa a device_id do usuário (calculada ou gerada pela implementação do DRM no dispositivo do usuário) ao cookie no back-end do Express. Esse cookie é usado da seguinte maneira:

   * No momento da compra/aluguel do conteúdo, o código query o back-end do Express para o device_id do usuário enviando o cookie associado ( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * Envie uma solicitação de geração de token com a chave do conteúdo adquirido (CEK), a keyID (CEKSID), as políticas e outras informações, anexando o cookie e a device_id acima como, respectivamente, o parâmetro de correlação `cookie` e o parâmetro de restrição de token `deviceid`.

   * Forneça este token ao usuário.

      Esse processo gera um token para o conteúdo vinculado à device_id do usuário. Quando o computador do usuário envia uma solicitação de licença com esse token, o back-end do Express verifica o device_id do token com o device_id da solicitação de licença.

      Um exemplo de servidor de direito do Express implementa esse fluxo de trabalho.
