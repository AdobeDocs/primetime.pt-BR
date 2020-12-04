---
seo-title: Uso da linha de comando
title: Uso da linha de comando
uuid: 1c3a450d-5d9c-4437-89dd-1bd8719268b7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# Uso da linha de comando {#command-line-usage}

O Gerenciador de Listas de Atualização de Política está no diretório \Reference Implementation\Command Line Tools no DVD. Para criar uma lista de atualização de política, use a seguinte sintaxe:

```
    java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` indica onde a lista de atualização de política será gravada.

Para visualização de uma lista de atualização de política existente, use a seguinte sintaxe:

```
    java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

A tabela a seguir contém descrições das opções de linha de comando mostradas na sintaxe acima:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opção de linha de comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o local do arquivo de configuração. Se essa opção não for usada, o Gerenciador de Listas de Atualização de Política procurará <span class="filepath"> flashaccess stools.properties </span> no diretório de trabalho. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d nome do arquivo  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Exibe informações sobre a lista de atualização de política. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> Data -e  </span> </td> 
   <td colname="2" class="- topic/entry "> (Opcional) A data de expiração da lista de atualização da política. Use o formato <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> ou <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:sec </span> (por exemplo, 2009-01-31-14:30:00 representa 31 de janeiro às 14:30). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f filename [certfile]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Adiciona todas as entradas da lista de atualização de política existente. Somente um arquivo existente pode ser especificado. </p> <p class="- topic/p ">Se essa lista existente tiver sido assinada com uma credencial diferente daquela usada para assinar a nova lista, especifique seu arquivo de certificado, para que sua assinatura possa ser verificada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e <span class="codeph"> -o </span> não estiver definido, um erro será retornado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se o arquivo de destino já existir, substitua-o sem solicitar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r  </span> <span class="+ topic/ph pr-d/codeph codeph"> data policyID  </span> "  <span class="+ topic/ph pr-d/codeph codeph"> reasonCode  </span>" "  <span class="+ topic/ph pr-d/codeph codeph"> reasonText  </span>" "  <span class="+ topic/ph pr-d/codeph codeph"> reasonURL  </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) Revoga a ID da política na data especificada. Um código de motivo opcional, texto de motivo e URL de motivo também podem ser fornecidos. Especifique uma string vazia "" para indicar que nenhum valor é fornecido para os parâmetros opcionais. Especifique a data como <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> ou <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:sec </span> (por exemplo, 2008-12-1 ou 2008-12-1-00:00:00 para meia-noite de 1º de dezembro 008). Se uma data não for especificada, a data atual será usada. O código de motivo deve ser maior ou igual a 0. Várias opções -r podem ser especificadas. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> data </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Executa a mesma ação que o sinalizador -r, mas extrai o identificador de política do arquivo especificado. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL"  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Substitui qualquer política correspondente em uma solicitação de licença por essa política usando o código de motivo fornecido (opcional), o texto do motivo (opcional) e o URL do motivo (opcional). </p> <p>Especifique uma string vazia "" para indicar que nenhum valor é fornecido para os parâmetros opcionais. </p> <p>O código de motivo deve ser maior ou igual a <span class="codeph"> 0 </span>. Várias opções <span class="codeph"> -u </span> podem ser especificadas. </p> </td> 
  </tr> 
 </tbody> 
</table>

