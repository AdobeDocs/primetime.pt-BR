---
description: A interface do token de licença do Widevine fornece serviços de produção e teste.
title: Solicitação/resposta do token de licença do Widevine
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 5%

---

# Solicitação/resposta do token de licença do Widevine {#widevine-license-token-request-response}

A interface do token de licença do Widevine fornece serviços de produção e teste.

Essa solicitação HTTP retorna um token que pode ser resgatado para uma licença Widevine.

**Método: GET, POST** (com um corpo codificado em www-url que contém parâmetros para ambos os métodos)

**URLs:**

* **Produção:** `https://wv-gen.{prod_domain}/hms/wv/token`

* **Teste:** ` [https://wv-gen.test.expressplay.com/hms/wv/token](https://wv-gen.test.expressplay.com/hms/wv/token)`

* **Exemplo de solicitação:**

  ```
  https://wv-gen.service.expressplay.com/hms/wv/token?customerAuthenticator= 
  <ExpressPlay customer authenticator identifier>
  ```

* **Exemplo de resposta:**

  ```
  https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
  ```

<!--<a id="section_1E22012EE4B94BB2974D3B16DE8812D9"></a>-->

**Tabela 13: Parâmetros de consulta de token**

<table id="table_ww1_hcs_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Parâmetro da consulta</b> </th> 
   <th class="entry"> <b>Descrição</b> </th> 
   <th class="entry"> <b>Obrigatório?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> customerAuthenticator </span> </td> 
   <td> <p>Essa é a chave da API do cliente, uma para cada ambiente de produção e teste. Você pode encontrá-lo na guia ExpressPlay Admin Dashboard. </p> </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> errorFormat </span> </td> 
   <td> Ou <span class="codeph"> html </span> ou <span class="codeph"> json </span>. <p>Se <span class="codeph"> html </span> (o padrão) uma representação HTML de quaisquer erros é fornecida no corpo da entidade da resposta. Se <span class="codeph"> json </span> for especificada, uma resposta estruturada no formato JSON será retornada. Consulte <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> Erros JSON </a> para obter detalhes. </p> <p>O tipo MIME da resposta é <span class="codeph"> text/uri-list </span> no sucesso, <span class="codeph"> text/html </span> para <span class="codeph"> html </span> formato de erro, ou <span class="codeph"> application/json </span> para <span class="codeph"> json </span> formato de erro. </p> </td> 
   <td> Não </td> 
  </tr> 
 </tbody> 
</table>

**Tabela 14: Parâmetros de consulta de licença**

| Parâmetro da consulta | Descrição | Obrigatório? |
|--- |--- |--- |
| `generalFlags` | Uma string hexadecimal de 4 bytes que representa os sinalizadores de licença. ‘0000’ é o único valor permitido | Não |
| `kek` | Chave de criptografia de chave (KEK). As chaves são armazenadas criptografadas com um KEK usando um algoritmo de quebra automática de chaves (AES Key Wrap, RFC3394). | Não |
| `kid` | Uma representação de string hexadecimal de 16 bytes da chave de criptografia de conteúdo ou uma string `^somestring'`. O comprimento da sequência de caracteres seguido pelo `^` não pode ter mais de 64 caracteres. Consulte a observação abaixo para ver um exemplo. | Sim |
| `ek` | Uma representação de sequência hexadecimal da chave de conteúdo criptografada. | Não |
| `contentKey` | Uma representação de string hexadecimal de 16 bytes da chave de criptografia de conteúdo | Sim, exceto se `kek` e `ek` ou `kid` são fornecidos |
| `contentId` | ID de conteúdo | Não |
| `securityLevel` | Os valores permitidos são de 1 a 5. <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul> | Sim |
| `hdcpOutputControl` | Os valores permitidos são 0, 1, 2. <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul> | Sim |
| `licenseDuration` * | Duração da licença em segundos. Se não for fornecido, indica que não há limite para a duração. Verifique a nota abaixo para obter informações detalhadas. | Não |
| `wvExtension` | Um formulário curto que ajusta extensionType e extensionPayload como uma cadeia de caracteres separada por vírgulas. Consulte o formato abaixo. Exemplo: `…&wvExtension=wudo,AAAAAA==&…` | Não, qualquer número pode ser usado |

Sobre `licenseDuration`: <ol><li> A reprodução será interrompida `licenseDuration` segundos após o início da reprodução. </li><li> Para permitir que a reprodução seja interrompida/retomada por um período ilimitado, omita `licenseDuration` (o padrão é infinito). Caso contrário, especifique o período durante o qual os usuários finais devem poder aproveitar o fluxo. </li></ol>

**Tabela 15: Parâmetros de consulta de restrição de token**

