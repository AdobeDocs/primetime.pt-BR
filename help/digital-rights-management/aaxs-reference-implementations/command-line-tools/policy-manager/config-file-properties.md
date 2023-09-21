---
title: Propriedades do arquivo de configuração
description: Propriedades do arquivo de configuração
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# Propriedades do arquivo de configuração {#configuration-file-properties}

O arquivo de configuração especifica as seguintes propriedades. Para nomes de propriedades que incluem `n`, `n` representa um número inteiro que começa com 1 e aumenta para cada instância da propriedade.

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Propriedade/Opção de linha de comando </th> 
   <th colname="2" class="- topic/entry entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -n</span> <i class="+ topic/ph hi-d/i ">policyname</i> </p> </td> 
   <td colname="2" class="- topic/entry "> O nome da política legível. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Se verdadeiro, um Servidor de chaves HTTPS será necessário para a entrega de chaves à iOS. O padrão é falso, se não for especificado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.forceJailbreak</span> <p class="- topic/p "><span class="codeph"> -forceJailbreak</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Se verdadeiro, para dispositivos que oferecem suporte à detecção de jailbreak, não permita a reprodução se jailbreak tiver sido detectado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> política.crítica</span> <p class="- topic/p "><span class="codeph"> -crítico</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Defina a criticalidade da política. Se verdadeiro, o servidor deve entender todas as partes da política (esse é o comportamento padrão). Se for falso, o servidor pode ignorar atributos de política que não entende. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">Certificado de servidor de licenças cuja chave pública é usada para criptografar a chave de criptografia raiz para o <a href="../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md" format="dita" scope="local"> Encadeamento de licenças aprimorado </a>
   Essa propriedade especifica um arquivo que contém somente o certificado (o formato PEM ou DER é aceitável). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">root-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Especifique a chave de criptografia raiz para o Encadeamento de Licenças Aprimorado. Se nenhuma chave for especificada e o Encadeamento de licenças aprimorado estiver ativado, uma chave aleatória será gerada. A chave deve ter 16 bytes de comprimento e ser especificada como valores hexadecimais. O espaço em branco entre os valores hexadecimais é opcional. Para atualizações, a opção de linha de comando não é permitida e a propriedade é ignorada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainURL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry "> URL do servidor de domínio, se o registro de domínio for necessário. Para atualizações, a opção de linha de comando não é permitida e a propriedade é ignorada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry "> Especifica se o registro de domínio anônimo é permitido. Defina a propriedade como true ou inclua essa opção de linha de comando para permitir acesso anônimo. Essa opção não pode ser usada com -domainAuthNS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">namespace</i> </p> </td> 
   <td colname="2" class="- topic/entry "> O namespace de autenticação para o registro de domínio. Se especificado, o cliente deve autenticar com um nome de usuário e senha emitidos pela autoridade especificada. Para atualizações, a opção de linha de comando não é permitida e a propriedade é ignorada. Essa opção não pode ser usada com -domainAnon. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.alog</span> <p class="- topic/p "><span class="codeph"> -opAnalog</span> <i class="+ topic/ph hi-d/i ">OpçãoAnalógica</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Restrições de proteção de saída analógica. Os seguintes valores são suportados: 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_5BC8F39B61894E83A7B27570FF848F09"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </p> </li> 
     <li class="- topic/li " id="li_FF14594A0714480496793A82C3FA1610"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </p> </li> 
     <li class="- topic/li " id="li_721FCC4DC1F34AE398EFAE4C0D3F50F5"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_D588BB278BEE4CEAB034BD48550EBCDC"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_7E5F006D2F114502BA6D0A9C4173004E"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> OBRIGATÓRIO</span> </p> </li> 
     <li class="- topic/li " id="li_9EBFAA4AACF249C2A94432D88E12C3B9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_6720C6A085864BEB957C0BF2C38551C9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_6FD98473ECDB4A66AC4B506FB9B3B360"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drmBlacklist</span> <i class="+ topic/ph hi-d/i ">pares nome/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Clientes DRM com acesso restrito a conteúdo protegido. Essa opção especifica uma lista de versões dos módulos DRM que não podem ser usadas (lista de bloqueios). O valor consiste em pares name=value separados por vírgula com o seguinte formato: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Os pares nome/valor adicionais devem ser separados por vírgulas. Por exemplo: <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklist</span> <i class="+ topic/ph hi-d/i ">pares nome/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Os tempos de execução do aplicativo são impedidos de acessar conteúdo protegido. Essa opção especifica uma lista de versões dos módulos de tempo de execução que não podem ser usadas (lista de bloqueios). O valor consiste em pares name=value separados por vírgula com o seguinte formato: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Os pares nome/valor adicionais devem ser separados por vírgulas. Por exemplo, <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">pares nome/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica os recursos do dispositivo necessários para acessar conteúdo protegido. O valor consiste em pares name=value separados por vírgula com o seguinte formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">Por exemplo, <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>. Durante a atualização, use <span class="codeph"> -devCapabilitiesV1</span> sem os argumentos restantes para remover a restrição de recursos do dispositivo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">pares nome/valor</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifique a frequência com que os clientes devem enviar mensagens de sincronização ao servidor. Se não estiver definido, os clientes não enviarão mensagens de sincronização ao reproduzir conteúdo protegido com esta política. O valor consiste em vírgulas <span class="codeph"> name=value</span> pares com o seguinte formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force|hardStop=numberValue</span> </p> <p class="- topic/p "> 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_25CAF96C27F34848A95B2E3693847C71"><span class="codeph"> start</span> (obrigatório) - O intervalo de início especifica que o cliente deve iniciar a sincronização com o servidor tantos minutos desde a última sincronização. </li> 
      <li id="li_CC9068CFE75645029C947C9E1B53351F"><span class="codeph"> force</span> (opcional) - Forçar probabilidade de sincronização é a probabilidade (0-100) com a qual o cliente deve forçar uma mensagem de sincronização durante a reprodução. </li> 
      <li id="li_C31A6250F19348FBB8B7569D00C6314E"><span class="codeph"> hardStop</span> (opcional) - Intervalo de parada permanente é o tempo em minutos após o qual o cliente falhará a reprodução se não conseguir sincronizar. Se definido, deve ser maior que o intervalo inicial. </li> 
     </ul>Durante a atualização, use <span class="codeph"> -sync</span> sem os argumentos restantes para remover os requisitos de sincronização. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">Indica se esta política tem uma licença raiz (consulte <i class="+ topic/ph hi-d/i ">Encadeamento de licenças aprimorado</i> in <i class="+ topic/ph hi-d/i ">Utilização do acesso ao Adobe para proteção de conteúdo</i>). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">A data após a qual o conteúdo é válido. Usar o formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> (por exemplo, <span class="codeph"> 31/01/2009</span> representa 31 de janeiro às 12h) ou <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:s</span> (por exemplo, <span class="codeph"> 14/01/2009:30:00</span> representa 31 de janeiro às 14h30). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data antes da qual o conteúdo é válido. Ambos <span class="codeph"> policy.expiration.endDate</span> e policy.expiration.duration não podem ser especificados simultaneamente. Usar o formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> ou <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:s</span> (por exemplo, 31-01-2009):30:00 representa 31 de janeiro às 14h30). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O tempo de validade do conteúdo (em minutos), a partir do momento em que é empacotado. Ambos <span class="codeph"> policy.expiration.endDate</span> e <span class="codeph"> policy.expiration.duration</span> não pode ser especificado ao mesmo tempo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Tempo de armazenamento em cache de uma licença no cliente (em minutos). Defina essa propriedade como 0 para não permitir o armazenamento em cache de licenças. O valor deve ser 0 ou superior. Ambos <span class="codeph"> policy.licenseCaching.duration</span> e <span class="codeph"> policy.licenseCaching.endDate</span> não podem ser usados simultaneamente. </p> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Nota</b>: esta configuração de política é aplicada somente ao cache de licença no disco. Ele não controla a duração da licença de memória em cache. A licença pode ser armazenada em cache na memória mesmo se a duração especificada da política for zero. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data após a qual as licenças não poderão ser armazenadas em cache. Ambos <span class="codeph"> policy.licenseCaching.duration</span> e <span class="codeph"> policy.licenseCaching.endDate</span> não podem ser usados simultaneamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica se a aquisição de licença anônima é permitida. O padrão é "false" (é necessária a autenticação do usuário/senha) se não for especificado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se a autenticação de nome de usuário/senha for necessária, essa propriedade especificará um qualificador de nome opcional para nomes de usuário. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Pares de nome/valor personalizados a serem usados pelo servidor durante a aquisição da licença. Use o seguinte formato para especificar propriedades: <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica a janela de reprodução (em minutos), que é a duração pela qual a licença é válida após a primeira vez que é usada para reproduzir conteúdo protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restrições de proteção de saída. Os valores devem ser um dos seguintes: </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">NO_PROTECTION, USE_IF_AVAILABLE, REQUIRED, NO_PLAYBACK</i> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O módulo DRM deve ter o nível mínimo de segurança especificado, ou superior, para acessar o conteúdo protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O módulo de tempo de execução do aplicativo deve ter o nível mínimo de segurança especificado, ou superior, para acessar o conteúdo protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uma lista de permissões de aplicativos Adobe AIR ou iOS com permissão para reproduzir conteúdo protegido. A propriedade deve usar o seguinte formato: <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min.</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uma lista de permissões de aplicativos SWF com permissão para reproduzir conteúdo protegido. Usar o seguinte formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">URL</span> ou arquivo=<span class="+ topic/ph pr-d/codeph codeph">arquivo_swf</span>,hora=<i class="+ topic/ph hi-d/i ">max_time_to_verify</i> <i class="+ topic/ph hi-d/i ">arquivo_swf</i> é o arquivo SWF para o qual calcular o hash e <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> é o tempo máximo para permitir o download e a verificação do SWF para conclusão (em segundos). </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Pares de nome/valor personalizados a serem incluídos nas licenças emitidas para usuários. Usar o seguinte formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> <p class="- topic/p ">Essa opção pode ser definida várias vezes para várias propriedades personalizadas. </p> </td> 
  </tr> 
 </tbody> 
</table>
