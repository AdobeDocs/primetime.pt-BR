---
title: Uso da linha de comando do Policy Manager
description: Uso da linha de comando do Policy Manager
copied-description: true
exl-id: 888be282-7eaa-4101-b4b1-4f8df99a967a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 0%

---

# Uso da linha de comando do Policy Manager {#policy-manager-command-line-usage}

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

**Tabela 1: Comandos**

| Comando | Descrição |
|---|---|
| `new` | Cria uma nova política DRM |
| `detail` | Descreve uma política DRM existente |
| `update` | Atualiza uma política DRM existente |

**Tabela 2: Opções**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opção de linha de comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o nome e o local do arquivo de configuração. </p> <p class="- topic/p ">Se você não especificar um nome ou um local, o DRM Policy Manager procurará <span class="filepath"> flashaccesstools.properties </span> no diretório de trabalho atual. </p> <p>Observação: As opções especificadas na linha de comando têm prioridade sobre as opções especificadas no arquivo de configuração. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se o arquivo de destino existir, você poderá substituí-lo sem ser solicitado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino existir e <span class="codeph"> -o </span> não estiver definido, ocorrerá um erro. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que a política DRM tem uma licença raiz. </p> <p class="- topic/p ">Esta opção não está disponível para atualizações. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e data </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data antes das licenças se torna válida. </p> <p>Você pode especificar a data em <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> ou <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span> formato. Por exemplo, 2008-12-1 ou 2008-12-1-00:00:00 para meia-noite de 1º de dezembro de 2008. </p> <p> 
     <ul id="ul_D5DB5044756D4BD6A734813971598425"> 
      <li id="li_B6BD62A524384060A9DDA14FF50936FA">O valor deve ser maior que o valor de <span class="codeph"> -s </span> se presente. </li> 
      <li id="li_C3C5AD0231A240EC9AC57685B9206E8D">Não é possível aplicar esta opção com <span class="codeph"> -r </span>. </li> 
      <li id="li_3790E2F829A149979BF44E0914CFF431">Para remover a data final ao atualizar uma política DRM, aplique <span class="codeph"> -e </span> sem especificar uma data. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r minutos </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A duração em minutos da validade do conteúdo protegido. </p> <p class="- topic/p ">A política DRM se torna válida quando o conteúdo é protegido com o empacotador. </p> <p> 
     <ul id="ul_4690A0E4677A4DF6A006B7FCBD46F1BE"> 
      <li id="li_D1F098D44B494EE7A8647C0B62D5ACFA">O valor deve ser não negativo. </li> 
      <li id="li_ADFDCB01EEE04B37AFA42886AAEF47EB">Não é possível aplicar esta opção juntamente com <span class="codeph"> -e </span>. </li> 
      <li id="li_E80563E68BEB43FC9E29A694594CAE01">Para remover ou excluir a duração ao atualizar uma política DRM, aplique <span class="codeph"> -r </span> sem especificar minutos. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s data </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data em que as licenças se tornam válidas. </p> <p>Você pode especificar a data no campo <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> ou <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span> formato. Por exemplo, <span class="codeph"> 2008-12-1 </span> ou <span class="codeph"> 12-1-2008:00:00 </span> para meia-noite de 1º de dezembro de 2008. </p> <p> 
     <ul id="ul_D52B337F547F4E7AB87FE025236CA930"> 
      <li id="li_DBAE380972434DB1A4EF20D399038AB8">O valor deve ser menor que o valor de <span class="codeph"> -e </span>, se presente. </li> 
      <li id="li_2899EC5559CF44319A4AC4ECD90A5B9A">Não é possível aplicar esta opção juntamente com <span class="codeph"> -r </span>. </li> 
      <li id="li_19861B1A64E44B95B649948EAB3E4085">Para remover ou excluir a data de início ao atualizar uma política DRM, use <span class="codeph"> -s </span> sem especificar uma data. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w [&lt;minutes&gt;[,enableHS|disableHS] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Janela de reprodução, que é o número de minutos em que o conteúdo pode ser visualizado desde a primeira reprodução. </p> <p>Se não especificado ou se <span class="codeph"> -w </span> é usada sem especificar um número de minutos. Não há limitação na janela de reprodução. O valor deve ser não negativo. </p> <p>O modelo opcional <span class="codeph"> enableHS </span> ou <span class="codeph"> disableHS </span> o sinalizador indica se é necessário ativar ou desativar o hard stop. O sinalizador indica se o contexto de descriptografia é destruído no final da janela de reprodução (ativado) ou não destruído (desativado). </p> <p>Por exemplo, para especificar que o conteúdo só pode ser exibido por 60 minutos e requer uma parada permanente: 
     <codeblock>
       -w&amp;nbsp;60,enableHS 
     </codeblock> </p> <p>Nota:  <i>Parada forte</i> No momento, o não é compatível com o Flash Player, Android e iOS. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l minutos </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A duração do cache de licenças é o tempo em minutos em que uma licença pode ser armazenada em cache no License Store do cliente depois que a licença for emitida pelo servidor. O valor deve ser não negativo. </p> <p>Você pode especificar <span class="codeph"> -l 0 </span> para indicar que o armazenamento em cache de licenças não é permitido. Para armazenamento em cache de licença ilimitada, especifique <span class="codeph"> -l </span> sem minutos. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate data </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data de término do armazenamento em cache da licença. </p> <p class="- topic/p ">Indica a data final em que o cliente poderá armazenar licenças em cache no License Store do cliente depois que o servidor DRM do Primetime tiver emitido a licença. </p> <p>Você pode especificar a data nos seguintes formatos: 
     <ul id="ul_112DE7248A9C48B19520A3AA9E5D1F03"> 
      <li id="li_01C5400E78B84A3B8955972FBA875AAC"> <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> </li> 
      <li id="li_AA13B1EFA07A4542A3DB41FA3320B143"> <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span> </li> 
     </ul>Por exemplo, <span class="codeph"> 2008-12-1 </span> ou <span class="codeph"> 12-1-2008:00:00 </span> para meia-noite de 1º de dezembro de 2008. É necessário aplicar <span class="codeph"> -l </span> sem especificar minutos para o armazenamento em cache de licença ilimitada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O namespace de autenticação. </p> <p class="- topic/p ">Se você aplicar esta opção, o cliente precisará digitar um nome de usuário e uma senha emitida pela autoridade especificada. </p> <p>Não é possível aplicar esta opção juntamente com <span class="codeph"> -x </span>. </p> <p>Essa opção não é permitida para atualizações. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Permitir acesso anônimo. </p> <p class="- topic/p ">Não é possível aplicar esta opção juntamente com <span class="codeph"> -authNS </span>. </p> <p class="- topic/p ">Essa opção não é permitida para atualizações. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> min. </span>]:[ <span class="+ topic/ph pr-d/codeph codeph"> max </span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uma lista de permissões de aplicativos AIR que podem reproduzir conteúdo protegido. </p> <p class="- topic/p ">Aplique essa opção para restringir quais editores, aplicativos e versões podem acessar o conteúdo protegido por essa política DRM. </p> <p class="- topic/p ">Se você não especificar <i class="+ topic/ph hi-d/i ">appId</i>, todos os aplicativos do editor <i class="+ topic/ph hi-d/i ">pubId</i> são permitidos. </p> <p>Nota:  <i class="+ topic/ph hi-d/i ">min.</i> e <i class="+ topic/ph hi-d/i ">max</i> os números de versão são opcionais. </p> <p class="- topic/p ">É possível especificar vários <span class="codeph"> -ar </span> opções para permitir vários aplicativos. Se você não especificar um aplicativo AIR ou SWF, todos os aplicativos poderão acessar esse conteúdo. Durante uma atualização, para remover ou deletar todas as entradas da lista, aplique <span class="codeph"> -ar </span> sem os argumentos restantes. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist nome </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> value </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pares </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os clientes DRM que estão impedidos de obter acesso ao conteúdo protegido. </p> <p class="- topic/p ">O valor oferece suporte a pares nome:valor separados por vírgulas no seguinte formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> so | release= stringValue </span> </p> <p class="- topic/p ">Por exemplo, <span class="codeph"> os=Win,release=2.0.1 </span>. Durante uma atualização, para remover todas as entradas da lista, <span class="codeph"> -drmBlacklist </span> sem os argumentos restantes. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que os clientes DRM devem ter um nível mínimo de segurança atribuído para obter acesso ao conteúdo protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | OBRIGATÓRIO | SEM_REPRODUÇÃO | OBRIGATÓRIO_ACP | REQUIRED_CGMSA | USE_IF_AVAILABLE_ACP | USE_IF_AVAILABLE_CGMSA </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restrições de proteção de saída analógica </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | OBRIGATÓRIO | SEM_REPRODUÇÃO </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restrições da proteção de saída digital </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist nome </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> value </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pares </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os tempos de execução do aplicativo que estão restritos de acessar conteúdo protegido. </p> <p class="- topic/p ">O valor suporta pares nome:valor separados por vírgulas no seguinte formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> so | aplicativo | release= stringValue </span> </p> <p class="- topic/p ">Por exemplo, <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. Durante uma atualização, para remover todas as entradas da lista, <span class="codeph"> -runtimeBlacklist </span> sem os argumentos restantes. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que os tempos de execução do aplicativo devem ter um nível mínimo de segurança especificado para acessar o conteúdo protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf arquivo= swf_arquivo </span>, <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uma lista de permissões de aplicativos SWF que têm permissão para reproduzir conteúdo protegido. </p> <p class="- topic/p ">É possível especificar vários <span class="codeph"> -swf </span> opções para permitir vários aplicativos. Se você não especificar aplicativos AIR ou SWF, todos os aplicativos poderão acessar esse conteúdo. </p> <p>Durante uma atualização, para remover todas as entradas da lista, <span class="codeph"> -swf </span> sem os argumentos restantes. Se quiser identificar um SWF pelo seu valor de hash, você precisará especificar o arquivo de SWF para o qual calcular o hash e o tempo máximo para permitir que a verificação de SWF seja concluída (em segundos). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= valor </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica valores/chaves personalizados que você deseja adicionar a uma política DRM. </p> <p class="- topic/p ">É possível especificar vários <span class="codeph"> -k </span> opções. Durante a atualização, é possível aplicar <span class="codeph"> -k </span> sem os argumentos restantes se desejar remover todas as propriedades. A interpretação ou manipulação dos dados é gerenciada pelo servidor de licenças do Primetime DRM. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Adiciona uma propriedade personalizada que aparece na licença gerada para cada cliente. </p> <p class="- topic/p ">É possível especificar vários <span class="codeph"> -p </span> opções para adicionar várias propriedades. Durante uma atualização, é necessário aplicar <span class="codeph"> -p </span> sem os argumentos restantes se desejar remover todas as propriedades. A interpretação ou manipulação desses dados é gerenciada pela implementação do aplicativo cliente. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> <span class="codeph"> -opOTA whitelist=&lt;connection types=""&gt; </span> </span> </td> 
   <td colname="2" class="- topic/entry "> Limitações da proteção de saída Over the Air (OTA). A variável <span class="codeph"> lista de permissões </span> campo especifica quais tipos de conexão devem ser listas de permissões e o formato de &lt;connection types=""&gt; é <span class="codeph"> [type(,type)*] </span>, em que o tipo pode ser qualquer um dos seguintes: MIRACAST, AIRPLAY, WIDI, DLNA </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opResolution &lt;filename&gt; </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Restrições de proteção de saída baseadas em resolução conforme definido no arquivo especificado. </p> <p>A codificação deste arquivo é JSON. A gramática da formatação pode ser encontrada em <i>Sobre a Proteção de Saída Baseada em Resolução</i>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Exemplos**

Para criar uma política que permita acesso anônimo ao seu conteúdo, usando seu próprio arquivo de propriedades de configuração:

```
java -jar libs\AdobePolicyManager.jar new policy_test.pol -x -c my_configuration.properties
```
