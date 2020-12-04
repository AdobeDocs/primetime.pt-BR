---
description: A interface do token de licença PlayReady fornece serviços de produção e teste.
seo-description: A interface do token de licença PlayReady fornece serviços de produção e teste.
seo-title: Solicitação / resposta do token de licença PlayReady
title: Solicitação / resposta do token de licença PlayReady
uuid: 20ebd582-ebb9-4716-8c1e-df3e58d6ec14
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 3%

---


# Solicitação de token de licença PlayReady / resposta {#playready-license-token-request-response}

A interface do token de licença PlayReady fornece serviços de produção e teste.

Esta solicitação HTTP retorna um token que pode ser resgatado para uma licença PlayReady.

**Método: GET, POST** (com um corpo codificado www-url que contém parâmetros para ambos os métodos)

**URLs:**

* **Produção:** `https://pr-gen.{prod_domain}/hms/pr/token`

* **Teste:** ` [https://pr-gen.test.expressplay.com/hms/pr/token](https://pr-gen.test.expressplay.com/hms/pr/token)`

* **Solicitação de amostra:**

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

* **Resposta de exemplo:**

   ```
   {"licenseAcquisitionUrl":"https://expressplay-licensing.axprod.net/LicensingService.ashx",
               "token":"<base64-encoded ExpressPlay token>"}
   ```

## Solicitar parâmetros de Query {#section_26F8856641A64A46A3290DBE61ACFAD2}

**Quadro 9: Parâmetros do Query de token**

<table id="table_zxg_dyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Parâmetro do query</b> </th> 
   <th class="entry"><b>Descrição</b> </th> 
   <th class="entry"><b>Obrigatório?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> customerAuthenticator</span> </td> 
   <td> <p>Esta é a chave da API do cliente, uma para cada ambiente de produção e teste. Isso pode ser encontrado na guia ExpressPlay Admin Painel. </p> </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> errorFormat</span> </td> 
   <td><span class="codeph"> html</span> ou <span class="codeph"> json</span>. Se <span class="codeph"> html</span> (o padrão) uma representação HTML de quaisquer erros for fornecida no corpo da entidade da resposta. <p>Se <span class="codeph"> json</span> for especificado, uma resposta estruturada no formato JSON será retornada. Consulte <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> Erros JSON</a> para obter detalhes. </p> <p>O tipo mime da resposta é <span class="codeph"> text/uri-lista</span> quando bem-sucedido, <span class="codeph"> text/html</span> para o formato de erro HTML ou <span class="codeph"> application/json</span> para o formato de erro JSON. </p> </td> 
   <td> Não </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 10: Parâmetros de Query de licença**

