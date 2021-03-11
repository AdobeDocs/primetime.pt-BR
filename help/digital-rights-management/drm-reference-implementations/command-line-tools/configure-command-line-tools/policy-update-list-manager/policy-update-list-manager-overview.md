---
title: Visão geral
description: Visão geral
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# Gerenciador de lista de atualização de política DRM {#policy-update-list-manager}

Use a ferramenta de linha de comando do Gerenciador de lista de atualização da política DRM Primetime ( [!DNL AdobePolicyUpdateListManager.jar]) para criar e gerenciar listas de atualização da política DRM e verificar se as políticas foram atualizadas ou revogadas.

Antes de executar a ferramenta de linha de comando Gerenciador de Lista de Atualização de Política, você deve definir propriedades na seção *Gerenciador de Lista de Atualização de Política e Propriedades* do Gerenciador de Lista de Revogação do arquivo de configuração.

>[!NOTE]
>
>Também é possível especificar todas as propriedades do Gerenciador de Lista de Atualização de Política na linha de comando.

## Uso da linha de comando do Gerenciador de Lista de Atualização de Política {#policy-update-list-manager-command-line-usage}

**Criar uma lista de atualização de política:**

```
java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` indica o nome do arquivo no qual a lista de atualização da política de DRM é gravada.

**Exibir uma lista de atualização de política existente:**

```
java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

* `filename` O nome do arquivo da lista de atualização de política.

**Quadro 4: Opções de linha de comando**

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o nome e o local do arquivo de configuração. </p> <p class="- topic/p ">Se você não especificar um nome ou um local, o Gerenciador de lista de atualização da política de DRM procura <span class="filepath"> flashaccess.properties </span> no diretório de trabalho atual. </p> <p>Observação:  As opções especificadas na linha de comando têm prioridade sobre as opções especificadas no arquivo de configuração. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d nome do arquivo  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Exibe informações sobre a lista de atualização da política de DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> data -e  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>(Opcional) A data de expiração da lista de atualização da política de DRM. </p> <p>Use o formato <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> ou <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:sec </span> (por exemplo, 2009-01-31-14:30:00 representa 31 de janeiro às 2:30 PM). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f filename [certfile]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Adiciona todas as entradas da lista de atualização da política de DRM existente. Você só pode especificar um arquivo existente. </p> <p class="- topic/p ">Se a lista existente tiver sido assinada com uma credencial diferente da usada para assinar a nova lista, será necessário especificar o arquivo de certificado para verificar a assinatura. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e <span class="codeph"> -o </span> não estiver definido, ocorrerá um erro. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se o arquivo de destino já existir, substitua-o sem solicitar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID  </span> <span class="+ topic/ph pr-d/codeph codeph"> date  </span> "  <span class="+ topic/ph pr-d/codeph codeph"> reasonCode  </span>" "  <span class="+ topic/ph pr-d/codeph codeph"> reasonText  </span>" "  <span class="+ topic/ph pr-d/codeph codeph"> reasonURL  </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) Revoga a ID da política de DRM na data especificada. Você pode fornecer um código de motivo opcional, texto do motivo e URL do motivo. Você precisa especificar uma string vazia "" para indicar que nenhum valor é fornecido para os parâmetros opcionais. É possível especificar a data em <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> ou <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:sec </span> nesses formatos. Por exemplo, 2008-12-1 ou 2008-12-1-00:00:00 representa meia-noite em 1° de dezembro de 2008). Se você não especificar uma data, a data atual será aplicada automaticamente. Portanto, o código do motivo deve ser maior ou igual a 0. Também é possível especificar várias opções -r. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> data </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Executa a mesma ação da opção <span class="codeph"> -r </span>. No entanto, ele extrai o identificador de política de DRM de um arquivo especificado. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL"  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Substitui qualquer política de DRM correspondente em uma solicitação de licença por essa política de DRM usando o código de motivo fornecido (opcional), o texto do motivo (opcional) e o URL do motivo (opcional). </p> <p>Uma string vazia "" indica que você não forneceu qualquer valor para os parâmetros opcionais. </p> <p>O código do motivo deve ser maior ou igual a <span class="codeph"> 0 </span>. Você pode especificar várias opções <span class="codeph"> -u </span>. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Propriedades de configuração {#configuration-properties}

As seguintes propriedades do Gerenciador de lista de atualização da política de DRM do Primetime especificam um arquivo PKCS12 que inclui credenciais para a assinatura de listas de revogação (Certificado do Servidor de Licenças), juntamente com uma senha.

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`