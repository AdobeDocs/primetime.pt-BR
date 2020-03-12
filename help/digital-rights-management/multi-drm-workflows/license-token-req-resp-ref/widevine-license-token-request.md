---
description: A interface do token de licença do Widevine fornece serviços de produção e teste.
seo-description: A interface do token de licença do Widevine fornece serviços de produção e teste.
seo-title: Solicitação / resposta do token de licença do Widevine
title: Solicitação / resposta do token de licença do Widevine
uuid: a3522422-7075-49a7-bc55-137ef84ee430
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Solicitação / resposta do token de licença do Widevine {#widevine-license-token-request-response}

A interface do token de licença do Widevine fornece serviços de produção e teste.

Esta solicitação HTTP retorna um token que pode ser resgatado para uma licença do Widevine.

**Método: GET, POST** (com um corpo codificado www-url que contém parâmetros para ambos os métodos)

**URLs:**

* **Produção:** `https://wv-gen.{prod_domain}/hms/wv/token`

* **Teste:** ` [https://wv-gen.test.expressplay.com/hms/wv/token](https://wv-gen.test.expressplay.com/hms/wv/token)`

* **Solicitação de amostra:**

   ```
   https://wv-gen.service.expressplay.com/hms/wv/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier>
   ```

* **Resposta de exemplo:**

   ```
   https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

<!--<a id="section_1E22012EE4B94BB2974D3B16DE8812D9"></a>-->

**Quadro 13: Parâmetros de consulta de token**

<table id="table_ww1_hcs_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Parâmetro de consulta</b> </th> 
   <th class="entry"> <b>Descrição</b> </th> 
   <th class="entry"> <b>Obrigatório?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> customerAuthenticator </span> </td> 
   <td> <p>Esta é a chave da API do cliente, uma para cada ambiente de produção e teste. Isso pode ser encontrado na guia ExpressPlay Admin Dashboard. </p> </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> errorFormat </span> </td> 
   <td> Ou <span class="codeph"> html </span> ou <span class="codeph"> json </span>. <p>Se <span class="codeph"> html </span> (o padrão) uma representação HTML de quaisquer erros for fornecida no corpo da entidade da resposta. Se <span class="codeph"> json </span> for especificado, uma resposta estruturada no formato JSON será retornada. Consulte Erros <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON </a> para obter detalhes. </p> <p>O tipo mime da resposta é <span class="codeph"> text/uri-list </span> em caso de sucesso, <span class="codeph"> text/html </span> para o formato de <span class="codeph"> erro </span> html ou <span class="codeph"> application/json </span> para o formato de <span class="codeph"> erro </span> json. </p> </td> 
   <td> Não </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 14: Parâmetros de consulta de licença**

| Parâmetro de consulta | Descrição | Obrigatório? |
|--- |--- |--- |
| `generalFlags` | Uma string hexadecimal de 4 bytes que representa os sinalizadores de licença. &quot;0000&quot; é o único valor permitido | Não |
| `kek` | Chave de criptografia de chave (KEK). As chaves são armazenadas criptografadas com um KEK usando um algoritmo de quebra automática de chave (AES Key Wrap, RFC3394). | Não |
| `kid` | Uma representação de string hexadecimal de 16 bytes da chave de criptografia de conteúdo ou de uma string `^somestring'`. O comprimento da string seguido pelo `^` não pode ser maior que 64 caracteres. Consulte a nota abaixo para ver um exemplo. | Sim |
| `ek` | Uma representação hexadecimal da chave de conteúdo criptografada. | Não |
| `contentKey` | Uma representação de string hexadecimal de 16 bytes da chave de criptografia de conteúdo | Sim, a menos que `kek` e `ek` ou `kid` sejam fornecidos |
| `contentId` | ID do conteúdo | Não |
| `securityLevel` | Os valores permitidos são 1-5. <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul> | Sim |
| `hdcpOutputControl` | Os valores permitidos são 0, 1, 2. <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul> | Sim |
| `licenseDuration` * | Duração da licença em segundos. Se não for fornecido, isso indica que não há limite para a duração. Verifique a nota abaixo para obter informações detalhadas. | Não |
| `wvExtension` | Um formulário curto vinculando extensionType e extensionPayload, como uma string separada por vírgulas. Consulte o formato abaixo. Example: `…&wvExtension=wudo,AAAAAA==&…` | Não, qualquer número pode ser usado |

Sobre `licenseDuration`: <ol><li> A reprodução parará `licenseDuration` segundos após o início da reprodução. </li><li> Para permitir que a reprodução seja interrompida/retomada por um período ilimitado, omita `licenseDuration` (o padrão será infinito). Caso contrário, especifique a quantidade de tempo durante a qual os usuários finais devem poder desfrutar do fluxo. </li></ol>

**Quadro 15: Parâmetros de Consulta de Restrição de Token**

| Parâmetro de consulta | Descrição | Obrigatório? |
|--- |--- |--- |
| `expirationTime` | Tempo de expiração deste token. Esse valor DEVE ser uma string no formato [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) date/time no designador de zona ‘Z’ (&quot;Zulu time&quot;) ou um número inteiro precedido por um sinal +. Um exemplo de uma data/hora RFC 3339 é 2006-04-14T12:01:10Z. <br> Se o valor for uma string no formato [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) de data/hora, então ele representa uma data/hora de expiração absoluta para o token. Se o valor for um número inteiro precedido por um sinal +, então ele será interpretado como um número relativo de segundos, desde a emissão, de que o token é válido. Por exemplo, `+60` especifica um minuto. <br> A duração máxima e padrão do token (se não especificada) é de 30 dias. | Não |

**Quadro 16: Parâmetros de consulta de correlação**

| **Parâmetro de consulta** | **Descrição** | **Obrigatório?** |
|---|---|---|
| `cookie` | Sequência arbitrária de até 32 caracteres carregada no token e registrada pelo servidor de resgate de token. Pode ser usado para correlacionar entradas de log no servidor de resgate e aquelas nos servidores do provedor de serviços. | Não |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**Quadro 17: Resposta HTTP**

| **Código de status HTTP** | **Descrição** | **Tipo de conteúdo** | **Corpo da Entidade Contém** |
|---|---|---|---|
| `200 OK` | Nenhum erro. | `text/uri-list` | URL de aquisição de licença + token |
| `400 Bad Request` | Argumentos inválidos | `text/html` os `application/json` | Descrição do erro |
| `401 Unauthorized` | Falha na autenticação | `text/html` os `application/json` | Descrição do erro |
| `404 Not found` | URL incorreto | `text/html` os `application/json` | Descrição do erro |
| `50x Server Error` | Erro do servidor | `text/html` os `application/json` | Descrição do erro |

**Quadro 18: Códigos de erro de evento**

<table id="table_agj_gqx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> Código </th> 
   <th class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> -2002 </td> 
   <td> Hora de expiração do token inválida: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> Endereço IP inválido </td> 
  </tr> 
  <tr> 
   <td> -2005 </td> 
   <td> Chave de criptografia de conteúdo inválida: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2008 </td> 
   <td> Sinalizadores de controle de saída inválidos especificados: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> O token de autenticação deve ser fornecido </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> Token de autenticação inválido: &lt;details&gt; <p>Observação:  Isso pode acontecer se o autenticador estiver incorreto ou ao acessar a API de teste em *.test.express.com usando o autenticador de produção e vice-versa. </p> <p importance="high">Observação:  O SDK de teste e a ATT (Advanced Test Tool) funcionam somente com <span class="filepath"> *.test.express.com, enquanto os dispositivos de produção devem usar </span><span class="filepath"> *.service.express.play.com </span> </p>. </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> Tokens insuficientes disponíveis </td> 
  </tr> 
  <tr> 
   <td> -2022 </td> 
   <td> Tempo de término do período de aluguel ausente </td> 
  </tr> 
  <tr> 
   <td> -2023 </td> 
   <td> Duração da reprodução de aluguel ausente </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> Duração inválida da reprodução de aluguel </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> A chave de criptografia de conteúdo deve ter 32 dígitos hexadecimais </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> Erro do administrador do ExpressPlay: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2031 </td> 
   <td> Conta de Serviço Desativada </td> 
  </tr> 
  <tr> 
   <td> -2033 </td> 
   <td> Cookie inválido </td> 
  </tr> 
  <tr> 
   <td> -2034 </td> 
   <td> Controle de saída inválido, valores fora do intervalo especificado </td> 
  </tr> 
  <tr> 
   <td> -2035 </td> 
   <td> Nenhum valor correspondente especificado </td> 
  </tr> 
  <tr> 
   <td> -2036 </td> 
   <td> O tipo de extensão deve ter 4 caracteres </td> 
  </tr> 
  <tr> 
   <td> -2037 </td> 
   <td> A carga da extensão deve ser codificada em Base64 </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td> <span class="codeph"> OutputControlFlag </span> deve ter a codificação 4 bytes </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> Formato de erro inválido especificado: &lt;format&gt; </td> 
  </tr> 
  <tr> 
   <td> -4001 </td> 
   <td> Não foi possível autenticar o dispositivo </td> 
  </tr> 
  <tr> 
   <td> -4010 </td> 
   <td> Token inválido </td> 
  </tr> 
  <tr> 
   <td> -4018 </td> 
   <td> Menino <span class="filepath"> ausente </span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Falha ao obter a chave de conteúdo do serviço de armazenamento de chave </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> criança </span> deve ter 32 caracteres hexadecimais </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> criança </span> deve ter 64 caracteres depois do '^' </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> Criança <span class="codeph"> inválida </span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> Chave ou chave <span class="codeph"> criptografada inválida </span> </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> Sinalizadores gerais inválidos </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> Dados de chave inválidos especificados </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> Duração de aluguer inválida especificada </td> 
  </tr> 
  <tr> 
   <td> -7002 </td> 
   <td> O vínculo de ID de dispositivo não é compatível com o Widevine </td> 
  </tr> 
  <tr> 
   <td> -7003 </td> 
   <td> Valor do nível de segurança ausente </td> 
  </tr> 
  <tr> 
   <td> -7004 </td> 
   <td> Valor de nível de segurança inválido </td> 
  </tr> 
  <tr> 
   <td> -7006 </td> 
   <td> Valor de controlo de saída HDCP ausente </td> 
  </tr> 
  <tr> 
   <td> -7007 </td> 
   <td> Duração de licença inválida especificada </td> 
  </tr> 
  <tr> 
   <td> -7008 </td> 
   <td> Falha ao gerar a licença do Widevine </td> 
  </tr> 
  <tr> 
   <td> -7009 </td> 
   <td> Parâmetros <span class="codeph"> WVExtension inválidos </span> especificados </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> Opção Widevine desativada </td> 
  </tr> 
 </tbody> 
</table>