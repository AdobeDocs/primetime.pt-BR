---
title: Propriedades do arquivo de configuração
description: Propriedades do arquivo de configuração
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---


# Propriedades do arquivo de configuração {#configuration-file-properties}

O arquivo de configuração especifica as seguintes propriedades. Para nomes de propriedades que incluem `n`, `n` representa um número inteiro que começa com 1 e aumenta para cada instância da propriedade.

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Opção de Linha de Propriedade/Comando </th> 
   <th colname="2" class="- topic/entry entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">npolicy name</i> </p> </td> 
   <td colname="2" class="- topic/entry "> O nome da política legível. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">keyServerboolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Se true, um Servidor de chave HTTPS será necessário para entrega de chave no iOS. O padrão é false, se não especificado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforceJailbreak</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">enforceJailbreakboolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Se verdadeiro, para dispositivos que oferecem suporte à detecção de quebra de maré, não permita a reprodução se a quebra de maré tiver sido detectada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> política.crítica</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">crialbooleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Defina a crítica da política. Se verdadeiro, o servidor deverá entender todas as partes da política (esse é o comportamento padrão). Se falso, o servidor pode ignorar atributos de política que não entende. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">Certificado do servidor de licença cuja chave pública é usada para criptografar a chave de criptografia raiz para o <a href="../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md" format="dita" scope="local"> Encadeamento de licença aprimorado </a>
   Essa propriedade especifica um arquivo que contém somente o certificado (o formato PEM ou DER é aceitável). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">rootKeyroot-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Especifique a chave de criptografia raiz para o Encadeamento de licença aprimorado. Se nenhuma chave for especificada e o Encadeamento de Licenças Avançado estiver ativado, uma chave aleatória será gerada. A chave deve ter 16 bytes de comprimento e ser especificada como valores hexadecimais. O espaço em branco entre os valores hexadecimais é opcional. Para atualizações, a opção de linha de comando não é permitida e a propriedade é ignorada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> - </span> <i class="+ topic/ph hi-d/i ">domainURLurl</i> </p> </td> 
   <td colname="2" class="- topic/entry "> URL do servidor de domínio, se o registro de domínio for necessário. Para atualizações, a opção de linha de comando não é permitida e a propriedade é ignorada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry "> Especifica se o registro de domínio anônimo é permitido. Defina a propriedade como true ou inclua essa opção de linha de comando para permitir acesso anônimo. Essa opção não pode ser usada com -domainAuthNS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> - </span> <i class="+ topic/ph hi-d/i ">domainAuthNSnamespace</i> </p> </td> 
   <td colname="2" class="- topic/entry "> O namespace de autenticação para registro de domínio. Se especificado, o cliente deve autenticar com um nome de usuário e senha emitidos pela autoridade especificada. Para atualizações, a opção de linha de comando não é permitida e a propriedade é ignorada. Essa opção não pode ser usada com -domainAnon. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.análogo</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">opAnalogAnalogOption</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Restrições de proteção de saída analógica. Os seguintes valores são suportados: 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_5BC8F39B61894E83A7B27570FF848F09"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </p> </li> 
     <li class="- topic/li " id="li_FF14594A0714480496793A82C3FA1610"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </p> </li> 
     <li class="- topic/li " id="li_721FCC4DC1F34AE398EFAE4C0D3F50F5"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_D588BB278BEE4CEAB034BD48550EBCDC"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_7E5F006D2F114502BA6D0A9C4173004E"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> OBRIGATÓRIO</span> </p> </li> 
     <li class="- topic/li " id="li_9EBFAA4AACF249C2A94432D88E12C3B9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NECESSÁRIO_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_6720C6A085864BEB957C0BF2C38551C9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> Required_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_6FD98473ECDB4A66AC4B506FB9B3B360"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">drmBlacklistname/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Os clientes DRM restringiram o acesso a conteúdo protegido. Essa opção especifica uma lista de versões de módulos DRM que podem não ser usadas (lista de bloqueios). O valor consiste em pares name=value separados por vírgula com o seguinte formato: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Os pares de nome/valor adicionais devem ser separados por vírgulas. Por exemplo: <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">runtimeBlacklist/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Tempo de execução do aplicativo restrito de acessar conteúdo protegido. Essa opção especifica uma lista de versões de módulos de tempo de execução que podem não ser usadas (lista de bloqueios). O valor consiste em pares name=value separados por vírgula com o seguinte formato: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Os pares de nome/valor adicionais devem ser separados por vírgulas. Por exemplo, <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">nome/pares de valores</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica os recursos do dispositivo necessários para acessar o conteúdo protegido. O valor consiste em pares name=value separados por vírgula com o seguinte formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">Por exemplo, <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>. Durante a atualização, use <span class="codeph"> -devCapabilitiesV1</span> sem os argumentos restantes para remover a restrição de recursos do dispositivo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">syncname/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifique a frequência com que os clientes são necessários para enviar mensagens de sincronização para o servidor. Se não estiver definido, os clientes não enviarão mensagens de sincronização ao reproduzir conteúdo protegido por esta política. O valor consiste em pares <span class="codeph"> name=value</span> separados por vírgula com o seguinte formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force|hardStop=numberValue</span> </p> <p class="- topic/p "> 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_25CAF96C27F34848A95B2E3693847C71"><span class="codeph"> start</span>  (obrigatório) - O intervalo de início especifica que o cliente deve começar a sincronizar com o servidor a tantos minutos desde a última sincronização. </li> 
      <li id="li_CC9068CFE75645029C947C9E1B53351F"><span class="codeph"> force</span>  (opcional) - Forçar probabilidade de sincronização é a probabilidade (0-100) com a qual o cliente deve forçar uma mensagem de sincronização durante a reprodução. </li> 
      <li id="li_C31A6250F19348FBB8B7569D00C6314E"><span class="codeph"> hardStop</span>  (opcional) - o intervalo de parada dura é o tempo em minutos após o qual o cliente falhará na reprodução se não conseguir sincronizar. Se definido, deve ser maior que o intervalo inicial. </li> 
     </ul>Durante a atualização, use <span class="codeph"> -sync</span> sem os argumentos restantes para remover os requisitos de sincronização. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">Indica se esta política tem uma licença raiz (consulte <i class="+ topic/ph hi-d/i ">Encadeamento de Licenças Avançado</i> em <i class="+ topic/ph hi-d/i ">Utilização de Acesso ao Adobe para Proteção de Conteúdo</i>). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">A data após a qual o conteúdo é válido. Use o formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> (por exemplo, <span class="codeph"> 2009-01-31</span> representa 31 de janeiro às 12:00 AM) ou <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:sec</span> (por exemplo, <span class="codeph"> 2009-01-31-14:30:00</span> representa 31 de janeiro às 2:30 PM). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data antes da qual o conteúdo é válido. Tanto <span class="codeph"> policy.expiration.endDate</span> quanto policy.expiration.duration podem não ser especificadas simultaneamente. Use o formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> ou <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:sec</span> (por exemplo, 2009-01-31-14:30:00 representa 31 de janeiro às 2:30 PM). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A quantidade de tempo em que o conteúdo é válido (em minutos), a partir de quando é empacotado. Tanto <span class="codeph"> policy.expiration.endDate</span> quanto <span class="codeph"> policy.expiration.duration</span> podem não ser especificadas ao mesmo tempo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Período de tempo em que uma licença pode ser armazenada em cache no cliente (em minutos). Defina essa propriedade como 0 para não permitir o armazenamento em cache de licenças. O valor deve ser 0 ou superior. Tanto <span class="codeph"> policy.licenseCaching.duration</span> quanto <span class="codeph"> policy.licenseCaching.endDate</span> podem não ser usadas simultaneamente. </p> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Observação</b>: Essa configuração de política é aplicada somente ao armazenamento em cache de licenças no disco. Ele não controla a duração da licença de memória em cache. A licença pode ser armazenada em cache na memória mesmo se a duração especificada pela política for zero. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data a partir da qual os certificados não podem ser armazenados em cache. Tanto <span class="codeph"> policy.licenseCaching.duration</span> quanto <span class="codeph"> policy.licenseCaching.endDate</span> podem não ser usadas simultaneamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica se a aquisição de licença anônima é permitida. O padrão é "false" (a autenticação de nome de usuário/senha é necessária) se não for especificado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se a autenticação de nome de usuário/senha for obrigatória, essa propriedade especificará um qualificador de nome opcional para nomes de usuário. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Pares de nome/valor personalizados que serão usados pelo servidor durante a aquisição da licença. Use o seguinte formato para especificar propriedades: <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica a janela de reprodução (em minutos), que é a duração para a qual a licença é válida após a primeira vez em que é usada para reproduzir conteúdo protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restrições de proteção de saída. Os valores devem ser um dos seguintes: </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">NO_PROTECTION, USE_IF_AVAILABLE, OBRIGATÓRIO, NO_PLAYBACK</i> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O módulo DRM deve ter o nível mínimo de segurança especificado, ou superior, para acessar conteúdo protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O módulo de tempo de execução do aplicativo deve ter o nível mínimo de segurança especificado, ou superior, para acessar conteúdo protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uma lista de permissões de aplicativos Adobe AIR ou iOS que podem reproduzir conteúdo protegido. A propriedade deve usar o seguinte formato: <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uma lista de permissões de aplicativos SWF permite reproduzir conteúdo protegido. Use o seguinte formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"></span> URLor file=<span class="+ topic/ph pr-d/codeph codeph">swf_file</span>, time=<i class="+ topic/ph hi-d/i ">max_time_to_</i> <i class="+ topic/ph hi-d/i ">verifyswf_</i> é o arquivo SWF para o qual calcular o hash e  <i class="+ topic/ph hi-d/i ">max_time_to_</i> verifyé o tempo máximo para permitir que o download e a verificação do SWF sejam concluídos (em segundos). </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Pares de nome/valor personalizados a serem incluídos em licenças emitidas para usuários. Use o seguinte formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> <p class="- topic/p ">Essa opção pode ser definida várias vezes para várias propriedades personalizadas. </p> </td> 
  </tr> 
 </tbody> 
</table>

