---
description: A interface do token de licença do FairPlay fornece serviços de produção e teste.
seo-description: A interface do token de licença do FairPlay fornece serviços de produção e teste.
seo-title: Solicitação / resposta do token de licença do FairPlay
title: Solicitação / resposta do token de licença do FairPlay
uuid: 10d4a760-8895-4fb3-8288-1c3a640df587
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 5%

---


# Resposta e solicitação de token de licença do FairPlay {#fairplay-license-token-request-response}

A interface do token de licença do FairPlay fornece serviços de produção e teste. Esta solicitação retorna um token que pode ser resgatado para uma licença do FairPlay.

**Método: GET, POST** (com um corpo codificado www-url que contém parâmetros para ambos os métodos)

**URLs:**

* **Produção:** `https://fp-gen.{prod_domain}/hms/fp/token`

* **Teste:** `https://fp-gen.test.expressplay.com/hms/fp/token`

* **Solicitação de amostra:**

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

* **Resposta de exemplo:**

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

**Parâmetros de Query de solicitação**

**Quadro 3: Parâmetros do Query de token**

| Parâmetro do query | Descrição | Obrigatório? |
|--- |--- |--- |
| customerAuthenticator Autenticador Cliente como parâmetro de query customerAuthenticator FairPlay | Esta é a chave da API do cliente, uma para cada ambiente de produção e teste. Isso pode ser encontrado na guia ExpressPlay Admin Painel. | Sim |
| errorFormat | Ou html ou json. Se html (o padrão) uma representação HTML de quaisquer erros é fornecida no corpo da entidade da resposta. Se json for especificado, uma resposta estruturada no formato JSON será retornada. Consulte Erros [](https://www.expressplay.com/developer/restapi/#json-errors) JSON para obter detalhes. O tipo mime da resposta é text/uri-lista em caso de sucesso, text/html para formato de erro HTML ou application/json para formato de erro JSON. | Não |

**Tabela 4: Parâmetros de Query de licença**

| **Parâmetro do query** | **Descrição** | **Obrigatório?** |
|---|---|---|
| `generalFlags` | Uma string hexadecimal de 4 bytes que representa os sinalizadores de licença. &quot;0000&quot; é o único valor permitido. | Não |
| `kek` | Chave de criptografia de chave (KEK). As chaves são armazenadas criptografadas com um KEK usando um algoritmo de quebra automática de chave (AES Key Wrap, RFC3394). Se `kek` for fornecido, é necessário fornecer um dos parâmetros `kid` ou os `ek` , *mas não ambos*. | Não |
| `kid` | Uma representação de string hexadecimal de 16 bytes da chave de criptografia de conteúdo ou de uma string `'^somestring'`. O comprimento da string seguido pelo `'^'` não pode ser maior que 64 caracteres. | Não |
| `ek` | Uma representação hexadecimal da chave de conteúdo criptografada. | Não |
| `contentKey` | Uma representação de string hexadecimal de 16 bytes da chave de criptografia de conteúdo | Sim, a menos que o `kek` e `ek` ou `kid` sejam fornecidos. |
| `iv` | Uma representação de string hexadecimal de 16 bytes da criptografia de conteúdo IV | Sim |
| `rentalDuration` | Duração do aluguer em segundos (padrão - 0) | Não |
| `fpExtension` | Um empacotamento de formulário curto `extensionType` e `extensionPayload`, como uma string separada por vírgulas. Por exemplo: […] `&fpExtension=wudo,AAAAAA==&`[…] | Não, qualquer número pode ser usado |

**Quadro 5: Parâmetros de Query de restrição de token**

<table id="table_ar3_lsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Parâmetro do query</b> </th> 
   <th class="entry"> <b>Descrição</b> </th> 
   <th class="entry"> <b>Obrigatório?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> expirationTime </span> </td> 
   <td> Tempo de expiração deste token. Esse valor DEVE ser uma string no formato de data/hora <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> no designador de zona ‘Z’ ("Tempo Zulu") ou um número inteiro precedido por um sinal '+'. Um exemplo de uma data/hora RFC 3339 é <span class="codeph"> 2006-04-14T12:01:10Z </span>. <p>Se o valor for uma string no formato de data/hora <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> , isso representará uma data/hora de expiração absoluta para o token. Se o valor for um número inteiro precedido por um sinal '+', então ele será interpretado como um número relativo de segundos, desde a emissão, de que o token é válido. </p> Por exemplo, <span class="codeph"> +60 </span> especifica um minuto. A duração máxima e padrão do token (se não especificada) é de 30 dias. </td> 
   <td> Não </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 6: Parâmetros de Query de correlação**

| **Parâmetro do query** | **Descrição** | **Obrigatório?** |
|---|---|---|
| `cookie` | Uma string arbitrária com até 32 caracteres, mantida no token e registrada pelo servidor de resgate de token. Isso pode ser usado para correlacionar entradas de log no servidor de resgate e as entradas nos servidores do provedor de serviço. | Não |

**Resposta**

**Quadro 7: Respostas HTTP**

| **Código de status HTTP** | **Descrição** | **Tipo de conteúdo** | **Corpo da Entidade Contém** |
|---|---|---|---|
| `200 OK` | Nenhum erro. | `text/uri-list` | URL de aquisição de licença + token |
| `400 Bad Request` | Argumentos inválidos | `text/html` ou `application/json` | Descrição do erro |
| `401 Unauthorized` | Falha na autenticação | `text/html` ou `application/json` | Descrição do erro |
| `404 Not found` | URL incorreto | `text/html` ou `application/json` | Descrição do erro |
| `50x Server Error` | Erro do servidor | `text/html` ou `application/json` | Descrição do erro |

**Quadro 8: Códigos de erro de evento**

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
   <td> Token de autenticação inválido: &lt;details&gt; <p>Observação:  Isso pode acontecer se o autenticador estiver incorreto ou ao acessar a API de teste em <span class="filepath"> *.test.expresplay.com </span> usando o autenticador de produção e vice-versa. </p> <p importance="high">Observação:  O SDK de teste e a ATT (Advanced Test Tool) funcionam somente com <span class="filepath"> *.test.express.com </span>, enquanto os dispositivos de produção devem usar <span class="filepath"> *.service.express.play.com </span>. </p> </td> 
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
   <td> Criança ausente </td> 
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
   <td> <span class="codeph"> o garoto </span> deve ter 64 caracteres depois do ^ </td> 
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
   <td> -6001 </td> 
   <td> Parâmetros <span class="codeph"> FPExtension inválidos </span> especificados </td> 
  </tr> 
  <tr> 
   <td> -6002 </td> 
   <td> Tipo de token FP inválido </td> 
  </tr> 
  <tr> 
   <td> -6003 </td> 
   <td> Foi especificado um parâmetro <span class="codeph"> iv </span> inválido </td> 
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
   <td> Serviço não autorizado para suporte do FairPlay </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> Duração de aluguer inválida especificada </td> 
  </tr> 
  <tr> 
   <td> -6008 </td> 
   <td> O vínculo de ID de dispositivo não é compatível com o FairPlay </td> 
  </tr> 
  <tr> 
   <td> -6009 </td> 
   <td> Opção FairPlay desativada </td> 
  </tr> 
 </tbody> 
</table>