---
description: Trabalhe com o SEES para ver como ativar um serviço de direito baseado em tempo usando o ExpressPlay.
title: Direito baseado no tempo do serviço de referência
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Serviço de Referência: Direito com Base no Tempo {#reference-service-time-based-entitlement}

Trabalhe com o SEES para ver como ativar um serviço de direito baseado em tempo usando o ExpressPlay.

O SEES recebe uma solicitação de direito (consulte a seção API pública) do cliente. O servidor SEES procura o CEK e o IV com base no `contentID`, adiciona o `expirationTime`e encaminha a solicitação ao servidor ExpressPlay. O token final do ExpressPlay é vinculado ao tempo. Consulte o diagrama de sequência Qualificações com base no tempo abaixo. ![](assets/fees-time-based.png)

**Tabela 1: Parâmetros de licença enviados pelo cliente**

| Parâmetro da consulta | Descrição | Obrigatório |
|---|---|---|
| `contentKey` | Uma representação de string hexadecimal de 16 bytes da chave de criptografia de conteúdo | Sim |
| `iv` | Uma representação de string hexadecimal de 16 bytes da criptografia de conteúdo IV | Sim |
| `rentalDuration` | Duração da locação em segundos (padrão = 0) | Não |

**Tabela 2: Parâmetros de Restrição de Token adicionados pelo SEES Server**

<table id="table_E979FAD7A61A4832A46667301939FAEB">  
 <thead> 
  <tr> 
   <th class="entry"> Parâmetro da consulta </th> 
   <th class="entry"> Descrição </th> 
   <th class="entry"> Obrigatório? </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> expirationTime</span> </td> 
   <td>Hora de expiração deste token. Este valor deve ser uma sequência de caracteres em <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a> formato de data/hora no designador de zona 'Z' ("Hora Zulu") ou um número inteiro precedido por um sinal '+'. Um exemplo de data/hora RFC 3339 é <span class="codeph"> 2006-04-14T12:01:10Z</span>. <p>Se o valor for uma string no formato de data/hora RFC 3339, ele representará uma data/hora de expiração absoluta do token. Se o valor for um número inteiro precedido por um sinal '+', ele será interpretado como um número relativo de segundos a partir da emissão de que o token é válido. Por exemplo, <span class="codeph"> +60</span> especifica um minuto. O tempo de vida máximo do token (e padrão, se não especificado) é de 30 dias. Use o formulário codificado "%2B" ao especificar o sinal "+". </p> </td> 
   <td> Não </td> 
  </tr> 
 </tbody> 
</table>
