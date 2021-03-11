---
description: Trabalhe com o SEES para ver como habilitar um serviço de direito baseado em tempo usando o ExpressPlay.
title: Direito baseado no tempo do serviço de referência
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# Serviço de referência: Direito baseado no tempo {#reference-service-time-based-entitlement}

Trabalhe com o SEES para ver como habilitar um serviço de direito baseado em tempo usando o ExpressPlay.

O SEES recebe uma Solicitação de direito (consulte a seção API pública ) do cliente. O servidor SEES procura o CEK e o IV com base no `contentID`, adiciona o `expirationTime` e encaminha a solicitação ao servidor ExpressPlay. O token final do ExpressPlay é vinculado ao tempo. Consulte o diagrama de sequência de Direitos Baseados em Tempo abaixo. ![](assets/fees-time-based.png)

**Quadro 1: Parâmetros de licença enviados pelo cliente**

| Parâmetro de consulta | Descrição | Obrigatório |
|---|---|---|
| `contentKey` | Uma representação de string hexadecimal de 16 bytes da chave de criptografia de conteúdo | Sim |
| `iv` | Uma representação de string hexadecimal de 16 bytes da criptografia de conteúdo IV | Sim |
| `rentalDuration` | Duração do aluguel em segundos (padrão = 0) | Não |

**Quadro 2: Parâmetros de restrição de token adicionados pelo servidor SEES**

<table id="table_E979FAD7A61A4832A46667301939FAEB">  
 <thead> 
  <tr> 
   <th class="entry"> Parâmetro de consulta </th> 
   <th class="entry"> Descrição </th> 
   <th class="entry"> Obrigatório? </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> expirationTime</span> </td> 
   <td>Hora de expiração desse token. Esse valor deve ser uma string no formato <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a> data/hora no designador de zona 'Z' ("Zulu time") ou um inteiro precedido por um sinal '+'. Um exemplo de uma data/hora RFC 3339 é <span class="codeph"> 2006-04-14T12:01:10Z</span>. <p>Se o valor for uma string no formato RFC 3339 de data/hora, então representa uma data/hora de expiração absoluta para o token. Se o valor for um inteiro precedido por um sinal '+', ele será interpretado como um número relativo de segundos a partir da emissão de que o token é válido. Por exemplo, <span class="codeph"> +60</span> especifica um minuto. O tempo de vida máximo (e padrão, se não especificado) do token é de 30 dias. Use o formulário codificado "%2B" ao especificar o sinal "+". </p> </td> 
   <td> Não </td> 
  </tr> 
 </tbody> 
</table>

