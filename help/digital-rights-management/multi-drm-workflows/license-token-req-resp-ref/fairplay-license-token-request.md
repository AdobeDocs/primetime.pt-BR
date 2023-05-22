---
description: A interface do token de licença FairPlay fornece serviços de produção e teste.
title: Solicitação/resposta do token de licença FairPlay
exl-id: 7073a74b-d907-4d45-8550-4305655c33f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 4%

---

# Solicitação e resposta do token de licença FairPlay {#fairplay-license-token-request-response}

A interface do token de licença FairPlay fornece serviços de produção e teste. Esta solicitação retorna um token que pode ser resgatado para uma licença FairPlay.

**Método: GET, POST** (com um corpo codificado em www-url que contém parâmetros para ambos os métodos)

**URLs:**

* **Produção:** `https://fp-gen.{prod_domain}/hms/fp/token`

* **Teste:** `https://fp-gen.test.expressplay.com/hms/fp/token`

* **Exemplo de solicitação:**

```<xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
  https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier> 
   &kid=<CEKSID> 
   &contentKey=<CEK> 
   &rightsType=BuyToOwn 
   &analogVideoOPL=0 
   &compressedDigitalAudioOPL=0 
   &compressedDigitalVideoOPL=0 
   &uncompressedDigitalAudioOPL=0 
   &uncompressedDigitalVideoOPL=0
```

* **Exemplo de resposta:**

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

**Parâmetros de consulta de solicitação**

**Tabela 3: Parâmetros de consulta de token**

