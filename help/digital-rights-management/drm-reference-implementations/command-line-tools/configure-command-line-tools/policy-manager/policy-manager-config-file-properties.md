---
description: nulo
keywords: hard stop
seo-description: nulo
seo-title: Propriedades de configuração
title: Propriedades de configuração
uuid: 216921d1-a9c1-4650-9dce-c025836986e5
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---


# Propriedades de configuração {#configuration-properties}

<!--<a id="section_20A96CDCC5C340DEAF455C6E300E5712"></a>-->

>[!NOTE]
>
>Para nomes de propriedades que incluem `.n`, o `n` representa um número inteiro que start com 1 e aumenta para cada instância da propriedade. Por exemplo: `policy.license.customProp.n`.

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Opção de Linha de Propriedade/Comando </th> 
   <th colname="2" class="- topic/entry entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -n</span> <i class="+ topic/ph hi-d/i ">nome da política</i> </p> </td> 
   <td colname="2" class="- topic/entry "> O nome da política DRM legível por humanos. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requirementsKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry ">São aplicáveis as seguintes condições: 
    <ul id="ul_AF4EBD6C19DC4DFAAB4756EF24BAC57D"> 
     <li id="li_6CC48ABF78EC426E9FC51458BD946BC9">Se verdadeiro, um servidor de chaves HTTPS é necessário para o delivery de chaves do iOS. </li> 
     <li id="li_63046A4ED7354C1E9E823B475E4AEFF7">Se não for especificado, o padrão será false. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.applyJailbreak</span> <p class="- topic/p "><span class="codeph"> -applyJailbreak</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Para dispositivos que suportam detecção de quebra de falha, se verdadeiro, não permita a reprodução quando for detectada quebra de parada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> política.crítica</span> <p class="- topic/p "><span class="codeph"> -crítico</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Define a importância da política de DRM: 
    <ul id="ul_63F1994798894233A67AC4F8220AB642"> 
     <li id="li_D05DD9AD70464D6B9DB9DFF95846E589">Se verdadeiro, o servidor deverá entender todas as partes da política de DRM, que representa o comportamento padrão. </li> 
     <li id="li_0211473DAF1F426787CC4A68F47643C6">Se falso, o servidor pode ignorar os atributos da política DRM que não reconhece. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">Certificado do servidor de licença cuja chave pública é usada para criptografar a chave de criptografia raiz para o Encadeamento <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"></a>de licença aprimorado. Essa propriedade especifica um arquivo que inclui apenas o certificado. <p>Observação:  Os formatos PEM ou DER são suportados. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">root-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Especifica a chave de criptografia raiz para o Encadeamento <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"></a>de licença aprimorado. Se nenhuma chave for especificada e o Encadeamento aprimorado de licença estiver ativado, uma chave aleatória será gerada automaticamente. </p> <p>A chave deve ter 16 bytes e ser especificada como valores hexadecimais. O espaço em branco entre os valores hexadecimais é opcional. Para atualizações, a opção de linha de comando não está disponível e a propriedade é ignorada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainURL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Se o registro de domínio for obrigatório, o <i>url</i> especifica o URL de um servidor de domínio. Para atualizações, a opção de linha de comando não está disponível e a propriedade é ignorada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonimous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry ">Especifica se o registro de domínio anônimo é permitido. Define a propriedade como true ou inclui essa opção de linha de comando para permitir acesso anônimo. <p>Observação: Esta opção não pode ser usada com <span class="codeph"> -domainAuthNS</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">namespace</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>A namespace de autenticação para registro de domínio. Se especificado, o cliente precisa ser autenticado com um nome de usuário e senha emitidos pela autoridade especificada. </p> <p>Para atualizações, a opção de linha de comando não está disponível e a propriedade é ignorada. </p> <p>Observação: Esta opção não pode ser usada com <span class="codeph"> -domainAnon</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.alog</span> <p class="- topic/p "><span class="codeph"> -opAnalog</span> <i class="+ topic/ph hi-d/i ">AnalogOption</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Restrições de proteção de saída analógica e os seguintes valores são suportados: 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_F920EC01159C4231AFBE579D487C8770"><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </li> 
     <li class="- topic/li " id="li_2DE0494AF8C446EB9E4567915F5E97C3"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </li> 
     <li class="- topic/li " id="li_207D2D6256D6423FBDABA7A8627A9B7D"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </li> 
     <li class="- topic/li " id="li_E17D944BED5F403FAE94708EE6AE4BBE"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </li> 
     <li class="- topic/li " id="li_66D5A0C8FE154445A522D91EFB05B7ED"><span class="+ topic/ph pr-d/codeph codeph"> OBRIGATÓRIO</span> </li> 
     <li class="- topic/li " id="li_AF2024F212A249ED99AEECCF3E844A11"><span class="+ topic/ph pr-d/codeph codeph"> NECESSÁRIO_ACP</span> </li> 
     <li class="- topic/li " id="li_FFF9B7DAE77740EE895EC35D1606A527"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </li> 
     <li class="- topic/li " id="li_52DED572F3AE495EB6A6450C611B440E"><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drmBlacklist</span> <i class="+ topic/ph hi-d/i ">name/value-pares</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Clientes DRM que não têm acesso a conteúdo protegido. Esta opção especifica uma lista de versões de módulos DRM que podem não ser usadas (lista de bloqueios). </p> <p>O valor consiste em pares de <span class="codeph"> nome=valor</span> separados por vírgula no seguinte formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Os pares de nome/valor adicionais devem ser separados por vírgulas. Por exemplo, <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklist</span> <i class="+ topic/ph hi-d/i ">name/value-pair</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Os tempos de execução do aplicativo não têm acesso a conteúdo protegido. Essa opção especifica uma lista de versões de módulos de tempo de execução que podem não ser usadas (lista de bloqueios). </p> <p>O valor consiste em pares de <span class="codeph"> nome=valor</span> separados por vírgulas no seguinte formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Os pares de nome/valor adicionais devem ser separados por vírgulas. Por exemplo, <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">nome/pares de valores</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica os recursos do dispositivo necessários para acessar conteúdo protegido. O valor consiste em pares de <span class="codeph"> nome=valor</span> separados por vírgula no seguinte formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">Por exemplo, <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>. </p> <p>Durante uma atualização, é necessário aplicar <span class="codeph"> -devCapabilitiesV1</span> sem os argumentos restantes que removem a restrição de recursos do dispositivo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">name/value-pares</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica com que frequência os clientes são necessários para enviar mensagens de sincronização para o servidor. </p> <p>Se a propriedade não estiver definida, os clientes não enviarão mensagens de sincronização quando reproduzirem conteúdo protegido por uma política de DRM. O valor consiste em pares de <span class="codeph"> nome=valor</span> separados por vírgulas no seguinte formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force=numberValue</span> </p> <p class="- topic/p ">A lista a seguir fornece informações adicionais sobre as opções: 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_FD2C0C6DA19E455AA1917A56E09A7F84">(obrigatório) <span class="codeph"> O start</span> especifica que o cliente precisa sincronizar o start com o servidor nos minutos especificados desde a última sincronização. </li> 
      <li id="li_9DEBC57385A442C3929AE3D0E3FA8992">(opcional) <span class="codeph"> force</span> é a probabilidade (0-100) com a qual o cliente precisa forçar uma mensagem de sincronização durante a reprodução. </li> 
     </ul>Durante a atualização, use <span class="codeph"> -sync</span> sem os argumentos restantes para remover os requisitos de sincronização. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">Indica se esta política de DRM tem uma licença raiz. <p>Para obter mais informações, consulte Encadeamento <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"></a>de licença aprimorado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">A data após a qual o conteúdo se torna válido. Você pode aplicar um dos seguintes formatos: 
    <ul id="ul_6610B44D0C16485098F6F45DE3F151D7"> 
     <li id="li_986707D4C6164C44B3CCBE2EEB4C09B6"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> <p>Por exemplo, <span class="codeph"> 2009-01-31</span> significa 31 de janeiro às 12:00 da manhã. </p> </li> 
     <li id="li_E15B782716124F6EAEFB04D16E5280DB"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:seg</span> <p>Por exemplo, <span class="codeph"> 2009-01-31-14:30:00</span> significa 31 de janeiro às 14:30. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data antes que o conteúdo se torne inválido. </p> <p>Observação: Não é possível especificar <span class="codeph"> policy.expiration.endDate</span> e <span class="codeph"> policy.expiration.duration</span> simultaneamente. </p> <p>Por exemplo, 2009-01-31-14:30:00 significa que o conteúdo expirará em 31 de janeiro às 14:30. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A hora em minutos em que o conteúdo se torna inválido. A hora é start ao empacotar o conteúdo. </p> <p>Observação: Não é possível especificar <span class="codeph"> policy.expiration.endDate</span> e <span class="codeph"> policy.expiration.duration</span> simultaneamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A hora em minutos em que uma licença pode ser armazenada em cache no cliente. Você pode definir essa propriedade como 0 para impedir o armazenamento em cache de licenças. O valor deve ser 0 ou superior. </p> <p>Observação: Não é possível especificar <span class="codeph"> policy.licenseCaching.duration</span> e <span class="codeph"> policy.licenseCaching.endDate</span> simultaneamente. </p> <p class="- topic/p ">Esta configuração de política de DRM é aplicada somente ao cache de licenças no disco e não controla a duração da licença em cache de memória. A licença pode ser armazenada em cache na memória mesmo se você não especificar uma política de DRM com duração zero. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A data após a qual você não pode mais armazenar licenças em cache. </p> <p>Observação: Não é possível especificar <span class="codeph"> policy.licenseCaching.duration</span> e <span class="codeph"> policy.licenseCaching.endDate</span> simultaneamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anônimo</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica se a aquisição de licença anônima é permitida. O padrão é definido como <span class="codeph"> false</span>, o que significa que um nome de usuário e senha são necessários. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se um nome de usuário e senha forem obrigatórios, essa propriedade especificará um qualificador de nome opcional para nomes de usuário. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Pares de nome/valor personalizados a serem usados pelo servidor durante a aquisição da licença. Você pode aplicar o seguinte formato para especificar propriedades: <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica a janela de reprodução em minutos. Este valor representa quanto tempo a licença é válida após a primeira vez que o conteúdo protegido é reproduzido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Restrições de proteção de saída, que devem ser um dos seguintes valores: 
     <ul id="ul_wsb_kfp_fs"> 
      <li id="li_FE012306F22F4F3FB981FE167C7A8B94"><span class="codeph"> NO_PROTECTION</span> </li> 
      <li id="li_A5591DC8983848FE9823C2A261BF7713"><span class="codeph"> USE_IF_AVAILABLE</span> </li> 
      <li id="li_74102C36ADE841C4B9ED71156E0A4C2C"><span class="codeph"> OBRIGATÓRIO</span> </li> 
      <li id="li_769E15C85B4E4DD48213DBD019D60BA7"><span class="codeph"> NO_PLAYBACK</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.ota</span> </td> 
   <td colname="2" class="- topic/entry ">Especifica os tipos de conexão OTA (Over the air) que devem ser permitidos listados. Os tipos de conexão válidos incluem: 
    <ul id="ul_iz5_4fp_fs"> 
     <li id="li_FB07519EFEFE4B95B3B1F5BFD4DE6591"><span class="codeph"> MIRACAST</span> </li> 
     <li id="li_51E7DE83679F4630B01264407DAD0E84"><span class="codeph"> JOGO AÉREO</span> </li> 
     <li id="li_D499A0487AAC409CB2CEA6164265D3CF"><span class="codeph"> DLNA</span> </li> 
     <li id="li_4FCC0EC4A0FC48F99A13EC8A1B78D6A1"><span class="codeph"> WIDI</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.resolution</span> </td> 
   <td colname="2" class="- topic/entry "> Especifica o arquivo de configuração no qual as restrições baseadas em resolução são definidas. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o nível de segurança mínimo para permitir que o módulo DRM acesse conteúdo protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O módulo de tempo de execução do aplicativo deve ter pelo menos o nível mínimo de segurança especificado para acessar conteúdo protegido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uma lista de permissões de aplicativos não Flash (Adobe AIR, iOS, Android etc.) que podem reproduzir conteúdo protegido. A propriedade deve usar o seguinte formato: <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uma lista de permissões de aplicativos SWF que podem reproduzir conteúdo protegido. A propriedade deve usar o seguinte formato: </p> <p class="- topic/p "> 
     <ul id="ul_EC20F52AD95C4BE3B7F703048A43CDF0"> 
      <li id="li_3E4A47D925C24834A2C25BC5943279D4"><span class="+ topic/ph pr-d/codeph codeph">URL</span> </li> 
      <li id="li_9A7CAF081C5F488FB5CDA6D38C5552F6"><span class="+ topic/ph pr-d/codeph codeph">file=swf_file</span> </li> 
      <li id="li_E10EA4223137489CBE4015DE999F7154"><span class="codeph">time=max_time_to_verify</span> </li> 
     </ul> <i class="+ topic/ph hi-d/i ">swf_file</i> é o arquivo SWF usado para calcular o hash, e <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> é o tempo máximo em segundos permitido para o download e verificação do SWF ser concluído. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Pares de nome/valor personalizados que devem ser incluídos nas licenças quando as licenças forem emitidas para os usuários. É necessário especificar o seguinte formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n=name</span> </p> <p class="- topic/p ">É possível definir essa opção várias vezes para várias propriedades personalizadas. </p> </td> 
  </tr> 
 </tbody> 
</table>