<table id="table_f1l_fyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Parâmetro do query</b> </th> 
   <th class="entry"><b>Descrição</b> </th> 
   <th class="entry"><b>Obrigatório?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> generalFlags</span> </td> 
   <td>Uma string hexadecimal de 4 bytes que representa os sinalizadores de licença. Deve ser fixado em "00000001" para uma licença persistente. <p>Observação: As licenças de aluguel (<span class="codeph"> rightsType=Rental</span>) DEVEM ser persistentes. </p> </td> 
   <td> Não </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> chave</span> </td> 
   <td> Chave de criptografia de chave (KEK). As chaves são armazenadas criptografadas com um KEK usando um algoritmo de quebra automática de chave (AES Key Wrap, RFC3394). </td> 
   <td> Não </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> criança</span> </td> 
   <td>Uma representação de string hexadecimal de 16 bytes da chave de criptografia de conteúdo ou uma string <span class="codeph"> ^somestring'</span>. O comprimento da string seguido pelo '^' não pode ser maior que 64 caracteres. </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> ek</span> </td> 
   <td> Uma representação hexadecimal da chave de conteúdo criptografada. </td> 
   <td> Não </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> contentKey</span> </td> 
   <td> Uma representação de string hexadecimal de 16 bytes da chave de criptografia de conteúdo </td> 
   <td>Sim, a menos que <span class="codeph"> kek</span> e <span class="codeph"> ek</span> ou <span class="codeph"> child</span> sejam fornecidos </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rightsType</span> </td> 
   <td>Especifica o tipo de direitos. Deve ser <span class="codeph"> BuyToOwn</span> ou <span class="codeph"> Aluguer</span>. </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> lease.periodEndTime</span> </td> 
   <td>Data de término do aluguel. Esse valor DEVE estar no formato ‘RFC 3339' _ data/hora no formato designador de zona ‘Z’ ("Hora Zulu"), ou um número inteiro precedido por um sinal '+'. <p>Se o valor for um formato de data/hora <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339</a>, então ele representa uma data/hora de expiração absoluta para a licença. Um exemplo de uma data/hora RFC 3339 é 2006-04-14T12:01:10Z. </p> <p> Se o valor for um número inteiro precedido por um sinal '+', ele será tomado como um número relativo de segundos a partir do momento em que o token é emitido. O conteúdo não pode ser reproduzido depois desse tempo. Só é válido se <span class="codeph"> rightsType</span> for <span class="codeph"> Aluguel</span>. </p> </td> 
   <td>Sim, quando <span class="codeph"> rightsType</span> for <span class="codeph"> Aluguel</span>. </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> lease.playDuration</span> </td> 
   <td>Tempo, em segundos, que o conteúdo pode ser reproduzido assim que a reprodução for iniciada. Só é válido se <span class="codeph"> rightsType</span> for Aluguel. </td> 
   <td> Não </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> análogoVideoOPL</span> </td> 
   <td> Valor inteiro para indicar o Nível de proteção de saída para vídeo analógico. Intervalo válido 0-999. </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compactadoDigitalAudioOPL</span> </td> 
   <td> Valor inteiro para indicar o Nível de proteção de saída para áudio digital compactado. Intervalo válido 0-999. </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compactadoDigitalVideoOPL</span> </td> 
   <td> Valor inteiro para indicar o Nível de proteção de saída para vídeo digital compactado. Intervalo válido 0-999. </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalAudioOPL</span> </td> 
   <td> Valor inteiro para indicar o Nível de proteção de saída para áudio digital descompactado. Intervalo válido 0-999. </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressDigitalVideoOPL</span> </td> 
   <td> Valor inteiro para indicar o Nível de proteção de saída para vídeo digital descompactado. Intervalo válido 0-999. </td> 
   <td> Sim </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> unknownOutputBehavior</span> </td> 
   <td>Comportamento obrigatório quando a saída é desconhecida. Valores permitidos: <span class="codeph"> Permitir</span>, <span class="codeph"> Não permitir</span> ou <span class="codeph"> SDOnly</span> </td> 
   <td> Não </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlags</span> </td> 
   <td> Um valor hexadecimal de 4 bytes para indicar os sinalizadores para outras opções de controle de saída </td> 
   <td> Não </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionType</span> </td> 
   <td>Uma palavra de 4 letras arbitrária que representa um identificador de 32 bits para uma extensão. O código ASCII de 8 bits de cada letra é a parte correspondente de 8 bits do identificador. Por exemplo, o valor do identificador 0x61626364 (hexadecimal) seria gravado como ‘<span class="codeph"> abcd</span>’, pois o código ASCII para ‘a' é 0x61, etc. </td> 
   <td> Não </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionPayload</span> </td> 
   <td> Uma string codificada em base64 da Extensão. </td> 
   <td>Sim, quando <span class="codeph"> extensionType</span> for especificado. </td> 
  </tr> 
 </tbody> 
</table>

## Respostas {#section_0079C31B4AF14DBBB6277CF251FB90E3}

**Quadro 11: Respostas HTTP**

| **Código de status HTTP** | **Descrição** | **Tipo de conteúdo** | **Corpo da Entidade Contém** |
|---|---|---|---|
| `200 OK` | Nenhum erro. | `text/uri-list` | URL e token de aquisição de licença |
| `400 Bad Request` | Argumentos inválidos | `text/html` ou  `application/json` | Descrição do erro |
| `401 Unauthorized` | Falha na autenticação | `text/html` ou  `application/json` | Descrição do erro |
| `404 Not found` | URL inválido | `text/html` ou  `application/json` | Descrição do erro |
| `50x Server Error` | Erro do servidor | `text/html` ou  `application/json` | Descrição do erro |

**Quadro 12: Códigos de erro de evento**

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
   <td>Token de autenticação inválido: &lt;details&gt; <p>Observação:  Isso pode acontecer se o autenticador estiver incorreto ou ao acessar a API de teste em *.test.express.com usando o autenticador de produção e vice-versa. </p> <p importance="high">Observação: O SDK de teste e a ATT (Advanced Test Tool) funcionam somente com <span class="filepath"> *.test.express.com</span>, enquanto os dispositivos de produção devem usar <span class="filepath"> *.service.express.com</span>. </p> </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> Tokens insuficientes disponíveis </td> 
  </tr> 
  <tr> 
   <td> -2020 </td> 
   <td> Tipo de direitos ausentes </td> 
  </tr> 
  <tr> 
   <td> -2021 </td> 
   <td> Tipo de direitos inválido </td> 
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
   <td> Conta desabilitada de serviço </td> 
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
   <td><span class="codeph"> O </span> OutputControlFlagt deve ter a codificação de 4 bytes </td> 
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
   <td> -4018 </td> 
   <td>Falta <span class="codeph"> criança</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Falha ao obter a chave de conteúdo do serviço de armazenamento de chave </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> deve ter 32 caracteres </span> hexadecimais </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> deve ter </span> 64 caracteres depois do ^ </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td><span class="codeph"> subordinado</span> inválido </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>Chave <span class="codeph"> criptografada inválida</span> ou chave </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> Erro de tipo de saída inválido </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> A opção PlayReady está desativada para este serviço </td> 
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
   <td>Apenas é possível especificar <span class="codeph"> kek</span> ou <span class="codeph"> contentKey</span> </td> 
  </tr> 
 </tbody> 
</table>
