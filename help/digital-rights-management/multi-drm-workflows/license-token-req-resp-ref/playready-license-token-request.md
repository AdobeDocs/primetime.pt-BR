---
description: A interface do token de licença do PlayReady fornece serviços de produção e teste.
title: Solicitação/resposta do token de licença do PlayReady
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---

# Solicitação/resposta do token de licença do PlayReady {#playready-license-token-request-response}

A interface do token de licença do PlayReady fornece serviços de produção e teste.

Esta solicitação HTTP retorna um token que pode ser resgatado para uma licença PlayReady.

**Método: GET, POST** (com um corpo codificado em www-url que contém parâmetros para ambos os métodos)

**URLs:**

* **Produção:** `https://pr-gen.{prod_domain}/hms/pr/token`

* **Teste:** ` [https://pr-gen.test.expressplay.com/hms/pr/token](https://pr-gen.test.expressplay.com/hms/pr/token)`

* **Exemplo de solicitação:**

  ```
  <xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
  https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator=
   <ExpressPlay customer authenticator identifier>
   &kid=<CEKSID>
   &contentKey=<CEK>
   &rightsType=BuyToOwn
   &analogVideoOPL=0
   &compressedDigitalAudioOPL=0
   &compressedDigitalVideoOPL=0
   &uncompressedDigitalAudioOPL=0
   &uncompressedDigitalVideoOPL=0
  </xref href="https:>
  ```

* **Exemplo de resposta:**

  ```
  {"licenseAcquisitionUrl":"https://expressplay-licensing.axprod.net/LicensingService.ashx",
              "token":"<base64-encoded ExpressPlay token>"}
  ```

## Parâmetros de consulta de solicitação {#section_26F8856641A64A46A3290DBE61ACFAD2}

**Tabela 9: Parâmetros de consulta de token**

<table id="table_zxg_dyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Parâmetro da consulta</b> </th> 
   <th class="entry"><b>Descrição</b> </th> 
   <th class="entry"><b>Obrigatório?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> customerAuthenticator</span> </td> 
   <td> <p>Essa é a chave da API do cliente, uma para cada ambiente de produção e teste. Você pode encontrá-lo na guia ExpressPlay Admin Dashboard. </p> </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> errorFormat</span> </td> 
   <td>Ou <span class="codeph"> html</span> ou <span class="codeph"> json</span>. Se <span class="codeph"> html</span> (o padrão) uma representação HTML de quaisquer erros é fornecida no corpo da entidade da resposta. <p>Se <span class="codeph"> json</span> for especificada, uma resposta estruturada no formato JSON será retornada. Consulte <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> Erros JSON</a> para obter detalhes. </p> <p>O tipo MIME da resposta é <span class="codeph"> text/uri-list</span> no sucesso, <span class="codeph"> text/html</span> para o formato de erro HTML, ou <span class="codeph"> application/json</span> para formato de erro JSON. </p> </td> 
   <td> Não </td> 
  </tr> 
 </tbody> 
</table>

**Tabela 10: Parâmetros de consulta de licença**