| Parâmetro da consulta | Descrição | Obrigatório? |
|--- |--- |--- |
| `expirationTime` | Hora de expiração deste token. Este valor DEVE ser uma sequência de caracteres em [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) formato de data/hora no designador de zona ‘Z’ (&quot;hora Zulu&quot;) ou um número inteiro precedido por um sinal +. Um exemplo de data/hora RFC 3339 é 2006-04-14T12:01:10Z <br> Se o valor for uma string em [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) formato de data/hora, então representa uma data/hora de expiração absoluta do token. Se o valor for um número inteiro precedido por um sinal +, então será interpretado como um número relativo de segundos, desde a emissão, se o token é válido. Por exemplo, `+60` especifica um minuto. <br> O tempo de vida máximo e padrão do token (se não especificado) é de 30 dias. | Não |

**Tabela 16: Parâmetros de consulta de correlação**

| **Parâmetro da consulta** | **Descrição** | **Obrigatório?** |
|---|---|---|
| `cookie` | Sequência arbitrária de até 32 caracteres carregada no token e registrada pelo servidor de resgate do token. Pode ser usado para correlacionar entradas de log no servidor de resgate e aquelas nos servidores do provedor de serviços. | Não |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**Tabela 17: Resposta HTTP**

| **Código de status HTTP** | **Descrição** | **Tipo de conteúdo** | **Corpo da entidade contém** |
|---|---|---|---|
| `200 OK` | Nenhum erro. | `text/uri-list` | URL + token de aquisição de licença |
| `400 Bad Request` | Argumentos inválidos | `text/html` ou `application/json` | Descrição do erro |
| `401 Unauthorized` | Falha de autenticação | `text/html` ou `application/json` | Descrição do erro |
| `404 Not found` | URL inválido | `text/html` ou `application/json` | Descrição do erro |
| `50x Server Error` | Erro do servidor | `text/html` ou `application/json` | Descrição do erro |

**Tabela 18: Códigos de erro do evento**

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
   <td> Tempo de expiração de token inválido: &lt;details&gt; </td> 
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
   <td> Token de autenticação inválido: &lt;details&gt; <p>Observação: isso pode acontecer se o autenticador estiver errado ou ao acessar a API de teste em *.test.expressplay.com usando o autenticador de produção e vice-versa. </p> <p importance="high">Observação: o SDK de teste e a Ferramenta de teste avançada (ATT) funcionam somente com o <span class="filepath"> *.test.expressplay.com </span>, enquanto os dispositivos de produção devem utilizar <span class="filepath"> *.service.expressplay.com </span> </p>. </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> Tokens insuficientes disponíveis </td> 
  </tr> 
  <tr> 
   <td> -2022 </td> 
   <td> Hora final do período de locação ausente </td> 
  </tr> 
  <tr> 
   <td> -2023 </td> 
   <td> Duração da reprodução de locação ausente </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> Duração inválida da reprodução de aluguel </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> A chave de criptografia do conteúdo deve ter 32 dígitos hexadecimais </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> Erro do administrador do ExpressPlay: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2031 </td> 
   <td> Conta de Serviço Desabilitada </td> 
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
   <td> A carga da extensão deve ser codificada na Base64 </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td> <span class="codeph"> SinalizadorControleSaída </span> deve ser codificado em 4 bytes </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> Formato inválido especificado: &lt;format&gt; </td> 
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
   <td> Ausente <span class="filepath"> criança </span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Falha ao obter a chave de conteúdo do serviço de armazenamento de chaves </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> criança </span> deve ter 32 caracteres hexadecimais </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> criança </span> deve ter 64 caracteres após o caractere '^' </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> Inválido <span class="codeph"> criança </span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> Chave criptografada inválida ou <span class="codeph"> kek </span> </td> 
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
   <td> Duração de locação inválida especificada </td> 
  </tr> 
  <tr> 
   <td> -7002 </td> 
   <td> A ligação da ID do dispositivo não é suportada para o Widevine </td> 
  </tr> 
  <tr> 
   <td> -7003 </td> 
   <td> Valor de nível de segurança ausente </td> 
  </tr> 
  <tr> 
   <td> -7004 </td> 
   <td> Valor de nível de segurança inválido </td> 
  </tr> 
  <tr> 
   <td> -7006 </td> 
   <td> Valor do controle de saída HDCP ausente </td> 
  </tr> 
  <tr> 
   <td> -7007 </td> 
   <td> Duração de licença inválida especificada </td> 
  </tr> 
  <tr> 
   <td> -7008 </td> 
   <td> Falha ao gerar a licença Widevine </td> 
  </tr> 
  <tr> 
   <td> -7009 </td> 
   <td> Inválido <span class="codeph"> Extensão WVE </span> parâmetros especificados </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> Opção Widevine desabilitada </td> 
  </tr> 
 </tbody> 
</table>
