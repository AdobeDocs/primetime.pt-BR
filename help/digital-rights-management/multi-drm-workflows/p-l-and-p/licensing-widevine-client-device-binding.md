---
description: Em alguns casos, talvez você queira impedir que os usuários finais reproduzam conteúdo em vários dispositivos quando o conteúdo for comprado ou alugado. Se o cliente estiver usando o Expressplay, isso poderá ser feito usando as APIs do Expressplay para vincular o token Expressplay do usuário à máquina do usuário.
title: Vinculação de dispositivo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Vinculação de dispositivo{#device-binding}

Em alguns casos, talvez você queira impedir que os usuários finais reproduzam conteúdo em vários dispositivos quando o conteúdo for comprado ou alugado. Se o cliente estiver usando o Expressplay, isso poderá ser feito usando as APIs do Expressplay para vincular o token Expressplay do usuário à máquina do usuário.

Você pode usar as APIs da seguinte maneira.

1. Gere um cookie.
1. Envie uma solicitação de geração de token fictício com o cookie gerado anexado como uma cadeia de caracteres de consulta (cookie=`<cookie>`) ou como cabeçalhos.
1. Faça com que a máquina do usuário envie uma solicitação de licença para o servidor de licenças do Expressplay usando o token acima, por exemplo, reproduzindo um conteúdo fictício.

   Esta solicitação de licença fictícia, quando bem-sucedida, associa o device_id do usuário (calculado ou gerado pela implementação DRM no dispositivo do usuário) ao cookie no back-end do Expressplay. Esse cookie é usado da seguinte maneira:

   * No momento da compra/aluguel do conteúdo, o código consulta o back-end do Expressplay para a device_id do usuário, enviando o cookie associado ( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * Envie uma solicitação de geração de token com a chave (CEK), a keyID (CEKSID), as políticas e outras informações do conteúdo adquirido, anexando o cookie e o device_id acima como, respectivamente, o `cookie` parâmetro de correlação e `deviceid` parâmetro de restrição de token.

   * Forneça esse token ao usuário.

     Esse processo gera um token para o conteúdo vinculado ao device_id do usuário. Quando o computador do usuário enviar uma solicitação de licença com esse token, o back-end do Expressplay verificará a device_id do token com a device_id da solicitação de licença.

     Um exemplo de servidor de direitos do Express implementa esse fluxo de trabalho.
