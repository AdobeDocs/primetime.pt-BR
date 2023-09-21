---
title: Uso da linha de comando
description: Uso da linha de comando
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# Uso da linha de comando {#command-line-usage}

Antes de usar o Policy Manager, certifique-se de atender aos requisitos listados em Requisitos.

O Policy Manager está na [!DNL \Reference Implementation\Command Line Tools] no DVD. Para executar a ferramenta, use a seguinte sintaxe:

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

A tabela a seguir contém descrições das ações de linha de comando mostradas na sintaxe acima:

| Ação da linha de comando | Descrição |
|---|---|
| `new` | Cria uma nova política. |
| `detail` | Descreve uma política existente. |
| `update` | Atualiza uma política existente. |

A tabela a seguir descreve as opções de linha de comando que podem ser especificadas com a sintaxe acima:

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o local do arquivo de configuração. Se essa opção não for usada, o Policy Manager procurará <span class="filepath"> flashaccesstools.properties </span> no diretório de trabalho. As opções especificadas na linha de comando têm precedência sobre as presentes no arquivo de configuração. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se o arquivo de destino já existir, substitua-o sem avisar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e <span class="codeph"> -o </span> não estiver definido, um erro será retornado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que a política tem uma licença raiz. Não permitido para atualizações. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e data </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data antes da qual as licenças serão válidas. Especificar como <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> ou <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span>. Por exemplo, 2008-12-1 ou 2008-12-1-00:00:00 para meia-noite de 1º de dezembro de 2008. O valor deve ser maior que o valor de <span class="codeph"> -s </span>, se presente. Essa opção não pode ser usada com <span class="codeph"> -r </span>. Para remover a data final ao atualizar uma política, use <span class="codeph"> -e </span> sem especificar uma data. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r minutos </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A duração (minutos) do conteúdo protegido com esta política é válida, a partir do momento em que o conteúdo é protegido com o empacotador. O valor deve ser não negativo. Essa opção não pode ser usada com <span class="codeph"> -e </span>. Para remover a duração ao atualizar uma política, use <span class="codeph"> -r </span> sem especificar alguns minutos. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s data </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data após a qual as licenças serão válidas. Especificar como <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> ou <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span>. Por exemplo, 2008-12-1 ou 2008-12-1-00:00:00 para meia-noite de 1º de dezembro de 2008. O valor deve ser menor que o valor de <span class="codeph"> -e </span>, se presente. Essa opção não pode ser usada com <span class="codeph"> -r </span>. Para remover a data de início ao atualizar uma política, use <span class="codeph"> -s </span> sem especificar uma data. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w minutos </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A janela de reprodução (o número de minutos em que o conteúdo pode ser exibido, começando da primeira reprodução). Se esta opção não for especificada ou se <span class="codeph"> -w </span> for usada sem especificar o número de minutos, não há limitação na janela de reprodução. O valor deve ser não negativo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l minutos </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A duração do armazenamento em cache da licença em minutos, que é o tempo em que uma licença poderá ser armazenada em cache no License Store do cliente depois que a licença for emitida pelo servidor. O valor deve ser não negativo. Especificar <span class="codeph"> -l 0 </span> para indicar que o armazenamento em cache de licenças não é permitido. Uso <span class="codeph"> -l </span> sem especificar um número de minutos para o armazenamento em cache de licença ilimitada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate data </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data final do armazenamento em cache da licença (a data após a qual as licenças não poderão ser armazenadas em cache no License Store do cliente, após a emissão da licença pelo servidor). Especificar como <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span><i class="+ topic/ph hi-d/i "> </i>ou<i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span>. Por exemplo, 2008-12-1 ou 2008-12-1-00:00:00 para meia-noite de 1º de dezembro de 2008. Uso <span class="codeph"> -l </span> sem especificar um número de minutos para o armazenamento em cache de licença ilimitada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O namespace de autenticação. Se especificado, o cliente deve autenticar com um nome de usuário e senha emitidos pela autoridade especificada. Essa opção não pode ser usada com <span class="codeph"> -x </span>. Atualizações não são permitidas. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Permitir acesso anônimo. Essa opção não pode ser usada com <span class="codeph"> -authNS </span>. Atualizações não são permitidas. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> min. </span>]:[ <span class="+ topic/ph pr-d/codeph codeph"> max </span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uma lista de permissões de aplicativos do AIR com permissão para reproduzir conteúdo protegido. Use isso para restringir quais editores, aplicativos e versões podem acessar conteúdo protegido com essa política. </p> <p class="- topic/p ">Se <i class="+ topic/ph hi-d/i ">appId</i> não for especificado, todos os aplicativos do editor <i class="+ topic/ph hi-d/i ">pubId</i> são permitidos. </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">min.</i> e <i class="+ topic/ph hi-d/i ">max</i> os números de versão são opcionais. </p> <p class="- topic/p ">Múltiplo <span class="codeph"> -ar </span> opções podem ser especificadas para permitir vários aplicativos. Se nenhum aplicativo AIR ou SWF for especificado, todos os aplicativos poderão acessar esse conteúdo. Durante uma atualização, use -air sem os argumentos restantes para remover todas as entradas da lista. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist nome </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> value </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pares </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os clientes DRM são impedidos de acessar o conteúdo protegido. O valor consiste em pares de nome:valor separados por vírgulas com o seguinte formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> so | release= stringValue </span> </p> <p class="- topic/p ">Por exemplo, <span class="codeph"> os=Win,release=2.0.1 </span>. Durante uma atualização, use <span class="codeph"> -drmBlacklist </span> sem os argumentos restantes para remover todas as entradas da lista. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que os clientes DRM devem ter o nível mínimo de segurança especificado para acessar o conteúdo protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | OBRIGATÓRIO | SEM_REPRODUÇÃO | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restrições de proteção de saída analógica. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | OBRIGATÓRIO | SEM_REPRODUÇÃO </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restrições da proteção de saída digital. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist nome </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> value </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pares </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os tempos de execução do aplicativo são impedidos de acessar conteúdo protegido. O valor consiste em pares de nome:valor separados por vírgulas com o seguinte formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> so | aplicativo | release= stringValue </span> </p> <p class="- topic/p ">Por exemplo, <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. Durante uma atualização, use <span class="codeph"> -runtimeBlacklist </span> sem os argumentos restantes para remover todas as entradas da lista. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica que os tempos de execução do aplicativo devem ter o nível mínimo de segurança especificado para acessar o conteúdo protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf arquivo= swf_arquivo </span>, <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uma lista de permissões de aplicativos SWF com permissão para reproduzir conteúdo protegido. Várias opções -swf podem ser especificadas para permitir vários aplicativos. Se nenhum aplicativo AIR ou SWF for especificado, todos os aplicativos poderão acessar esse conteúdo. Durante uma atualização, use -swf sem os argumentos restantes para remover todas as entradas da lista. Para identificar um SWF pelo seu valor de hash, especifique o arquivo de SWF para o qual calcular o hash e o tempo máximo para permitir que a verificação de SWF seja concluída (em segundos). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= valor </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica chave/valores personalizados para adicionar à política. Múltiplo <span class="codeph"> -k </span> opções podem ser especificadas. Durante a atualização, use <span class="codeph"> -k </span> sem os argumentos restantes para remover todas as propriedades. A interpretação ou o tratamento desses dados depende totalmente da implementação do servidor de licenças de acesso ao Adobe. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Adiciona uma propriedade personalizada, que aparecerá na licença gerada para cada cliente. Múltiplo <span class="codeph"> -p </span> opções podem ser especificadas para adicionar várias propriedades. Durante uma atualização, use <span class="codeph"> -p </span> sem os argumentos restantes para remover todas as propriedades. A interpretação ou manuseio desses dados depende totalmente da implementação do aplicativo cliente. </p> </td> 
  </tr> 
 </tbody> 
</table>
