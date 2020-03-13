---
description: Trabalhe com o SEES para ver como habilitar um serviço de direito baseado em tempo usando o ExpressPlay.
seo-description: Trabalhe com o SEES para ver como habilitar um serviço de direito baseado em tempo usando o ExpressPlay.
seo-title: Direito baseado em tempo do serviço de referência
title: Direito baseado em tempo do serviço de referência
uuid: dd937299-a271-49a9-9b26-eec16f1484df
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Serviço de referência: Direito baseado em tempo {#reference-service-time-based-entitlement}

Trabalhe com o SEES para ver como habilitar um serviço de direito baseado em tempo usando o ExpressPlay.

O SEES recebe uma Solicitação de direito (consulte a seção API pública) do cliente. O servidor SEES procura o CEK e o IV com base no `contentID`, adiciona o `expirationTime`e encaminha a solicitação para o servidor ExpressPlay. O token final do ExpressPlay é vinculado ao tempo. Consulte o diagrama de sequência de autorização com base em tempo abaixo. ![](assets/fees-time-based.png)

**Tabela 1: Parâmetros de licença enviados pelo cliente**

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
   <td>Tempo de expiração deste token. Esse valor deve ser uma string no formato <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a> date/time no designador de zona 'Z' ("Zulu time") ou um número inteiro precedido por um sinal '+'. Um exemplo de uma data/hora RFC 3339 é <span class="codeph"> 2006-04-14T12:01:10Z</span>. <p>Se o valor for uma string no formato de data/hora RFC 3339, isso representa uma data/hora de expiração absoluta para o token. Se o valor for um número inteiro precedido por um sinal '+', então ele será interpretado como um número relativo de segundos após a emissão que o token será válido. Por exemplo, <span class="codeph"> +60</span> especifica um minuto. A duração máxima (e padrão, se não especificada) do token é de 30 dias. Use o formulário codificado "%2B" ao especificar o sinal '+'. </p> </td> 
   <td> Não </td> 
  </tr> 
 </tbody> 
</table>

