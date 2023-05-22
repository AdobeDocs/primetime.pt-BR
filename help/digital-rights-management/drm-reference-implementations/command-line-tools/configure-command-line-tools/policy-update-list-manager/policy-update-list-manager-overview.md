---
title: Visão geral
description: Visão geral
copied-description: true
exl-id: 1e06bead-4b45-4bf0-8bcf-1ea376af6bd8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Gerenciador de Lista de Atualização de Política DRM {#policy-update-list-manager}

Usar a ferramenta de linha de comando Gerenciador de Lista de Atualização de Política DRM do Primetime ( [!DNL AdobePolicyUpdateListManager.jar]) para criar e gerenciar listas de atualização de política DRM e verificar se as políticas foram atualizadas ou revogadas.

Antes de executar a ferramenta de linha de comando Policy Update List Manager, defina as propriedades na *Propriedades do Gerenciador de Listas de Atualização de Políticas e do Gerenciador de Listas de Revogação* seção do seu arquivo de configuração.

>[!NOTE]
>
>Você também pode especificar todas as propriedades do Policy Update List Manager a partir da linha de comando.

## Uso da linha de comando do Gerenciador de Lista de Atualização de Políticas {#policy-update-list-manager-command-line-usage}

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

* `destfile` indica o nome do arquivo no qual a lista de atualização de política DRM é gravada.

**Exibir uma lista de atualização de política existente:**

```
java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

* `filename` O nome do arquivo da lista de atualização de política.

**Tabela 4: Opções da linha de comando**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opção de linha de comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o nome e o local do arquivo de configuração. </p> <p class="- topic/p ">Se você não especificar um nome ou um local, o Gerenciador de Lista de Atualização de Política DRM procurará <span class="filepath"> flashaccesstools.properties </span> no diretório de trabalho atual. </p> <p>Observação: As opções especificadas na linha de comando têm prioridade sobre as opções especificadas no arquivo de configuração. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d nome do arquivo </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Exibe informações sobre a lista de atualização de política DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e data </span> </td> 
   <td colname="2" class="- topic/entry "> <p>(Opcional) A data de expiração da lista de atualização da política DRM. </p> <p>Usar o formato <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> ou <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span> (por exemplo, 31-01-2009):30:00 representa 31 de janeiro às 14h30). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f nome do arquivo [certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Adiciona todas as entradas da lista de atualização de política DRM existente. Você só pode especificar um arquivo existente. </p> <p class="- topic/p ">Se a lista existente tiver sido assinada com uma credencial diferente da que está sendo usada para assinar a nova lista, será necessário especificar o arquivo de certificado para verificar a assinatura. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e <span class="codeph"> -o </span> não estiver definido, ocorrerá um erro. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se o arquivo de destino já existir, substitua-o sem avisar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID </span> <span class="+ topic/ph pr-d/codeph codeph"> data </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) Revoga a ID da política DRM na data especificada. Você pode fornecer um código de motivo opcional, texto do motivo e URL do motivo. Você precisa especificar uma string vazia " " para indicar que nenhum valor é fornecido para os parâmetros opcionais. Você pode especificar a data em <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> ou <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span> nesses formatos. Por exemplo, 2008-12-1 ou 2008-12-1-00:00:00 representa meia-noite de 1º de dezembro de 2008). Se você não especificar uma data, a data atual será aplicada automaticamente. Portanto, o código de motivo deve ser maior ou igual a 0. Você também pode especificar várias opções -r. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> data </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Executa a mesma ação que a variável <span class="codeph"> -r </span> opção. No entanto, ele extrai o identificador de política DRM de um arquivo especificado. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Substitui qualquer política DRM correspondente em uma solicitação de licença por esta política DRM usando o código do motivo fornecido (opcional), o texto do motivo (opcional) e a URL do motivo (opcional). </p> <p>Uma string vazia "" indica que você não forneceu nenhum valor para os parâmetros opcionais. </p> <p>O código de motivo deve ser maior ou igual a <span class="codeph"> 0 </span>. É possível especificar vários <span class="codeph"> -u </span> opções. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Propriedades de configuração {#configuration-properties}

As propriedades do Gerenciador de Lista de Atualização de Política DRM do Primetime a seguir especificam um arquivo PKCS12 que inclui credenciais para assinar listas de revogação (Certificado de Servidor de Licença), juntamente com uma senha.

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`