| Parâmetro da consulta | Descrição | Obrigatório? |
|--- |--- |--- |
| customerAuthenticator Autenticador do cliente como parâmetro de consulta customerAuthenticator FairPlay | Essa é a chave da API do cliente, uma para cada ambiente de produção e teste. Você pode encontrá-lo na guia ExpressPlay Admin Dashboard. | Sim |
| errorFormat | html ou json. Se html (o padrão) uma representação de HTML de quaisquer erros é fornecida no corpo da entidade da resposta. Se json for especificado, uma resposta estruturada no formato JSON será retornada. Consulte [Erros JSON](https://www.expressplay.com/developer/restapi/#json-errors) para obter detalhes. O tipo mime da resposta é text/uri-list em caso de sucesso, text/html para o formato de erro HTML ou application/json para o formato de erro JSON. | Não |

**Tabela 4: Parâmetros de consulta de licença**

| **Parâmetro da consulta** | **Descrição** | **Obrigatório?** |
|---|---|---|
| `generalFlags` | Uma string hexadecimal de 4 bytes que representa os sinalizadores de licença. ‘0000’ é o único valor permitido. | Não |
| `kek` | Chave de criptografia de chave (KEK). As chaves são armazenadas criptografadas com um KEK usando um algoritmo de quebra automática de chaves (AES Key Wrap, RFC3394). Se `kek` for fornecida, uma das opções `kid` ou o `ek` os parâmetros devem ser fornecidos, *mas não ambos*. | Não |
| `kid` | Uma representação de string hexadecimal de 16 bytes da chave de criptografia de conteúdo ou uma string `'^somestring'`. O comprimento da sequência de caracteres seguido pelo `'^'` não pode ter mais de 64 caracteres. | Não |
| `ek` | Uma representação de sequência hexadecimal da chave de conteúdo criptografada. | Não |
| `contentKey` | Uma representação de string hexadecimal de 16 bytes da chave de criptografia de conteúdo | Sim, a menos que a variável `kek` e `ek` ou `kid` são fornecidos. |
| `iv` | Uma representação de string hexadecimal de 16 bytes da criptografia de conteúdo IV | Sim |
| `rentalDuration` | Duração da locação em segundos (padrão - 0) | Não |
| `fpExtension` | Encapsulamento de formulário curto `extensionType` e `extensionPayload`, como uma cadeia de caracteres separada por vírgulas. Por exemplo: [..] `&fpExtension=wudo,AAAAAA==&`[..] | Não, qualquer número pode ser usado |

**Tabela 5: Parâmetros de consulta de restrição de token**

<table id="table_ar3_lsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Parâmetro da consulta</b> </th> 
   <th class="entry"> <b>Descrição</b> </th> 
   <th class="entry"> <b>Obrigatório?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> expirationTime </span> </td> 
   <td> Hora de expiração deste token. Este valor DEVE ser uma sequência de caracteres em <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> formato de data/hora no designador de zona ‘Z’ ("hora Zulu") ou um número inteiro precedido por um sinal '+'. Um exemplo de data/hora RFC 3339 é <span class="codeph"> 2006-04-14T12:01:10Z </span>. <p>Se o valor for uma string em <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> formato de data/hora, então representa uma data/hora de expiração absoluta do token. Se o valor for um número inteiro precedido por um sinal '+', então será interpretado como um número relativo de segundos, a partir da emissão, se o token é válido. </p> Por exemplo, <span class="codeph"> +60 </span> especifica um minuto. O tempo de vida máximo e padrão do token (se não especificado) é de 30 dias. </td> 
   <td> Não </td> 
  </tr> 
 </tbody> 
</table>

**Tabela 6: Parâmetros de consulta de correlação**

| **Parâmetro da consulta** | **Descrição** | **Obrigatório?** |
|---|---|---|
| `cookie` | Uma sequência arbitrária de até 32 caracteres, carregada no token e registrada pelo servidor de resgate do token. Isso pode ser usado para correlacionar as entradas de log no servidor de resgate com aquelas nos servidores do provedor de serviços. | Não |

**Resposta**

**Tabela 7: Respostas HTTP**

| **Código de status HTTP** | **Descrição** | **Tipo de conteúdo** | **Corpo da entidade contém** |
|---|---|---|---|
| `200 OK` | Nenhum erro. | `text/uri-list` | URL + token de aquisição de licença |
| `400 Bad Request` | Argumentos inválidos | `text/html` ou `application/json` | Descrição do erro |
| `401 Unauthorized` | Falha de autenticação | `text/html` ou `application/json` | Descrição do erro |
| `404 Not found` | URL inválido | `text/html` ou `application/json` | Descrição do erro |
| `50x Server Error` | Erro do servidor | `text/html` ou `application/json` | Descrição do erro |

**Tabela 8: Códigos de erro do evento**

<table id="table_i2c_zsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Código</b> </th> 
   <th class="entry"> <b>Descrição</b> </th> 
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
   <td> Token de autenticação inválido: &lt;details&gt; <p>Observação: isso pode acontecer se o autenticador estiver errado ou ao acessar a API de teste em <span class="filepath"> *.test.expressplay.com </span> usando o autenticador de produção e vice-versa. </p> <p importance="high">Observação: o SDK de teste e a Ferramenta de teste avançada (ATT) funcionam somente com o <span class="filepath"> *.test.expressplay.com </span>, enquanto os dispositivos de produção devem utilizar <span class="filepath"> *.service.expressplay.com </span>. </p> </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> Tokens insuficientes disponíveis </td> 
  </tr> 
  <tr> 
   <td> -2020 </td> 
   <td> Tipo de direitos ausente </td> 
  </tr> 
  <tr> 
   <td> -2021 </td> 
   <td> Tipo de direitos inválido </td> 
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
   <td> Criança desaparecida </td> 
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
   <td> <span class="codeph"> criança </span> deve ter 64 caracteres após ^ </td> 
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
   <td> -6001 </td> 
   <td> Inválido <span class="codeph"> FPExtension </span> parâmetros especificados </td> 
  </tr> 
  <tr> 
   <td> -6002 </td> 
   <td> Tipo de token FP inválido </td> 
  </tr> 
  <tr> 
   <td> -6003 </td> 
   <td> Inválido <span class="codeph"> iv </span> parâmetro especificado </td> 
  </tr> 
  <tr> 
   <td> -6004 </td> 
   <td> Falha ao gerar CKC para FP </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> Dados de chave inválidos especificados </td> 
  </tr> 
  <tr> 
   <td> -6006 </td> 
   <td> Serviço não autorizado para suporte a FairPlay </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> Duração de locação inválida especificada </td> 
  </tr> 
  <tr> 
   <td> -6008 </td> 
   <td> A ligação da ID do dispositivo não é suportada para FairPlay </td> 
  </tr> 
  <tr> 
   <td> -6009 </td> 
   <td> Opção FairPlay desabilitada </td> 
  </tr> 
 </tbody> 
</table>
