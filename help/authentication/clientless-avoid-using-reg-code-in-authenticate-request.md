---
title: Evite usar '&'reg_code na solicitação /authentication
description: Evite usar '&'reg_code na solicitação /authentication
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Evite usar &#39;&amp;&#39;reg_code na solicitação /authentication {#clientless-avoid-using-reg_code-in-authenticate-request}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>



## Problema

O navegador IE 9 interpreta &#39;\®&#39; como um comando especial e o converte para ®. 

## Explicação

Se a variável `/authenticate` A solicitação é composta da seguinte maneira...

 

```
    <FQDN>authenticate? requestor_id=someRequestor&reg_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

...ele será interpretado pelo navegador IE como abaixo e será enviado ao Adobe neste formato:

 

```
    <FQDN>authenticate?requestor_id=someRequestor&reg;_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

O solicitante\_id será interpretado como univision®\_code=EKAFMFI, pois não há &#39;&amp;&#39; e o Adobe não encontrará um `regCode` param para associar o token.  Há uma chance de o token AuthN não ser criado, nesse caso `/checkauthn` as chamadas não encontrarão tokens.



## Solução

Uma das opções a seguir deve resolver esse problema:

1. Evite usar o `&reg_code` parâmetro entre os outros parâmetros da string de consulta.  Em vez disso, mova-o para o primeiro parâmetro da string de consulta no URL da solicitação, tornando o url da solicitação assim:\
    

       &lt;fqdn>autentica?reg_code =EKAFMFI&amp;requestor_id=someRequestor&amp;domain_name=someRequestor.com&amp;noflash=true&amp;mso_id=someMvpd&amp;redirect_url=someRequestor.redirect.url.html
   

   Dessa forma, o `&reg` param não será interpretado incorretamente.

1. Normalizar `&reg_code` como usar `&amp;reg_code`.

1. O Adobe poderia introduzir um novo recurso para enviar um código de erro de volta para a segunda tela em resposta a uma chamada de autenticação, se a criação do token AuthN falhasse.

