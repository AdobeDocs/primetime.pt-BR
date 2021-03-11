---
description: Em alguns casos, você pode querer impedir que usuários finais reproduzam conteúdo em vários dispositivos quando o conteúdo for comprado ou alugado. Se o cliente estiver usando o Express, isso pode ser feito usando as APIs de Exibição para vincular o token de Exibição do usuário à máquina do usuário.
title: Vínculo do dispositivo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Vínculo de dispositivo{#device-binding}

Em alguns casos, você pode querer impedir que usuários finais reproduzam conteúdo em vários dispositivos quando o conteúdo for comprado ou alugado. Se o cliente estiver usando o Express, isso pode ser feito usando as APIs de Exibição para vincular o token de Exibição do usuário à máquina do usuário.

Você pode usar as APIs da seguinte maneira.

1. Gere um cookie.
1. Envie uma solicitação de geração de token fictício com o cookie gerado anexado como uma sequência de consulta (cookie=`<cookie>`) ou como cabeçalhos.
1. Faça com que a máquina do usuário envie uma solicitação de licença para o servidor de licenças do Expressplay usando o token acima, por exemplo, reproduzindo um conteúdo fictício.

   Essa solicitação de licença de teste, quando bem-sucedida, associa a device_id do usuário (calculada ou gerada pela implementação do DRM no dispositivo do usuário) ao cookie no back-end da Expressão. Esse cookie é usado da seguinte maneira:

   * No momento da compra/aluguel do conteúdo, o código consulta o back-end da Expressão para o device_id do usuário, enviando o cookie associado ( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * Envie uma solicitação de geração de token com a chave do conteúdo adquirido (CEK), a keyID (CEKSID), as políticas e outras informações, anexando o cookie e a device_id acima como, respectivamente, o parâmetro de correlação `cookie` e o parâmetro de restrição de token `deviceid`.

   * Forneça este token ao usuário.

      Esse processo gera um token para o conteúdo vinculado à device_id do usuário. Quando a máquina do usuário envia uma solicitação de licença com esse token, o back-end da Exibição verificará o device_id do token com a id_do_dispositivo da solicitação de licença.

      Um exemplo de servidor de direito de Exibição implementa esse workflow.
