---
title: Uso da linha de comando do Gerenciador de políticas
description: Uso da linha de comando do Gerenciador de políticas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 0%

---


# Uso da linha de comando do Gerenciador de políticas {#policy-manager-command-line-usage}

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

**Quadro 1: Comandos**

| Comando | Descrição |
|---|---|
| `new` | Cria uma nova política de DRM |
| `detail` | Descreve uma política de DRM existente |
| `update` | Atualiza uma política de DRM existente |

**Quadro 2: Opções**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opção de linha de comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o nome e o local do arquivo de configuração. </p> <p class="- topic/p ">Se você não especificar um nome ou um local, o Gerenciador de Políticas de DRM pesquisa por <span class="filepath"> flashaccess stools.properties </span> no diretório de trabalho atual. </p> <p>Observação:  As opções especificadas na linha de comando têm prioridade sobre as opções especificadas no arquivo de configuração. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se o arquivo de destino existir, é possível substituir o arquivo sem ser solicitado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino existir e <span class="codeph"> -o </span> não estiver definido, ocorrerá um erro. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que a política de DRM tem uma licença raiz. </p> <p class="- topic/p ">Esta opção não está disponível para atualizações. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> data -e  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data de validade das licenças. </p> <p>Você pode especificar a data no formato <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> ou <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:sec </span>. Por exemplo, 2008-12-1 ou 2008-12-1-00:00:00 para meia-noite de 1º de dezembro de 2008. </p> <p> 
     <ul id="ul_D5DB5044756D4BD6A734813971598425"> 
      <li id="li_B6BD62A524384060A9DDA14FF50936FA">O valor deve ser maior que o valor de <span class="codeph"> -s </span>, se presente. </li> 
      <li id="li_C3C5AD0231A240EC9AC57685B9206E8D">Não é possível aplicar essa opção com <span class="codeph"> -r </span>. </li> 
      <li id="li_3790E2F829A149979BF44E0914CFF431">Para remover a data de término ao atualizar uma política de DRM, aplique <span class="codeph"> -e </span> sem especificar uma data. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r minutos  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A duração, em minutos, da validade do conteúdo protegido. </p> <p class="- topic/p ">A política de DRM se torna válida quando o conteúdo é protegido com o empacotador. </p> <p> 
     <ul id="ul_4690A0E4677A4DF6A006B7FCBD46F1BE"> 
      <li id="li_D1F098D44B494EE7A8647C0B62D5ACFA">O valor deve ser não negativo. </li> 
      <li id="li_ADFDCB01EEE04B37AFA42886AAEF47EB">Não é possível aplicar essa opção junto com <span class="codeph"> -e </span>. </li> 
      <li id="li_E80563E68BEB43FC9E29A694594CAE01">Para remover ou excluir a duração ao atualizar uma política de DRM, aplique <span class="codeph"> -r </span> sem especificar nenhum minuto. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> data -s  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data de validade das licenças. </p> <p>Você pode especificar a data no formato <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> ou <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:sec </span>. Por exemplo, <span class="codeph"> 2008-12-1 </span> ou <span class="codeph"> 2008-12-1-00:00 </span> para meia-noite de 1º de dezembro de 2008. </p> <p> 
     <ul id="ul_D52B337F547F4E7AB87FE025236CA930"> 
      <li id="li_DBAE380972434DB1A4EF20D399038AB8">O valor deve ser menor que o valor de <span class="codeph"> -e </span>, se presente. </li> 
      <li id="li_2899EC5559CF44319A4AC4ECD90A5B9A">Não é possível aplicar essa opção junto com <span class="codeph"> -r </span>. </li> 
      <li id="li_19861B1A64E44B95B649948EAB3E4085">Para remover ou excluir a data de início ao atualizar uma política de DRM, use <span class="codeph"> -s </span> sem especificar uma data. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w [&lt;minutes&gt;[,enableHS|disableHS]]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Janela de reprodução, que é o número de minutos em que o conteúdo pode ser visualizado na primeira reprodução. </p> <p>Se não especificado, ou se <span class="codeph"> -w </span> for usado sem especificar um número de minutos, não há limitação da janela de reprodução. O valor deve ser não negativo. </p> <p>O sinalizador opcional <span class="codeph"> enableHS </span> ou <span class="codeph"> disableHS </span> sinaliza se deve ativar ou desativar a parada rígida. O sinalizador indica se o contexto de descriptografia foi destruído no final da janela de reprodução (ativado) ou não destruído (desativado). </p> <p>Por exemplo, para especificar que o conteúdo só pode ser visualizado por 60 minutos e requer uma interrupção: 
     <codeblock>
       -w&amp;nbsp;60,enableHS 
     </codeblock> </p> <p>Observação:  <i>No momento, a interrupção permanente</i> não é suportada no Flash Player, Android e iOS. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l minutos  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A duração do armazenamento em cache de licenças é o tempo em minutos que uma licença pode ser armazenada em cache no License Store do cliente depois que a licença for emitida pelo servidor. O valor deve ser não negativo. </p> <p>Você pode especificar <span class="codeph"> -l 0 </span> para indicar que o armazenamento em cache de licenças não é permitido. Para armazenamento em cache de licença ilimitado, especifique <span class="codeph"> -l </span> sem nenhum minuto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> data -limite  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data de término do armazenamento em cache de licenças. </p> <p class="- topic/p ">Isso indica a data final em que o cliente pode armazenar licenças em cache no License Store do cliente depois que o servidor DRM Primetime emitir a licença. </p> <p>Você pode especificar a data nos seguintes formatos: 
     <ul id="ul_112DE7248A9C48B19520A3AA9E5D1F03"> 
      <li id="li_01C5400E78B84A3B8955972FBA875AAC"> <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd  </span> </li> 
      <li id="li_AA13B1EFA07A4542A3DB41FA3320B143"> <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:seg  </span> </li> 
     </ul>Por exemplo, <span class="codeph"> 2008-12-1 </span> ou <span class="codeph"> 2008-12-1-00:00 </span> para meia-noite de 1º de dezembro de 2008. Você precisa aplicar <span class="codeph"> -l </span> sem especificar minutos para o armazenamento em cache de licenças ilimitado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O namespace de autenticação. </p> <p class="- topic/p ">Se você aplicar essa opção, o cliente precisará digitar um nome de usuário e uma senha emitidos pela autoridade especificada. </p> <p>Não é possível aplicar essa opção junto com <span class="codeph"> -x </span>. </p> <p>Esta opção não é permitida para atualizações. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Permitir acesso anônimo. </p> <p class="- topic/p ">Não é possível aplicar essa opção junto com <span class="codeph"> -authNS </span>. </p> <p class="- topic/p ">Esta opção não é permitida para atualizações. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId  </span>[:  <span class="+ topic/ph pr-d/codeph codeph"> appId  </span>[:[  <span class="+ topic/ph pr-d/codeph codeph"> mín  </span>]:[  <span class="+ topic/ph pr-d/codeph codeph"> máx  </span>]]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uma lista de permissões de aplicativos AIR que podem reproduzir conteúdo protegido. </p> <p class="- topic/p ">Você pode aplicar essa opção para restringir quais editores, aplicativos e versões podem acessar o conteúdo protegido por esta política de DRM. </p> <p class="- topic/p ">Se você não especificar <i class="+ topic/ph hi-d/i ">appId</i>, todos os aplicativos para publisher <i class="+ topic/ph hi-d/i ">pubId</i> serão permitidos. </p> <p>Observação:  Os números de versão <i class="+ topic/ph hi-d/i ">min</i> e <i class="+ topic/ph hi-d/i ">max</i> são opcionais. </p> <p class="- topic/p ">Você pode especificar várias opções <span class="codeph"> -air </span> para permitir vários aplicativos. Se você não especificar um aplicativo AIR ou SWF, todos os aplicativos podem acessar esse conteúdo. Durante uma atualização, para remover ou excluir todas as entradas da lista, aplique <span class="codeph"> -air </span> sem os argumentos restantes. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist name  </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> value  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pairs  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os clientes DRM que são restritos de obter acesso a conteúdo protegido. </p> <p class="- topic/p ">O valor suporta pares name:value separados por vírgulas no seguinte formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue  </span> </p> <p class="- topic/p ">Por exemplo, <span class="codeph"> os=Win,release=2.0.1 </span>. Durante uma atualização, para remover todas as entradas da lista, aplique <span class="codeph"> -drmBlacklist </span> sem os argumentos restantes. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que os clientes DRM devem ter um nível mínimo de segurança atribuído para obter acesso ao conteúdo protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | OBRIGATÓRIO | NO_PLAYBACK | OBRIGATÓRIO_ACP | NECESSÁRIO_CGMSA | USE_IF_AVAILABLE_ACP | USE_IF_AVAILABLE_CGMSA  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restrições de proteção de saída analógica </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | OBRIGATÓRIO | NO_PLAYBACK  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restrições de proteção de saída digital </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist name  </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> value  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pairs  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os tempos de execução do aplicativo que são restritos ao acesso a conteúdo protegido. </p> <p class="- topic/p ">O valor suporta pares name:value separados por vírgulas no seguinte formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | aplicação | release= stringValue  </span> </p> <p class="- topic/p ">Por exemplo, <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. Durante uma atualização, para remover todas as entradas da lista, aplique <span class="codeph"> -runtimeBlacklist </span> sem os argumentos restantes. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que os tempos de execução do aplicativo devem ter um nível mínimo de segurança especificado para acessar conteúdo protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> url do swf  </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf file= swf_file,  </span>  <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uma lista de permissões de aplicativos SWF que podem reproduzir conteúdo protegido. </p> <p class="- topic/p ">Você pode especificar várias opções <span class="codeph"> -swf </span> para permitir vários aplicativos. Se você não especificar nenhum aplicativo AIR ou SWF, todos os aplicativos podem acessar esse conteúdo. </p> <p>Durante uma atualização, para remover todas as entradas da lista, aplique <span class="codeph"> -swf </span> sem os argumentos restantes. Se quiser identificar um SWF pelo seu valor de hash, você precisa especificar o arquivo SWF para o qual calcular o hash e o tempo máximo para permitir que a verificação do SWF seja concluída (em segundos). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= value  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica a chave/valores personalizados que você deseja adicionar a uma política de DRM. </p> <p class="- topic/p ">Você pode especificar várias opções <span class="codeph"> -k </span>. Durante a atualização, você pode aplicar <span class="codeph"> -k </span> sem os argumentos restantes se desejar remover todas as propriedades. A interpretação ou o manuseio dos dados são gerenciados pelo servidor de licenças Primetime DRM. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Adiciona uma propriedade personalizada que aparece na licença gerada para cada cliente. </p> <p class="- topic/p ">Você pode especificar várias opções <span class="codeph"> -p </span> para adicionar várias propriedades. Durante uma atualização, é necessário aplicar <span class="codeph"> -p </span> sem os argumentos restantes se desejar remover todas as propriedades. A interpretação ou o tratamento desses dados são gerenciados pela implementação do aplicativo cliente. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> <span class="codeph"> -opOTA whitelist=&lt;connection types=""&gt; </span> </span> </td> 
   <td colname="2" class="- topic/entry "> Sobre as restrições de proteção de saída de ar (OTA). O campo <span class="codeph"> lista de permissões </span> especifica quais tipos de conexão para a lista de permissões e o formato de &lt;tipos de conexão&gt; é <span class="codeph"> [type(,type)*] </span>, onde o tipo pode ser qualquer um dos seguintes: MIRACAST, AIRPLAY, WIDI, DLNA </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opResolution  &lt;filename&gt; </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Restrições de proteção de saída baseadas em resolução, conforme definido no arquivo especificado. </p> <p>A codificação desse arquivo é JSON. A gramática da formatação pode ser encontrada em <i>Sobre a Proteção de Saída Baseada em Resolução</i>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Exemplos**

Para criar uma política que permita acesso anônimo ao seu conteúdo, usando seu próprio arquivo de propriedades de configuração:

```
java -jar libs\AdobePolicyManager.jar new policy_test.pol -x -c my_configuration.properties
```