<table id="table_f1l_fyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Parâmetro da consulta</b> </th> 
   <th class="entry"><b>Descrição</b> </th> 
   <th class="entry"><b>Obrigatório?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> generalFlags</span> </td> 
   <td>Uma string hexadecimal de 4 bytes que representa os sinalizadores de licença. Deve ser definido como ‘00000001’ para uma licença persistente. <p>Observação: licenças de aluguel (<span class="codeph"> rightsType=Aluguel</span>) DEVE ser persistente. </p> </td> 
   <td> Não </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> kek</span> </td> 
   <td> Chave de criptografia de chave (KEK). As chaves são armazenadas criptografadas com um KEK usando um algoritmo de quebra automática de chaves (AES Key Wrap, RFC3394). </td> 
   <td> Não </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> criança</span> </td> 
   <td>Uma representação de string hexadecimal de 16 bytes da chave de criptografia de conteúdo ou uma string <span class="codeph"> ^somestring'</span>. O comprimento da cadeia de caracteres seguido por '^' não pode ser maior que 64 caracteres. </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> ek</span> </td> 
   <td> Uma representação de sequência hexadecimal da chave de conteúdo criptografada. </td> 
   <td> Não </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> contentKey</span> </td> 
   <td> Uma representação de string hexadecimal de 16 bytes da chave de criptografia de conteúdo </td> 
   <td>Sim, exceto se <span class="codeph"> kek</span> e <span class="codeph"> ek</span> ou <span class="codeph"> criança</span> são fornecidos </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rightsType</span> </td> 
   <td>Especifica o tipo de direitos. Deve ser <span class="codeph"> BuyToOwn</span> ou <span class="codeph"> Aluguel</span>. </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rent.periodEndTime</span> </td> 
   <td>Data final da locação. Este valor DEVE estar no formato de data/hora 'RFC 3339' _ no formato de designador de zona 'Z' ("Zulu time") ou um número inteiro precedido por um sinal '+'. <p>Se o valor for um <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339</a> formato de data/hora e, em seguida, representa uma data/hora de expiração absoluta da licença. Um exemplo de data/hora RFC 3339 é 2006-04-14T12:01:10Z </p> <p> Se o valor for um número inteiro precedido por um sinal '+', ele será considerado um número relativo de segundos a partir do momento em que o token for emitido. O conteúdo não pode ser reproduzido após esse tempo. Somente válido se <span class="codeph"> rightsType</span> é <span class="codeph"> Aluguel</span>. </p> </td> 
   <td>Sim, quando <span class="codeph"> rightsType</span> é <span class="codeph"> Aluguel</span>. </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rent.playDuration</span> </td> 
   <td>Tempo, em segundos, que o conteúdo pode ser reproduzido depois que a reprodução é iniciada. Somente válido se <span class="codeph"> rightsType</span> é Aluguel. </td> 
   <td> Não </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> análogoVideoOPL</span> </td> 
   <td> Valor inteiro para indicar o Nível de Proteção de Saída para vídeo analógico. Intervalo válido de 0 a 999. </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalAudioOPL</span> </td> 
   <td> Valor inteiro para indicar o Nível de Proteção de Saída para áudio digital compactado. Intervalo válido de 0 a 999. </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalVideoOPL</span> </td> 
   <td> Valor inteiro para indicar o Nível de proteção de saída para vídeo digital compactado. Intervalo válido de 0 a 999. </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalAudioOPL</span> </td> 
   <td> Valor inteiro para indicar o Nível de Proteção de Saída para áudio digital descompactado. Intervalo válido de 0 a 999. </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalVideoOPL</span> </td> 
   <td> Valor inteiro para indicar o Nível de proteção de saída para vídeo digital descompactado. Intervalo válido de 0 a 999. </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> unknownOutputBehavior</span> </td> 
   <td>Comportamento necessário quando a saída é desconhecida. Valores permitidos: <span class="codeph"> Permitir</span>, <span class="codeph"> Não permitir</span> ou <span class="codeph"> SDOnly</span> </td> 
   <td> Não </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlags</span> </td> 
   <td> Um valor hexadecimal de 4 bytes para indicar os sinalizadores de outras opções de controle de saída </td> 
   <td> Não </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionType</span> </td> 
   <td>Uma palavra arbitrária de 4 letras que representa um identificador de 32 bits para uma Extensão. O código ASCII de 8 bits de cada letra é a parte correspondente de 8 bits do identificador. Por exemplo, o valor do identificador 0x61626364 (hexadecimal) seria escrito ‘<span class="codeph"> abcd</span>', porque o código ASCII para 'a' é 0x61, etc. </td> 
   <td> Não </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionPayload</span> </td> 
   <td> Uma string codificada em base64 da Extensão. </td> 
   <td>Sim, quando <span class="codeph"> extensionType</span> é especificado. </td> 
  </tr> 
 </tbody> 
</table>

## Respostas {#section_0079C31B4AF14DBBB6277CF251FB90E3}

**Tabela 11: Respostas HTTP**

| **Código de status HTTP** | **Descrição** | **Tipo de conteúdo** | **Corpo da entidade contém** |
|---|---|---|---|
| `200 OK` | Nenhum erro. | `text/uri-list` | URL e token de aquisição de licença |
| `400 Bad Request` | Argumentos inválidos | `text/html` ou `application/json` | Descrição do erro |
| `401 Unauthorized` | Falha de autenticação | `text/html` ou `application/json` | Descrição do erro |
| `404 Not found` | URL inválido | `text/html` ou `application/json` | Descrição do erro |
| `50x Server Error` | Erro do servidor | `text/html` ou `application/json` | Descrição do erro |

**Tabela 12: Códigos de erro do evento**

<table id="table_lqb_ycs_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Código</b> </th> 
   <th class="entry"><b>Descrição</b> </th> 
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
   <td>Token de autenticação inválido: &lt;details&gt; <p>Observação: isso pode acontecer se o autenticador estiver errado ou ao acessar a API de teste em *.test.expressplay.com usando o autenticador de produção e vice-versa. </p> <p importance="high">Observação: o SDK de teste e a Ferramenta de teste avançada (ATT) funcionam somente com o <span class="filepath"> *.test.expressplay.com</span>, enquanto os dispositivos de produção devem utilizar <span class="filepath"> *.service.expressplay.com</span>. </p> </td> 
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
   <td><span class="codeph"> SinalizadorControleSaída</span> deve ser codificado em 4 bytes </td> 
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
   <td> -4018 </td> 
   <td>Ausente <span class="codeph"> criança</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Falha ao obter a chave de conteúdo do serviço de armazenamento de chaves </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> criança</span> deve ter 32 caracteres hexadecimais </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> criança</span> deve ter 64 caracteres após ^ </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td>Inválido <span class="codeph"> criança</span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>Criptografado inválido <span class="codeph"> key</span> ou kek </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> Erro de tipo de saída desconhecido inválido </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> A opção PlayReady está desabilitada para este serviço </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> Sinalizadores gerais inválidos </td> 
  </tr> 
  <tr> 
   <td> -5004 </td> 
   <td> A ID do dispositivo deve ter 32 caracteres hexadecimais </td> 
  </tr> 
  <tr> 
   <td> -5005 </td> 
   <td> ID de dispositivo inválida </td> 
  </tr> 
  <tr> 
   <td> -5006 </td> 
   <td> Valor OPL ausente </td> 
  </tr> 
  <tr> 
   <td> -5007 </td> 
   <td>Somente um de <span class="codeph"> kek</span> ou <span class="codeph"> contentKey</span> pode ser especificado </td> 
  </tr> 
 </tbody> 
</table>
