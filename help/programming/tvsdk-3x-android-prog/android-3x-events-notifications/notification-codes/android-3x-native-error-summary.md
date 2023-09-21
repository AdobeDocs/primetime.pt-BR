---
title: Detalhes da notificação NATIVE_ERROR
description: Detalhes da notificação NATIVE_ERROR
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '6868'
ht-degree: 2%

---

# Detalhes da notificação NATIVE_ERROR {#details-for-the-native-error-notification}

Quando o TVSDK lida com um erro nativo, ele retorna alguns ou todos os valores de chave de metadados a seguir como cadeias de caracteres.

<table id="table_7F713B7A56024D8DA3C84E449D09CC91"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Nome da chave de metadados</b></th> 
   <th colname="col2" class="entry"><b>Valor de metadados</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR_CODE</span> </td> 
   <td colname="col2"> <p>Código de erro nativo do AVE. </p> <p>Esses códigos representam o seguinte: 
     <ul id="ul_1F33D523DDFE4CE8B4F0DC279FF7E4F8"> 
      <li id="li_07A2D9BEE6364935A61EF3BD4AB6DE27">Erros DRM (códigos 3300 a 3367). Esses são os mesmos que os códigos de erro de Flash Player equivalentes </li> 
      <li id="li_433BA22DE3504AEEB623598BB4F939FA">Erros de reprodução de vídeo (-1 a 89) </li> 
      <li id="li_B347CB151DB94DE0A1DDEB1B33D2DABA">Erros de criptografia (300 a 307) </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR</span> </td> 
   <td colname="col2">Breve descrição da notificação (por exemplo, <span class="codeph"> AXS_VoucherInválido</span> ou <span class="codeph"> DECODIFICADOR_FALHA</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESCRIÇÃO</span> </td> 
   <td colname="col2"> Descrição longa da notificação (por exemplo, Falha na operação de resolução de anúncio). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR_CODE</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> valor numérico como uma string (por exemplo, "13"). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> como uma string (por exemplo, <span class="codeph"> kECNetworkError</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AVISO</span> </td> 
   <td colname="col2"> Descrição do aviso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ERRO</span> </td> 
   <td colname="col2"> Descrição do erro. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>DRM</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_SUBERROR_CODE</span> </td> 
   <td colname="col2"> Erro secundário do módulo DRM. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_STRING</span> </td> 
   <td colname="col2"> Descrição do erro. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_SERVER_URL</span> </td> 
   <td colname="col2"> URL do servidor DRM com o qual o TVSDK tentou se comunicar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Falha no carregamento do manifesto de anúncio</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_URL</span> </td> 
   <td colname="col2"> URL do conteúdo que não foi carregado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_TYPE</span> </td> 
   <td colname="col2">Tipo de anúncio (uma constante do <span class="codeph"> MediaResource.Type</span> enum). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_DURATION</span> </td> 
   <td colname="col2"> Duração do anúncio em milissegundos. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_ID</span> </td> 
   <td colname="col2"> ID atribuída ao anúncio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Erros de arquivo</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="col2"> Descrição do erro durante o download do arquivo de mídia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> URL</span> </td> 
   <td colname="col2"> URL do arquivo que está sendo baixado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> MANIFEST_ERROR</span> </td> 
   <td colname="col2"> Descrição do erro durante o download do arquivo de manifesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="col2">Descrição do erro durante o fragmento (por exemplo, <span class="codeph"> ts</span>) baixar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Erros de trilha de áudio</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_NAME</span> </td> 
   <td colname="col2"> Nome da faixa de áudio que não foi carregada, conforme especificado no manifesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_LANGUAGE</span> </td> 
   <td colname="col2"> Idioma da faixa de áudio, conforme especificado no manifesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Buscar erros</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_PERIOD</span> </td> 
   <td colname="col2"> ID do período (número inteiro). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_POSITION</span> </td> 
   <td colname="col2"> <p>Posição (em milissegundos) procurada (duplo). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Diversos</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDITUDE_ERROR_CODE</span> </td> 
   <td colname="col2"> código de erro Auditude (número). </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: valores DRM {#section_D240082B93D34902A18C3923C1C717B3}

A interface do Codificador de vídeo do mecanismo de vídeo Adobe retorna essas notificações DRM na variável `NATIVE_ERROR` objeto de metadados.

Ao relatar erros de DRM para o Adobe, inclua a variável `NATIVE_SUBERROR_CODE` e `DRM_ERROR_STRING` para obter ajuda com a solução de problemas.

>[!TIP]
>
>Esta lista fornece informações específicas do TVSDK sobre os erros. Para obter descrições completas, consulte [Referência de ActionScript de erros de tempo de execução do ActionScript para a Adobe Flash Platform](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html#3300).

<table id="table_CD59A859865F4FFDBAA249C89C74770A"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Valor para a chave de metadados NATIVE_- ERROR_CODE</b></th> 
   <th colname="col2" class="entry"><b>Valor para a chave de metadados NATIVE_ERROR_NAME</b></th> 
   <th colname="col3" class="entry"><b>Significado</b></th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 3300 </td> 
   <td colname="col2"><span class="codeph"> AXS_VoucherInválido</span> </td> 
   <td colname="col3"> 
    <ul id="ul_516E4CB32D624B22892DDB9266CB04CA"> 
     <li id="li_348FC0F38B11417994119B61C9244076">O que o software do distribuidor deve fazer: 
      <ul id="ul_7AFD45CF92454BA4927783FAA628FBC4"> 
       <li id="li_0D9CCE61612643648C12DCDDD252E52A">Se você estiver usando o Google Chrome, estiver no modo Incógnito e a versão do Flash Player for anterior à 11.6, este erro pode ocorrer. <p>Recomendamos que o reprodutor verifique o número da versão do navegador e aconselhe o usuário a sair do modo Incógnito. </p> </li> 
       <li id="li_1DC6B755BD0840D48BEC92568FD330BA">Solicite a licença novamente. <p>Se a solicitação for bem-sucedida, não será necessário registrar nem escalar. Se a solicitação não tiver êxito, registre o conteúdo que causou o erro. <span class="codeph"> subErrorId</span> contém um erro de linha, se presente. </p> </li> 
      </ul> </li> 
     <li id="li_060B5D60C9BB419CBFA7B062FBCF2632">O que o distribuidor deve fazer: 
      <ul id="ul_FADB29DBF0DA4A0E8E54134AEB7DCD8A"> 
       <li id="li_FC5B1C04D21E4AECB0EBD9ADD3198504">Se as tentativas forem malsucedidas em configurações diferentes do Chrome com Flash inferior à versão 11.6, uma falha pode ter ocorrido no pacote. </li> 
       <li id="li_A720ECE591254021879B335B81B1F76D">Verifique se o problema é específico de determinado conteúdo e reempacote. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3301 </td> 
   <td colname="col2"><span class="codeph"> AXS_AuthenticationFailed</span> </td> 
   <td colname="col3"> <p>O servidor não pôde autenticar ou autorizar o cliente. </p> 
    <ul id="ul_BE77AC1848FB4C09B6318359ACF1B8EE"> 
     <li id="li_6FB37D317D174E8488C5070D20CD241C">O software do distribuidor deve tomar todas as medidas necessárias para restabelecer as credenciais do usuário ou orientá-lo a adquirir acesso ao conteúdo. </li> 
     <li id="li_BE071D59805B42D38E3E7650BC936417">O distribuidor deve confirmar que o mecanismo de autorização e autenticação do distribuidor está a funcionar corretamente. <p>Se os distribuidores não estiverem planejando usar os recursos de autenticação ou autorização, eles deverão verificar se a política do conteúdo ofensivo requer autenticação e ver Discrepâncias de política/licença de diagnóstico. </p> </li> 
    </ul> <p>Para obter mais informações sobre esse código de erro, consulte <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> Causas e resolução do erro DRM 3301</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3302 </td> 
   <td colname="col2"><span class="codeph"> AXS_RequireSSL</span> </td> 
   <td colname="col3"> <p>No Access 4.0 e superior, esse erro é lançado no iOS quando o URL da chave remota não usa HTTPS como esquema. HTTPS é necessário. </p> 
    <ul id="ul_3D47777BBCA14B67B107FBBE3E37E40C"> 
     <li id="li_7F7BBB27AE754CC39ABAAF9269739C49">Se o distribuidor estiver usando uma versão anterior ao Access v4 ou a versão pelo menos 4, mas a plataforma não for iOS, o software do distribuidor deverá registrar o erro. <p>O erro é lançado somente no iOS. </p> </li> 
     <li id="li_D83C427D2A0D47408F723EF7195070B6">Se o software do distribuidor for pelo menos o Adobe Access versão 4 e a plataforma for iOS, os distribuidores deverão alterar o URL do servidor da chave remota que estão usando para HTTPS. <p>Se eles estiverem usando apenas HTTP, talvez os distribuidores precisem configurar um servidor HTTPS. Caso contrário, os distribuidores precisarão enviar as informações registradas para o Adobe e encaminhar o problema. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3303 </td> 
   <td colname="col2"><span class="codeph"> AXS_ContentExpired</span> </td> 
   <td colname="col3"> <p>O conteúdo que você está visualizando expirou de acordo com as regras definidas pelo provedor de conteúdo. subErrorId contém um erro específico do cliente ou erro de linha. </p> <p> 
     <ul id="ul_1E4B3B8AE87A4E79997553BB2A0E52B9"> 
      <li id="li_EE3F2EEBF73743B9A38E4FCB7531E275">O software do distribuidor deve tentar readquirir uma licença do servidor uma vez para determinar se uma nova licença não expirada está disponível. <p>Se nenhuma licença estiver disponível ou a licença tiver expirado, permita que o usuário adquira uma nova licença ou informe ao usuário que o conteúdo não pode ser assistido.Se o conteúdo tiver sido empacotado com uma política que tenha uma data de expiração/término expirada, os registros do servidor de licença relatarão um <span class="codeph"> ExceçãoDeAvaliaçãoDePolítica</span> e declaram que a Data final da política expirou (Código de erro do servidor 303). Verifique os arquivos de log do servidor. </p> <p>Se possível, os clientes devem verificar a política usada durante o empacotamento para ver se ela expirou. A ferramenta de linha de comando Java é: <code> java&nbsp;-jar&nbsp;libs/AdobePolicyManager.jar&nbsp;&nbsp;&nbsp;detail&nbsp;demo.pol</code> </p> </li> 
      <li id="li_50DBE680D8F04E7DA3E29C65A93188E7">O distribuidor deve confirmar se as datas de expiração da licença estão configuradas conforme esperado. </li> 
     </ul> </p> <p>Para obter mais informações sobre esse código de erro, consulte <a href="https://forums.adobe.com/thread/1300813" format="https" scope="external"> 3303 (Conteúdo expirado) com AMS/FMS usando um Live Stream?</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3304 </td> 
   <td colname="col2"><span class="codeph"> AXS_AuthorizationFailed</span> </td> 
   <td colname="col3">Para obter mais informações sobre esse código de erro, consulte <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> Causas e resolução do erro DRM 3301</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3305 </td> 
   <td colname="col2"><span class="codeph"> AXS_ServerConnectionFailed</span> </td> 
   <td colname="col3"> <p>A conexão com os servidores de licença ou de domínio atingiu o tempo limite devido a um atraso de rede ou porque o cliente estava offline. Normalmente, o subErrorId contém o código de retorno HTTP. </p> 
    <ul id="ul_938C7D8F07F64B4FA71A09DDF37E2E64"> 
     <li id="li_6648EA0049094E369BD9AE9CCA6B148D">O software do distribuidor deve tentar uma conexão de rede com um servidor em boas condições. <p>Se a tentativa falhar, peça para o usuário se reconectar à rede. Se a tentativa for bem-sucedida, registre-a. </p> </li> 
     <li id="li_2ECA2C04BA08449DA3AD79A52EFAA229">O distribuidor deve verificar se as licenças e os servidores de domínio em uso estão online e visíveis na rede do cliente. </li> 
    </ul> <p>Para obter mais informações sobre esse código de erro, consulte <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> Causas e resolução do DRM 3305 [ServerConnectionFailed]</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3306 </td> 
   <td colname="col2"><span class="codeph"> AXS_ClientUpdateRequire</span> </td> 
   <td colname="col3"> Use uma versão mais recente do TVSDK para Android. <p>O cliente atual não pode concluir a ação solicitada, mas um cliente atualizado pode conseguir concluir a solicitação. </p> <p>Isso pode ter várias causas: 
     <ul id="ul_2EC4D42D5273439FA1AFDA1A2578B3D6"> 
      <li id="li_FCA926F5FAED4E7190BE855545AB6ACF">Um domínio compartilhado que não está disponível neste cliente foi usado. Esse provavelmente é o caso quando a reprodução funciona no Chrome, mas não em qualquer outro navegador e vice-versa. <p> <p>Dica: o Chrome usa uma chave PHDS/PHLS diferente da usada pelos outros navegadores. Para obter mais informações, consulte <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </p> </li> 
      <li id="li_3B633FB699234DCEA136E9BE3CC3386D">O aplicativo está tentando adicionar várias DRMSessions ao ser executado em uma versão do iOS anterior à 5.0. </li> 
      <li id="li_F7ED993AF0B941A7A27216B4D587A999">Os metadados têm uma versão de 3 ou superior quando há suporte apenas para a versão 2. </li> 
     </ul> </p> 
     <ul id="ul_EE4AE6AD4F1745A5B5623E53B599DB62"> 
      <li id="li_7A83869D4262443DA35FA1DF8D3097DD">O software do distribuidor deve alertar o usuário e interromper a operação. <p>Se o software tiver uma maneira de determinar se um upgrade está disponível, direcione o usuário para esse upgrade da maneira apropriada para a plataforma. </p> </li> 
      <li id="li_AF9C2711FDE54DA196EB9D2864632000">Se o problema ocorrer devido a um domínio compartilhado, o distribuidor precisará verificar com o Adobe se há um tempo de execução ou biblioteca atualizada. <p>Para o tempo de execução do Flash, o distribuidor pode forçar a atualização em seu aplicativo diretamente. No caso de uma biblioteca, o distribuidor precisará obter uma biblioteca atualizada, reconstruir o aplicativo e implantá-la nos usuários. </p> <p>Se o problema ocorrer devido a várias DRMSessions, o distribuidor precisará atualizar o aplicativo para verificar o número da versão do iOS antes de adicionar várias DRMSessions. Ou eles podem restringir a distribuição de seus aplicativos no iOS v5 e superior. </p> <p>se o problema ocorrer porque a versão dos metadados é superior à versão 2, o problema provavelmente são metadados corrompidos. Eles podem tentar reconstruir os metadados e observar os resultados. Se o problema persistir, registre o problema e encaminhe para Adobe. </p> </li> 
     </ul> <p>Para obter mais informações sobre esse código de erro, consulte <a href="https://forums.adobe.com/thread/1266675" format="https" scope="external"> Como corrigir um código de erro 3306 DRMErrorEvent</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3307 </td> 
   <td colname="col2"><span class="codeph"> AXS_InternalFailure</span> </td> 
   <td colname="col3"> <p>Isso geralmente representa um bug no código de acesso do Adobe e é inesperado, a menos que haja um bug conhecido, como abaixo. subErrorId contém um erro específico do cliente ou erro de linha. </p> 
    <ul id="ul_79F4A9655A2148519B1E9509C41F78C3"> 
     <li id="li_0E093AB4D6BD489B852279E6C1525A15">Se o navegador for o Chrome no Windows e a versão do Flash for 11.6 (SWF versão 19 ou superior), o software do distribuidor deve supor que o usuário pressionou <span class="uicontrol"> Negar</span> na barra de informações e trate o mesmo que um 3368. </li> 
     <li id="li_0215D1089B344861A2C0A73E1067CFEF">Se o 3307 ocorrer quando o navegador não for o Chrome ou a versão do Flash não for a 11.6, o distribuidor deverá encaminhar para o Adobe. </li> 
    </ul> <p>Importante: <span class="codeph"> 3307:1107296344 (FailedToGetBrokerHandle)</span> O pode acontecer com as versões 24-28 do navegador Chrome. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3308 </td> 
   <td colname="col2"><span class="codeph"> AXS_ChaveDeLicençaErrada</span> </td> 
   <td colname="col3"> <p>Esse erro é lançado sempre que a licença que está sendo usada contém a chave errada para descriptografar o conteúdo. subErrorId contém um erro específico do cliente ou erro de linha. </p> <p>Parece que há apenas duas maneiras de gerar esse erro: 
    <ul id="ul_1C955BD74C7843809D1B5A0CDCA5ED7B"> 
     <li id="li_18F0A7FDA6584887AD9DB3EDE54080D8">O cliente modificou a ferramenta Adobe padrão para gerar licenças (por exemplo, a estrutura Java do servidor de licenças). <p>Nesse caso, a licença contém uma chave incorreta que pode não corresponder a nenhum conteúdo. </p> </li> 
     <li id="li_21D04ED1F1FA464785BC297D385766FF">O cliente emitiu várias licenças com a mesma ID de licença. <p>Nesse caso, há várias licenças disponíveis no cliente que correspondem aos metadados do conteúdo, e o código de acesso selecionou a incorreta para uso. </p> </li> 
    </ul> </p> 
    <ul id="ul_64AEE62BE36946F290067CF475A36ECA"> 
     <li id="li_9EEB2B11A4DA41E78C5840D8FAA81F0D">O software do distribuidor deve tentar readquirir a licença do servidor. 
      <ul id="ul_ACADC5518B054D0A853AEED2B675DB23"> 
       <li id="li_394835C8731048A5BF7D9370AC12448C">Se nenhuma licença estiver disponível ou tiver expirado, forneça um fluxo de trabalho para o usuário adquirir nova licença ou informe ao usuário que o conteúdo não pode ser assistido e registre o problema. </li> 
       <li id="li_3FE50518BE53405F9563FA620F7EAD5F">Se era um conteúdo vinculado a um domínio (para AIR), forneça uma maneira de o usuário ingressar no domínio. </li> 
      </ul> </li> 
     <li id="li_C80B353C1AEA4E9398241420CB491E84">O distribuidor deve: 
      <ul id="ul_B5C50009374C4EED9B2B050B48F5F0F6"> 
       <li id="li_D5E6B760E0BC4B5C949ED1544B398838">Verifique se eles não personalizaram as partes de emissão da licença do servidor de Licença de Acesso. </li> 
       <li id="li_AA8F4E4B6DDD40BA8807C0920A92186B">Verifique se estão emitindo IDs de licença exclusivas para todas as licenças. </li> 
       <li id="li_A2C53FE779AC4FDDB65E00A2C4F43EC4">Escalone o problema com o Adobe. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3309 </td> 
   <td colname="col2"><span class="codeph"> AXS_CorruptedAdditionalHeader </span> </td> 
   <td colname="col3"> <p>Isso ocorrerá se o cabeçalho tiver mais de 65536 bytes. </p> 
    <ul id="ul_82C0F688519B4F43A764D59A891F1903"> 
     <li id="li_E66AC9149A0649E88A79C5289C12C395">O software do distribuidor deve registrar qual parte do conteúdo causou o erro. </li> 
     <li id="li_1C5916A33E7B4DC9968105B9BD20A727">O distribuidor deve confirmar que o erro é reproduzível com partes específicas do conteúdo. Reempacotar conteúdo corrompido. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3310 </td> 
   <td colname="col2"><span class="codeph"> AXS_AppIDMismatch </span> </td> 
   <td colname="col3">O aplicativo Android não corresponde ao aplicativo em uso. <p>O aplicativo AIR ou SWF de Flash correto não está sendo usado. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3311 </td> 
   <td colname="col2"><span class="codeph"> AXS_AppVersionMismatch </span> </td> 
   <td colname="col3"> Não está em uso. Esse problema ainda pode ser gerado pela pilha da versão 1.x no AIR. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3312 </td> 
   <td colname="col2"><span class="codeph"> AXS_LicenseIntegrity </span> </td> 
   <td colname="col3"> Para corrigir isso, baixe novamente a licença do servidor. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3313 </td> 
   <td colname="col2"><span class="codeph"> AXS_WriteMicrosafeFailed </span> </td> 
   <td colname="col3"> <p>Esse problema ocorre quando o sistema não consegue gravar no sistema de arquivos. <span class="codeph"> subErrorId</span> contém um erro específico do cliente ou erro de linha. </p> <p>No Microsoft Windows, o erro 3313 pode ser lançado pelo flash player do plug Ative X ou NPAPI quando o conteúdo criptografado tem uma licenseID ou uma policyID muito longa. Isso se deve ao comprimento máximo do caminho no Windows. (O plug-in Pepper não tem esse problema.) </p> <p>Consulte watson 3549660 </p> 
    <ul id="ul_DFD527D1E1224A439766DF7BED878E3B"> 
     <li id="li_FAF8FD98A4E8478CA7A92F770676ADFC">O software do distribuidor deve solicitar que o usuário confirme se seu diretório de usuário não está bloqueado nem em um volume que esteja cheio ou bloqueado. </li> 
     <li id="li_6D1136EA750A459BBECEEE5F73F527BB">Se o distribuidor estiver usando o AIR, em vez do Flash, o problema pode ser causado por uma limitação de comprimento de caminho. <p>Os distribuidores devem encurtar o nome do aplicativo AIR para algo razoável. Além disso, publique o conteúdo novamente com um menor <span class="codeph"> licenseID</span> e uma <span class="codeph"> policyID</span>. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3314 </td> 
   <td colname="col2"><span class="codeph"> AXS_MetadadosDRMMrompidos </span> </td> 
   <td colname="col3"> <p>Esse erro geralmente indica que o conteúdo foi empacotado com certificados PKI de teste e o reprodutor é criado com PKI de produção ou vice-versa. subErrorId contém um erro específico do cliente ou erro de linha. </p> 
    <ul id="ul_A122EF304CAF48A8B4DA1E3F4413E29B"> 
     <li id="li_A9A1A5B23E884C22A71E2DE7535FEB3B">O software do distribuidor deve registrar qual parte do conteúdo causou o erro. </li> 
     <li id="li_7AD7F13A4B1B4998A7E49664E7645815">O distribuidor deve confirmar que o erro é reproduzível com conteúdos específicos. <p>Talvez seja necessário reempacotar o conteúdo com falha. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3315 </td> 
   <td colname="col2"><span class="codeph"> AXS_PermissionDenied </span> </td> 
   <td colname="col3"> <p>Há bugs conhecidos nos quais esse código de erro é lançado quando um 3305 é pretendido. Para obter mais informações, consulte <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> Causas e resolução do DRM 3305 [ServerConnectionFailed]</a>. </p> <p>O SWF remoto carregado pelo AIR não tem permissão para acessar a funcionalidade do Flash Access. Esse código de erro também pode ser lançado se ocorrer um erro de segurança durante o acesso à rede. Os exemplos incluem o servidor de destino no qual o cliente não pode se conectar usando o crossdomain.xml ou o crossdomain.xml não está acessível. </p> <p>Para obter mais informações, consulte <a href="https://forums.adobe.com/thread/1266592" format="https" scope="external"> Possível causa raiz e resolução do erro DRM 3315</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3316 </td> 
   <td colname="col2"><span class="codeph"> AXS_NOTUSED_MOVED </span> </td> 
   <td colname="col3"> Foi <span class="codeph"> ADOBECPSHIM_MinorErr_MissingAdobeCPModule</span>. Movido para 3344 devido a conflito com o código de erro do Flash. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3317 </td> 
   <td colname="col2"><span class="codeph"> AXS_LoadAdobeCPFailed </span> </td> 
   <td colname="col3"> <p>Importante: esse é um erro raro e geralmente não ocorre em um ambiente de produção. </p> <p>Se o erro ocorrer, siga um destes procedimentos: 
     <ul id="ul_BC435E61623444BB98A86216531DC892"> 
      <li id="li_FA433D0758B642D2AFDCF04906B3FE18">Se você estiver usando o AIR, reinstale-o. </li> 
      <li id="li_F08D9AAFF46244F8842DEE5FD9CBBE0A">Se estiver usando o Flash Player, baixe o <span class="codeph"> AdobeCP</span> módulos novamente. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3318 </td> 
   <td colname="col2"><span class="codeph"> AXS_IncompatibleAdobeCPVersion </span> </td> 
   <td colname="col3"> Não aplicável para Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3319 </td> 
   <td colname="col2"><span class="codeph"> AXS_MissingAdobeCPGetAPI </span> </td> 
   <td colname="col3"> Não aplicável para Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3320 </td> 
   <td colname="col2"><span class="codeph"> AXS_HostAuthenticateFailed </span> </td> 
   <td colname="col3"> Não aplicável para Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3321 </td> 
   <td colname="col2"><span class="codeph"> AXS_I15nFalha </span> </td> 
   <td colname="col3"> <p>Falha no processo de provisionamento do cliente com chaves. subErrorId contém um erro de linha, específico do servidor ou do cliente. </p> 
    <ul id="ul_98D919B9060A441AACB6106F6D8E8DA7"> 
     <li id="li_DCAB00A8AC4A426CBBD377374B3F71AE">O software do distribuidor deve repetir a operação pelo menos uma vez. <p>Se você estiver usando o Google Chrome no Windows, forneça uma explicação sobre como permitir o acesso ao plug-in que não está em uma sandbox. Acesso à unsandbox do Google Chrome negado</a>. </p> </li> 
     <li id="li_7FB7681FE32D444BB1BDBA3E5953A2C3">O distribuidor deve concluir uma das seguintes tarefas: 
      <ul id="ul_486B64F187C44AE3B4775953A6142836"> 
       <li id="li_095B1D4CD051427CB2BFA7082B454056">Se o erro for consistente em todas as plataformas, você deverá escalonar o problema com o Adobe. </li> 
       <li id="li_0C6EB7B912FA41E59657216498DA3515">Se o erro estiver limitado ao Chrome no Windows, oriente o usuário a permitir acesso a plug-in fora da área restrita. </li> 
      </ul> <p>Os distribuidores devem atualizar seu SWF para a versão 19 ou posterior, e o erro 3321 específico do Chrome, um erro 3368 é lançado. O erro 3368 pode ser tratado mais especificamente pelo software do distribuidor. Essa alteração foi introduzida no canal Chrome Stable versão 26.0.1410.43. </p> <p>Dica: Erro <span class="codeph"> 3321:1090519056</span> pode acontecer com as versões 11.1 a 11.6 do Flash Player. Recomendamos que você atualize para a versão mais recente do Flash Player. </p> </li> 
    </ul> <p>Para obter mais informações, consulte <a href="https://forums.adobe.com/thread/1277138" format="https" scope="external"> Erro DRM 3321 Causes &amp; Resolution</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Erros de corrupção do armazenamento global</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3322 </td> 
   <td colname="col2"><span class="codeph"> AXS_DeviceBindingFailed </span> </td> 
   <td colname="col3"> <p>O dispositivo não parece corresponder à configuração que estava presente quando inicializado. subErrorId contém um erro de linha ou específico do cliente. </p> <p>O software do distribuidor deve executar uma das seguintes tarefas: 
     <ul id="ul_444401051A2E407B95BC44491E9BB71C"> 
      <li id="li_93493EA05DB44CB1AEC368663F1ABA8D"> <p>Se o dispositivo não estiver usando o Flash Player e estiver usando o AIR, iOS e assim por diante, chame <span class="codeph"> DRMManager.resetDRMVouchers()</span>. </p> <p>Se o problema ocorrer no iOS em uma fase de desenvolvimento, peça ao desenvolvedor para confirmar se o problema é observado ao alternar entre builds que foram baixadas de sistemas de distribuição de pré-lançamento de terceiros (por exemplo, HockeyApp) e uma build local do Xcode. Os atributos de uma instalação anterior não são totalmente substituídos ao alternar entre uma build distribuída do HockeyApp e uma build do Xcode. Essa situação pode acionar o erro 3322. </p> <p>Para resolver esse problema, o desenvolvedor deve remover a build mais antiga do dispositivo antes de instalar a nova build. </p> </li> 
      <li id="li_A5C9633F11584C788A2D9A23CC18FA6D">Se o dispositivo estiver usando o Flash Player e não puder ser usado a partir de códigos de erro 3322 ou 3346, consulte as instruções do Adobe sobre como redefinir programaticamente o armazenamento de licenças DRM em <a href="https://forums.adobe.com/message/5535907#5535907" format="https" scope="external"> Erro de DRM 3322/3346/3368 no Chrome (problemas na barra de informações)</a>. </li> 
     </ul> </p> <p>Este erro não é esperado com frequência. Em ambientes corporativos que usam perfis móveis, se um usuário estava visualizando conteúdo protegido por DRM, a probabilidade de ocorrência do erro 3322 aumenta à medida que o usuário faz logon em máquinas diferentes. Se possível, o distribuidor deve tentar obter essas informações do usuário. </p> <p>Se o erro ocorrer com frequência, encaminhe para Adobe. Você deve notificar o Adobe se a redefinição do armazenamento de licenças resolveu (ou não) o problema e informar ao Adobe em quais navegadores o erro está ocorrendo. </p> <p>Para obter mais informações, consulte os seguintes artigos: 
     <ul id="ul_C468409D1EA046178CA7F54DCDCB84EA"> 
      <li id="li_20C8CA3853574CE486F21E7A3667DAB9"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> https://forums.adobe.com/message/5520902</a> </li> 
      <li id="li_6E6F1BD6FE7843449B3E2F06F342EFF7"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> https://forums.adobe.com/message/5535911</a> </li> 
      <li id="li_2BE40E513A0C4BAD900C7B69FEF5D690"><a href="https://forums.adobe.com/message/5748618" format="https" scope="external"> https://forums.adobe.com/message/5748618</a> </li> 
      <li id="li_9C2BD122E3874E2893DD43E082A877E0"><a href="https://forums.adobe.com/message/6061165" format="https" scope="external"> https://forums.adobe.com/message/6061165</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3323 </td> 
   <td colname="col2"><span class="codeph"> AXS_CorruptGlobalStateStore </span> </td> 
   <td colname="col3"> <p>Os arquivos usados pelo cliente DRM foram modificados inesperadamente. subErrorId contém um erro de linha ou específico do cliente. </p> 
    <ul id="ul_96EA771046CA4B2B9FAE24D493F43FF2"> 
     <li id="li_D2693CD8EFEF46108828BA17E3F54FF6">O software do distribuidor deve orientar o usuário a redefinir da mesma forma que para o 3322. </li> 
     <li id="li_0149B82436B64E28AC2B8C9B0EB09898">Se o GlobalStore estiver falhando a uma taxa maior que a taxa de falha esperada dos discos rígidos da sua base de usuários, transfira o problema para o Adobe. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3324 </td> 
   <td colname="col2"><span class="codeph"> AXS_MachineTokenInvalid </span> </td> 
   <td colname="col3"> Redefinir o armazenamento local DRM para este aplicativo. Chame DRMManager.resetDRM. <p>Talvez o servidor de licenças não possa se conectar ao servidor CRL (Lista de Certificados Revogados) para atualizar seus arquivos CRL, ou a máquina cliente está solicitando uma licença/autenticação que foi revogada pelo servidor de licenças. </p> <p>Nos registros do servidor, um código de erro 111 é MachineTokenInvalid. No entanto, no nível do cliente, o código de erro 111 é convertido no código de erro 3324. </p> <p>O administrador do servidor de licenças DRM deve verificar se o servidor de licenças do cliente conseguiu recuperar os arquivos CRL do Adobe. Se o cliente estiver usando o Tomcat, ele poderá verificar a<span class="filepath"> tomcat/temp/</span> diretório para ver se há 4 arquivos CRL. </p> 
    <ul id="ul_23B7F1A104AF49E79EA87DB8E15E337E"> 
      <li id="li_855D87F251184FE688A8D5FA0F6C9EF5">Se os arquivos estiverem nesse diretório, clique duas vezes nos arquivos no Windows Explorer e no aplicativo visualizador de CRL para determinar se algum dos arquivos expirou. </li> 
      <li id="li_58EC4EDA2B5146188A0FF7B33C91E2FD">Se não houver arquivos em tomcat/temp/, pode-se supor que este servidor de licença nunca foi capaz de alcançar o servidor CRL Adobe devido a um problema de firewall/roteamento. Para obter mais informações, consulte <a href="https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_secure_deployment_guidelines.pdf" format="http" scope="external"> Regras de firewall.</a></li>
    </ul> </p> <p>Se os arquivos da CRL não estiverem disponíveis ou tiverem expirado, você deverá confirmar se o servidor de licenças pode ser acessado. Abra um farejador de rede no servidor de licenças do cliente, reinicie o servidor e peça a um cliente que tente solicitar uma licença do servidor. Você pode observar o tráfego da rede para ver se as chamadas para os seguintes pontos de extremidade de URL são bem-sucedidas: <p>Dica: você também pode inserir as seguintes URLs de CRL em um navegador para ver se é possível baixar manualmente cada arquivo. </p> 
    <ul id="ul_9B65C7ABBDEC4AC9BF3755FFD3587971"> 
      <li id="li_6867A9050E8D421C9138AC853D1784C9"><a href="https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl</a> </li> 
      <li id="li_6431689260554EAFAFDA2EC31798DCB5"><a href="https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl</a> </li> 
      <li id="li_2939674D0F854ADEB67E45FD216288A2"><a href="https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessRootCA.crl</a> </li> 
      <li id="li_96386E00BE9D4CB99D100057A5F7C6DD">crl3.adobe.com/AdobeSystemsIncorporated FlashAccessRuntime/LatestCRL.crl</li> 
    </ul> </p> <p>Se as regras de firewall estiverem abertas e não houver erros 3324 atuais, pode ter havido um problema temporário de rede. Verifique os registros do servidor do cliente, que provavelmente estão no <span class="codeph"> /tomcat/logs/</span> para determinar se ocorreu um erro quando o servidor de licenças tentou buscar as Listas de Revogação de Certificado. <p>Importante: pode ocorrer um erro quando um grande número (ou uma intermitência) de clientes relatam um erro 3324 a um problema temporário de rede ao renovar um arquivo CRL. Quando o problema de rede foi resolvido, os problemas do 3324 também foram resolvidos. </p> </p> <p>Se todos os 4 arquivos da CRL existirem no <span class="filepath"> tomcat/temp/</span> e os clientes ainda estiverem recebendo códigos de erro 3324, pode haver problemas de acesso a arquivos da CRL. Para resolver esse problema, talvez você queira revisar os logs e limpar os arquivos CRL existentes. </p> <p>Se não houver problemas no servidor, solicite que o usuário redefina no conforme descrito em 3322. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Erros de corrupção do Repositório do Servidor</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
</tr> 
  <tr> 
   <td colname="col1"> 3325 </td> 
   <td colname="col2"><span class="codeph"> AXS_CorruptServerStateStore </span> </td> 
   <td colname="col3"> <p>Os arquivos usados pelo cliente DRM foram modificados inesperadamente. <span class="codeph"> subErrorId</span> contém um erro de linha ou específico do cliente. </p> 
    <ul id="ul_860D2402DA61460AB0D938F1116F6D64"> 
     <li id="li_CF368C43452B4265B62ADA3E223894BA">O software do distribuidor deve repetir a operação, pois o Adobe CP excluiu o armazenamento de servidor incorreto internamente e uma nova tentativa deve ser bem-sucedida. Se a nova tentativa falhar, registre o problema. </li> 
     <li id="li_51A5803A1F754970BB4EBD6494F5DC96">Se as tentativas estiverem falhando a uma taxa maior que a taxa de falha esperada dos discos rígidos da sua base de usuários, transfira o problema para o Adobe. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3326 </td> 
   <td colname="col2"><span class="codeph"> AXS_StoreTamperingDetected </span> </td> 
   <td colname="col3"> Chame <span class="codeph"> DRMManager.resetDRM</span>. <p>O repositório de licenças foi violado/corrompido e não pode mais ser usado. </p> <p>O software do distribuidor deve orientar o usuário a redefinir da mesma forma descrita em 3322. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3327 </td> 
   <td colname="col2"><span class="codeph"> AXS_ClockTamperingDetected </span> </td> 
   <td colname="col3"> Corrija o relógio ou adquira <span class="codeph"> Autn/Lic/Domain</span> licença novamente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Erros de servidor de Autenticação/Licença/Domínio</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3328 </td> 
   <td colname="col2"><span class="codeph"> AXS_ServerErrorTryAgain </span> </td> 
   <td colname="col3"> <p>Este é um erro do lado do servidor em que o servidor não pôde concluir a solicitação do cliente. Esse erro pode ocorrer quando, por exemplo, o servidor está ocupado, HTTP/500, o servidor não tem a chave necessária para descriptografar a solicitação e assim por diante. </p> <p>No cliente, não há como determinar o que deu errado. O cliente deve analisar os registros do servidor de acesso ao Adobe, que normalmente são chamados de <span class="codeph"> AdobeFlashAccess.log</span>, para determinar o que deu errado. Há sempre um rastreamento de pilha descritivo no log para indicar o problema. <span class="codeph"> subErrorId</span> contém um erro de linha ou específico do servidor. </p> <p>O distribuidor deve examinar os logs do servidor para identificar qual servidor está enviando esse erro. Para erros 3328 com código de suberro 101, o servidor não pode descriptografar a solicitação. O cliente deve validar se os certificados do servidor de licença/transporte instalados no servidor de licença correspondem e correspondem aos certificados usados durante a embalagem. </p> <p>Além disso, se os clientes estiverem usando a Implementação de referência, eles devem garantir que não haja erros de digitação na <span class="codeph"> flashaccess-refimpl.properties</span> arquivo onde os certificados primário e adicional são especificados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3329 </td> 
   <td colname="col2"><span class="codeph"> AXS_ApplicationSpecificError </span> </td> 
   <td colname="col3"> <p>O código de suberro específico do aplicativo não é conhecido pelo Flash Access. <span class="codeph"> subErrorId</span> contém um erro específico do servidor do servidor de licenças personalizado de editores. O servidor retornou um erro no namespace específico do aplicativo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3330 </td> 
   <td colname="col2"><span class="codeph"> AXS_NeedAuthentication </span> </td> 
   <td colname="col3"> <p>Esse erro ocorre quando o conteúdo é configurado para solicitar que os clientes se autentiquem antes de obter as licenças. </p> 
    <ul id="ul_712D29B8B5A6401FB014C4A283918E32"> 
     <li id="li_2D56905EB50D4FDEAD69CA8EAE38AD1A">O software do distribuidor deve autenticar o usuário e adquirir a licença novamente. <p>Se o serviço não pretende usar autenticação, registre a identificação do conteúdo que está causando esse erro. </p> </li> 
     <li id="li_B3BCF899B8BE41C7A4F7CF84B0503483">Esse erro não deve exigir um escalonamento, a menos que o conteúdo não deva ser configurado para exigir autenticação. <p>Nesse caso, reempacote o conteúdo ofensivo com a política adequada. Se o conteúdo for empacotado corretamente, consulte Diagnóstico de discrepâncias de política/licença. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Erros de Imposição de Licença que não são cobertos acima</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
</tr> 
  <tr> 
   <td colname="col1"> 3331 </td> 
   <td colname="col2"><span class="codeph"> AXS_ContentNotYetValid </span> </td> 
   <td colname="col3"> <p>A licença adquirida ainda não é válida. Para resolver esse problema, verifique se o relógio do cliente não está configurado corretamente. Para configurar o relógio do cliente, reempacote o conteúdo ou modifique a configuração do servidor de licenças. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3332 </td> 
   <td colname="col2"><span class="codeph"> AXS_CachedLicenseExpired </span> </td> 
   <td colname="col3"> Adquira novamente a licença do servidor. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3333 </td> 
   <td colname="col2"><span class="codeph"> AXS_PlaybackWindowExpired </span> </td> 
   <td colname="col3"> <p>Você deve notificar os usuários de que não é possível reproduzir esse conteúdo até que a política expire. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3334 </td> 
   <td colname="col2"><span class="codeph"> AXS_DRMPlatformInválido </span> </td> 
   <td colname="col3"> <p>Essa plataforma não tem permissão para reproduzir o conteúdo porque, por exemplo, o provedor de conteúdo configurou o Acesso ao Adobe para negar o conteúdo ao Adobe Acesso em uma plataforma ou uma licença de domínio compartilhado vinculada está vinculada a um token de domínio compartilhado destinado a uma partição diferente. </p> <p>O CDM pode gerar esse erro se o conteúdo não for empacotado usando uma certificação apropriada de empacotador (vinculada a recurso do CDM). </p> <p>Se o conteúdo for empacotado com um certificado PHDS/PHLS incorreto, ele poderá funcionar no Chrome, mas não em outros navegadores (ou vice-versa). <p>Dica: isso ocorre porque o Chrome usa certificados PHDS/PHLS diferentes. </p>Para confirmar qual certificado está sendo usado, descarte os detalhes dos metadados de conteúdo e procure a variável <i>certificados de recipient</i>. Para obter mais informações, consulte <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3335 </td> 
   <td colname="col2"><span class="codeph"> AXS_InvalidDRMVersion </span> </td> 
   <td colname="col3"> Atualize para a versão mais recente do TVSDK para Android. <p>Para resolver esse problema, conclua uma das seguintes tarefas: 
     <ul id="ul_BF1742948BC9461CB8686DE70124D3CD"> 
      <li id="li_690D440C94CC45A0AE55EC319B1C4C23">Atualizar o AIR </li> 
      <li id="li_CDD20251C881466E88BE7BBB53D61EBC">No Flash Player, atualize o módulo AdobeCP e tente reproduzir novamente. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3336 </td> 
   <td colname="col2"><span class="codeph"> AXS_InvalidRuntimePlatform </span> </td> 
   <td colname="col3"> <p>Essa plataforma não tem permissão para reproduzir o conteúdo porque, por exemplo, o provedor de conteúdo configurou o Access para negar conteúdo ao FP/AIR em uma plataforma. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3337 </td> 
   <td colname="col2"><span class="codeph"> AXS_InvalidRuntimeVersion </span> </td> 
   <td colname="col3"> Atualize para a versão mais recente do TVSDK para Android. <p>Isso ocorre se o conteúdo ou o servidor estiver configurado para negar a reprodução para uma versão específica dos tempos de execução do Flash ou do AIR. </p> 
    <ul id="ul_B0732D941256483CABBDD30C9BF43249"> 
     <li id="li_72782B1D638F48C0B87084689FB9C798">Se o usuário estiver em um sistema operacional no qual o Flash possa ser atualizado, o software do distribuidor deverá solicitar que o usuário atualize o Flash e tentar novamente. Caso contrário, aconselhe o usuário a usar uma máquina diferente. </li> 
     <li id="li_1E3FD93CE39E43F2B7D961299B1211DA">Se houver suspeita do erro 3337s, identifique se ele está ocorrendo para um conteúdo específico e reempacote-o. Se o conteúdo for empacotado corretamente, consulte Diagnóstico de discrepâncias de política/licença </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3338 </td> 
   <td colname="col2"><span class="codeph"> AXS_UnknownConnectionType </span> </td> 
   <td colname="col3"> <p>Não é possível detectar o tipo de conexão, e a política requer que você ative a Proteção de Saída. Esse problema é esperado somente se o conteúdo for empacotado para exigir proteção de saída digital ou analógica. </p> <p>Ocasionalmente, ocorria um problema nas versões do Flash Player anteriores à versão 11.8.800.168, causava o erro 3338 no conteúdo para o qual a política indicava que a proteção de conteúdo é <span class="codeph"> USAR SE DISPONÍVEL</span>. Este problema foi corrigido na versão 11.8.800.168 e posterior. </p> 
    <ul id="ul_4B6CA26A53F84838B5B95400925464D4"> 
     <li id="li_CBD890F467E449EBB5116E1561252058">O software do distribuidor seleciona uma variante do conteúdo que não requer proteção de saída (por exemplo, variante SD de um fluxo HD). <p>Se o erro 3338 estiver ocorrendo em <span class="codeph"> USE_IF_AVAILABLE </span> conteúdo, verifique o número da versão do player. Se a versão do reprodutor for anterior a 11.8.800.168, aconselhe o usuário a atualizar o Flash Player. Se o erro 3338 estiver ocorrendo em versões acima de 11.8.800.168, registre qual conteúdo causou o erro. </p> </li> 
     <li id="li_62886C1D96264B129928A7E29E6C70E1">O distribuidor deve verificar qual conteúdo está causando esse erro e validar se a política do conteúdo está sendo definida <span class="codeph"> NO_PROTECTION</span> ou <span class="codeph"> USE_IF_AVAILABLE</span> para saídas analógicas e digitais. <p>Se o conteúdo for empacotado inadvertidamente com <span class="codeph"> NO_OUTPUT</span> ou <span class="codeph"> OBRIGATÓRIO</span>, reempacotar o conteúdo. Se o conteúdo for empacotado corretamente, consulte Diagnóstico de discrepâncias de política/licença. Caso contrário, encaminhe para Adobe. </p> </li> 
    </ul> <p>Para obter mais informações, consulte <a href="https://forums.adobe.com/message/5518688" format="https" scope="external"> Obtendo erros 3338 inesperados quando sua política DRM está definida como USE_IF_AVAILABLE?</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3339 </td> 
   <td colname="col2"><span class="codeph"> AAXS_SemReproduçãoAnalógicaPermitida </span> </td> 
   <td colname="col3"> Não é possível reproduzir no dispositivo analógico. Para resolver o problema, conecte um dispositivo digital. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3340 </td> 
   <td colname="col2"><span class="codeph"> AXS_NoAnalogProtectionAvail </span> </td> 
   <td colname="col3"> Não é possível reproduzir o conteúdo porque o dispositivo de vídeo externo analógico conectado (monitor/TV) não tem os recursos corretos (por exemplo, o dispositivo não tem Macrovision ou ACP). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3341 </td> 
   <td colname="col2"><span class="codeph"> AXS_NoDigitalPlaybackAllowed </span> </td> 
   <td colname="col3"> Não é possível reproduzir o conteúdo em um dispositivo digital. <p>Importante: esse problema não deve ocorrer em um ambiente de produção, pois os editores de conteúdo não devem proibir a reprodução digital. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3342 </td> 
   <td colname="col2"><span class="codeph"> AXS_NoDigitalProtectionAvail </span> </td> 
   <td colname="col3"> O dispositivo de vídeo externo digital conectado (monitor/TV) não tem os recursos corretos. Por exemplo, o dispositivo não tem HDCP. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3343 </td> 
   <td colname="col2"><span class="codeph"> AXS_IntegrityVerificationFailed </span> </td> 
   <td colname="col3"> <p>Não aplicável para Android. </p> <p>Este erro é conhecido inicialmente após o lançamento de uma nova versão do Flash. Isso ocorre porque o Flash foi atualizado enquanto o Flash estava aberto, o que coloca o Flash em um estado incorreto até que o navegador seja reiniciado. </p> 
    <ul id="ul_A0AC4A77550E40409A04BD33748EA987"> 
     <li id="li_F41C1ABD838D41ABB0DF65093E664A29">O software do distribuidor deve executar as seguintes tarefas: 
      <ul id="ul_79B2AB1372074D448F129851AA24F985"> 
       <li id="li_B93EDD263D78434FAF198A01938D3508">Recomende que o usuário feche ou encerre todos os navegadores e, em seguida, reabra. </li> 
       <li id="li_ADFBCFA66AD849E18DB390455458528E">Verifique se a versão do Flash é atual. <p>Se a versão não for a atual, aconselhe o cliente a atualizar, feche todas as guias no navegador e reabra. </p> </li> 
      </ul> </li> 
     <li id="li_281B54582B5949AEA7D166246917EE41">Se o erro parecer ocorrer após uma reinicialização bem-sucedida do navegador, encaminhe para Adobe. <p>Quando uma nova versão é lançada, recomendamos que você entre em contato com o Suporte do Adobe para ver se o problema de atualizações em segundo plano foi corrigido. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3344 </td> 
   <td colname="col2"><span class="codeph"> AXS_MissingAdobeCPModule </span> </td> 
   <td colname="col3"> Não aplicável para Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3345 </td> 
   <td colname="col2"><span class="codeph"> AXS_DRMNoAccessError </span> </td> 
   <td colname="col3"> <p>Não aplicável para Android. </p> <p>Esse erro ocorre quando parte do Flash ou do AIR não foi instalada corretamente. </p> <p>O software do distribuidor deve executar um dos seguintes procedimentos: 
     <ul id="ul_D1188E2D4FDF4BD89A04F5629D75D981"> 
      <li id="li_B33FBCA5D4534D668B86A5E93DB3A809">Peça ao usuário para desinstalar e reinstalar o AIR. </li> 
      <li id="li_B7D2388E9FA84C26AF1C87B48AF9EF16">Para o Flash Player, chame <span class="codeph"> Atualização.sistema</span>. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3346 </td> 
   <td colname="col2"><span class="codeph"> AXS_MigrationFailed </span> </td> 
   <td colname="col3"> 
    <ul id="ul_518AD4931CC64EB3A962DD451E6C5067"> 
     <li id="li_3C44F0740B08490E9C62D89C40B57DC2">O software do distribuidor deve executar um dos seguintes procedimentos: 
      <ul id="ul_7D90526684BF4EB2BBADCF598AA13086"> 
       <li id="li_D15B4BEDAF7340F6B9BC886DF6E346EC">Se for AIR, chame <span class="codeph"> DRMManager.resetDRMVouchers()</span> </li> 
       <li id="li_40A51D35408249CFA28DBC49FDA3408B">Se o Flash tiver sido inutilizado devido ao código de erro 3322 ou 3346, os usuários deverão acessar <a href="https://forums.adobe.com/message/5535907#5535907" format="http" scope="external"> https://forums.adobe.com/message/5535907#5535907</a> e siga as instruções do artigo do Adobe para redefinir programaticamente a loja de licenças DRM. </li> 
      </ul> </li> 
     <li id="li_0464471E4A094C80BF2986694341921A">Se esse erro ocorrer com frequência, o distribuidor deverá fornecer os detalhes sobre a versão do reprodutor de frequência e a versão do navegador para o Adobe. </li> 
    </ul> <p>Para obter mais informações, consulte os seguintes artigos do fórum: 
     <ul id="ul_44E0077FEAA749CC9549BF3846065304"> 
      <li id="li_2BE3B2443380415DA73B7AA3B6547B31"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Erro de DRM 3322/3346/3368 no Chrome (problemas na barra de informações)</a> </li> 
      <li id="li_4E5C7414756644E1AB78BE7B8112228C"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> Erro 3322 ou 3346 após alteração de hardware</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3347 </td> 
   <td colname="col2"><span class="codeph"> AXS_RecursosInsuficientesDeDispositivo </span> </td> 
   <td colname="col3"> <p>O principal significado desse erro é que a licença tem uma restrição que o certificado DRM dos clientes indica que não pode atender. Os seguintes "recursos de hardware" são definidos quando o certificado DRM dos clientes é emitido: 
     <ul id="ul_1EB6F1469C244CF0BA52C212495C053D"> 
      <li id="li_646043CE045C4DE2BBC939E1F4963DFE"><b>Barramento acessível não-usuário</b>. Se <b>true</b>, a mídia descriptografada nunca flui através de um barramento ou para a memória principal, onde um aplicativo pode acessá-la. <p>Se <b>false</b>, o conteúdo pode estar acessível ao aplicativo após a descriptografia. </p> </li> 
      <li id="li_02AAECAF4D35447BA10554541B46DE67"><b>Raiz de confiança do hardware</b>. Se <b>true</b>, todos os softwares carregados no momento da inicialização no dispositivo foram validados em relação a uma chave ou resumo que só está disponível no hardware. <p>Ambas as restrições são verificadas no lado do cliente quando a licença é aberta em relação ao certificado DRM para o cliente e a falha é imediata. Essas restrições também podem ser verificadas no lado do servidor antes da emissão da licença. </p> </li> 
     </ul> </p> <p>O significado secundário desse erro é que a licença tem a política "Imposição de Jailbreak" definida e uma jailbreak foi detectada no dispositivo. Essa verificação é feita periodicamente no lado do cliente e não pode ser verificada no lado do servidor. </p> <p>Os distribuidores podem atualizar as políticas e remover as restrições. Para políticas de recursos do dispositivo, execute o comando de atualização de política com o <span class="codeph"> -devCapabilitiesV1</span> sinalizador e nenhum argumento. Para imposição de jailbreak, defina <span class="codeph"> policy.forceJailbreak=false</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3348 </td> 
   <td colname="col2"><span class="codeph"> AXS_HardStopIntervalExpired </span> </td> 
   <td colname="col3"> O intervalo de parada permanente expirou. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3349 </td> 
   <td colname="col2"><span class="codeph"> AXS_ServerVersionTooHigh </span> </td> 
   <td colname="col3"> O servidor está sendo executado em uma versão que é superior à versão mais recente suportada pelo cliente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3350 </td> 
   <td colname="col2"><span class="codeph"> AXS_ServerVersionTooLow </span> </td> 
   <td colname="col3"> O servidor está sendo executado em uma versão inferior à versão mínima que é suportada pelo cliente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3351 </td> 
   <td colname="col2"><span class="codeph"> AXS_DomainTokenInvalid </span> </td> 
   <td colname="col3"> O token de domínio era inválido. Para resolver esse problema, registre-se no domínio novamente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3352 </td> 
   <td colname="col2"><span class="codeph"> AXS_DomainTokenTooOld </span> </td> 
   <td colname="col3"> O token de domínio é mais antigo que o token exigido pela licença. Para resolver o problema, registre-se no domínio novamente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3353 </td> 
   <td colname="col2"><span class="codeph"> AXS_DomainTokenTooNew </span> </td> 
   <td colname="col3"> O token de domínio é mais recente do que o token exigido pela licença. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3354 </td> 
   <td colname="col2"><span class="codeph"> AXS_DomainTokenExpired </span> </td> 
   <td colname="col3"> O token de domínio expirou. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3355 </td> 
   <td colname="col2"><span class="codeph"> AXS_DomainJoinFailed </span> </td> 
   <td colname="col3"> Falha ao ingressar no domínio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3356 </td> 
   <td colname="col2"><span class="codeph"> AXS_NoCorrespondingRoot </span> </td> 
   <td colname="col3"> Uma licença raiz para uma licença folha V3 não foi encontrada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3357 </td> 
   <td colname="col2"><span class="codeph"> AXS_NoValidEmbeddedLicense </span> </td> 
   <td colname="col3"> Nenhuma licença incorporada válida foi encontrada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3358 </td> 
   <td colname="col2"><span class="codeph"> AXS_NoACPProtectionAvail </span> </td> 
   <td colname="col3"> Não é possível reproduzir porque o dispositivo analógico conectado não tem proteção de ACP. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3359 </td> 
   <td colname="col2"><span class="codeph"> AXS_NoCGMSAProtectionAvail </span> </td> 
   <td colname="col3"> Não é possível reproduzir porque o dispositivo analógico conectado não tem proteção CGMS-A. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3360 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainRegistrationRequired </span> </td> 
   <td colname="col3"> O conteúdo requer registro de domínio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3361 </td> 
   <td colname="col2"><span class="codeph"> AXS_NotRegisteredToDomain </span> </td> 
   <td colname="col3"> O computador não está registrado no domínio para os metadados especificados. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3362 </td> 
   <td colname="col2"><span class="codeph"> AXS_OperationTimeoutError </span> </td> 
   <td colname="col3"> A operação assíncrona demorou mais de <span class="codeph"> maxOperationTimeout</span>. Retornado somente pelo iOS DRMNative Framework. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3363 </td> 
   <td colname="col2"><span class="codeph"> AXS_UnsupportedIOSPlaylistError </span> </td> 
   <td colname="col3"> A lista de reprodução M3U8 enviada tinha conteúdo não compatível. Retornado somente pelo iOS DRMNative Framework. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3364 </td> 
   <td colname="col2"><span class="codeph"> AXS_NoDeviceId </span> </td> 
   <td colname="col3"> <p>A estrutura solicitou a ID do dispositivo, mas o valor retornado estava vazio. </p> <p>O usuário não deve selecionar o <span class="uicontrol"> Permitir identificadores para conteúdo protegido</span> nas configurações do Chrome. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3365 </td> 
   <td colname="col2"><span class="codeph"> AXS_IncógnitoModeNotAllowed </span> </td> 
   <td colname="col3"> <p>Essa combinação de navegador/plataforma não permite a reprodução protegida por DRM no modo Incógnito. </p> <p>O software do distribuidor deve avisar o usuário para sair do modo Incógnito ou usar um navegador diferente. Para obter mais informações, consulte <a href="https://forums.adobe.com/thread/1266622" format="https" scope="external"> Causa e resolução do erro DRM 3365</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3366 </td> 
   <td colname="col2"><span class="codeph"> AXS_BadParameter </span> </td> 
   <td colname="col3"> <p>O tempo de execução do host chamou a biblioteca de Acesso com um parâmetro incorreto. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3367 </td> 
   <td colname="col2"><span class="codeph"> AXS_BadSignature </span> </td> 
   <td colname="col3"> Falha na assinatura do manifesto m3u8. Retornado somente pelo iOS DRMNative Framework ou AVE. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3368 </td> 
   <td colname="col2"><span class="codeph"> AXS_UserSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>O usuário cancelou a operação ou inseriu configurações que não permitem acesso ao sistema. </p> <p>Esse erro só é lançado quando a versão do SWF é 19 ou posterior. Para compatibilidade com versões anteriores, 3321 é lançado quando o SWF é versão 18 ou anterior. </p> <p>O software do distribuidor deve orientar o usuário para uma explicação de como permitir o acesso a plug-ins fora da área restrita. Acesso à unsandbox do Google Chrome negado</a> e <a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Erro de DRM 3322/3346/3368 no Chrome (problemas na barra de informações)</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3369 </td> 
   <td colname="col2"><span class="codeph"> AXS_InterfaceNotAvailable</span> </td> 
   <td colname="col3"> <p>Uma interface de navegador necessária não está disponível. Esse problema ocorre somente no Pepper. Pode haver uma incompatibilidade entre o plug-in do Flash e a versão do navegador. </p> <p>O software do distribuidor deve orientar o usuário para garantir que ele tenha a versão mais recente do navegador instalada. </p> <p> Se as incidências desse erro estiverem aumentando e corresponderem a uma atualização do navegador sendo lançada, encaminhar para Adobe. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3370 </td> 
   <td colname="col2"><span class="codeph"> AXS_ContentIdSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>O usuário desativou o <span class="uicontrol"> Permitir identificadores para conteúdo protegido</span> configuração. </p> <p>Dica: este erro apareceu com as versões Pepper 13.0.0.x ou superior. </p> <p>O software do distribuidor deve orientar o usuário a habilitar o <span class="uicontrol"> Permitir identificadores para conteúdo protegido</span> configuração. </p> <p>A equipe de operações do distribuidor deve orientar o usuário para habilitar o <span class="uicontrol"> Permitir identificadores para conteúdo protegido</span> configuração. </p> <p>Para obter mais informações, consulte <a href="https://forums.adobe.com/message/6518323#6518323" format="https" scope="external"> https://forums.adobe.com/message/6518323#6518323</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3371 </td> 
   <td colname="col2"><span class="codeph"> AXS_SemOPConstraintInPixel</span><span class="codeph"> Restrições</span> </td> 
   <td colname="col3"> <p>Resolução malformada com base nas restrições de proteção de saída da licença. </p> <p>O software do distribuidor deve exibir uma mensagem de erro. Peça ao usuário para relatar o problema ao distribuidor com um título de conteúdo. </p> <p>O distribuidor deve reempacotar o conteúdo com uma política válida. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3372 </td> 
   <td colname="col2"><span class="codeph"> ResoluçãoMaiorQueResoluçãoMáxAXS</span> </td> 
   <td colname="col3"> <p>A resolução do conteúdo é maior que a resolução máxima especificada na restrição de proteção de saída. </p> <p>Se a equipe de operações do distribuidor vir esse erro em seus registros, ela deverá revisar a política de proteção de saída com base em resolução e, se necessário, reempacotar o conteúdo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3373 </td> 
   <td colname="col2"><span class="codeph"> AXS_MenorErro_ResoluçãoExibiçãoMaiorQueRestrição</span> </td> 
   <td colname="col3"> <p>A resolução do conteúdo é maior que a resolução especificada pela restrição de proteção de saída ativa no momento. </p> <p>Se a equipe de operações do distribuidor vir esse erro em seus registros, ela deverá revisar a política de proteção de saída com base em resolução e, se necessário, reempacotar o conteúdo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3374 </td> 
   <td colname="col2"><span class="codeph"> AXS_MinorErr_ClientCommProcessFailed</span> </td> 
   <td colname="col3"> <p>Falha durante o processamento de comunicação do lado do cliente, por exemplo, geração de solicitação, processamento de resposta, token de autenticação incorreto e assim por diante. </p> <p>Se a equipe de operações do distribuidor vir esse erro em seus registros, ela deverá revisar a política de proteção de saída com base em resolução e, se necessário, reempacotar o conteúdo. </p> </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: valores de reprodução de vídeo {#section_7079501250C2487499639F92EC774525}

A interface do Codificador de vídeo do AVE retorna essas notificações de reprodução de vídeo no `NATIVE_ERROR` objeto de metadados.

<table id="table_5EEB1F60E5854452A8B0BABBE9B32651"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Valor da chave de metadados NATIVE_ERROR_CODE</b></th> 
   <th colname="col2" class="entry"><b>Valor para a chave de metadados NATIVE_ERROR_NAME</b></th> 
   <th colname="col3" class="entry"><b>Descrição</b></th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> -1 </td> 
   <td colname="col2"><span class="codeph"> END_OF_PERIOD</span> </td> 
   <td colname="col3"> Fim do período. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> SUCESSO</span> </td> 
   <td colname="col3"> Operação bem-sucedida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> Operação assíncrona. A solicitação de operação foi feita. As informações de sucesso/falha estarão disponíveis posteriormente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> Operação não possível devido à condição de fim de arquivo (EOF). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> DECODIFICADOR_FALHA</span> </td> 
   <td colname="col3"> Falha do decodificador no tempo de execução. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> DEVICE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Falha ao abrir o decodificador de hardware. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> ARQUIVO_NÃO_ENCONTRADO </span> </td> 
   <td colname="col3"> O recurso não pode ser localizado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> GENERIC_ERROR </span> </td> 
   <td colname="col3"> Erro genérico. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> IRRECUPERÁVEL_ERRO </span> </td> 
   <td colname="col3"> Uma condição de erro da qual o mecanismo de vídeo não pode se recuperar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERABLE </span> </td> 
   <td colname="col3"> Erro de rede, tentando recuperar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> NO_FIXED_SIZE </span> </td> 
   <td colname="col3"> Não é possível determinar o tamanho do recurso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10 </td> 
   <td colname="col2"><span class="codeph"> NOT_IMPLEMENTED </span> </td> 
   <td colname="col3"> Recurso não implementado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11 </td> 
   <td colname="col2"><span class="codeph"> SEM_MEMÓRIA </span> </td> 
   <td colname="col3"> Sem memória. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR </span> </td> 
   <td colname="col3"> Erro ao analisar o arquivo de mídia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13 </td> 
   <td colname="col2"><span class="codeph"> TAMANHO_DESCONHECIDO </span> </td> 
   <td colname="col3"> O recurso tem um tamanho, mas ele é desconhecido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14 </td> 
   <td colname="col2"><span class="codeph"> UNDER_FLOW </span> </td> 
   <td colname="col3"> Condição de estouro negativo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_CONFIG </span> </td> 
   <td colname="col3"> A configuração não é compatível. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_OPERATION </span> </td> 
   <td colname="col3"> A operação não é aceita. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17 </td> 
   <td colname="col2"><span class="codeph"> WAITING_FOR_INIT </span> </td> 
   <td colname="col3"> Ainda não inicializado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18 </td> 
   <td colname="col2"><span class="codeph"> INVALID_PARAMETER </span> </td> 
   <td colname="col3"> Parâmetro inválido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 19 </td> 
   <td colname="col2"><span class="codeph"> INVALID_OPERATION</span> </td> 
   <td colname="col3"> Operação não permitida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 20 </td> 
   <td colname="col2"><span class="codeph"> OP_ONLY_ALLOWED_IN_PAUSED_STATE</span> </td> 
   <td colname="col3"> A operação é permitida somente enquanto está pausada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21 </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> A operação não pode ser usada em arquivos somente de áudio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22 </td> 
   <td colname="col2"><span class="codeph"> PREVIOUS_STEP_SEEK_IN_PROGRESS</span> </td> 
   <td colname="col3"> A operação de busca anterior ainda está em andamento. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23 </td> 
   <td colname="col2"><span class="codeph"> SOURCE_NOT_SPECIFIED </span> </td> 
   <td colname="col3"> Recurso não especificado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24 </td> 
   <td colname="col2"><span class="codeph"> RANGE_ERROR</span> </td> 
   <td colname="col3"> O valor especificado está fora do intervalo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25 </td> 
   <td colname="col2"><span class="codeph"> INVALID_SEEK_TIME</span> </td> 
   <td colname="col3"> Tempo de busca inválido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26 </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> O arquivo especificado não está em conformidade com a sintaxe esperada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27 </td> 
   <td colname="col2"><span class="codeph"> COMPONENT_CREATION_FAILURE</span> </td> 
   <td colname="col3"> Não foi possível criar um componente essencial. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28 </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> Falha ao criar o contexto de DRM. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29 </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORTED </span> </td> 
   <td colname="col3"> O tipo de contêiner não é suportado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30 </td> 
   <td colname="col2"><span class="codeph"> SEEK_FAILED</span> </td> 
   <td colname="col3"> Falha na busca. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31 </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Codec sem suporte. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32 </td> 
   <td colname="col2"><span class="codeph"> REDE_INDISPONÍVEL</span> </td> 
   <td colname="col3"> Rede não disponível. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_ERROR</span> </td> 
   <td colname="col3"> Erro ao obter dados da rede. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34 </td> 
   <td colname="col2"><span class="codeph"> ESTOURO</span> </td> 
   <td colname="col3"> Estouro. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35 </td> 
   <td colname="col2"><span class="codeph"> VIDEO_PROFILE_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Perfil de vídeo não suportado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_NOT_LOADED</span> </td> 
   <td colname="col3"> Tentativa de operação em um período SUSPENSO ou em um período que ainda não foi carregado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37 </td> 
   <td colname="col2"><span class="codeph"> INVALID_REPLACE_DURATION</span> </td> 
   <td colname="col3"> A duração de substituição especificada é inválida ou se estende além do final do fluxo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38 </td> 
   <td colname="col2"><span class="codeph"> CALLED_FROM_WRONG_THREAD</span> </td> 
   <td colname="col3"> A API não pode ser chamada do thread errado. Geralmente, para elementos de API que devem ser chamados somente a partir do thread principal. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39 </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> Erro de leitura do fragmento. Nenhum failover presente. O mecanismo tentará ler o próximo fragmento. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40 </td> 
   <td colname="col2"><span class="codeph"> ANULADO</span> </td> 
   <td colname="col3"> A operação foi anulada por uma chamada explícita de Anular ou Destruir. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_HLS_VERSION</span> </td> 
   <td colname="col3"> Não é possível reproduzir esta versão da mídia HLS. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> Não é possível fazer failover. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43 </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> O download de HTTP atingiu o tempo limite. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_DOWN </span> </td> 
   <td colname="col3"> A conexão de rede do usuário está inoperante. A reprodução pode parar a qualquer momento e será retomada quando a conexão estiver disponível. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45 </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> Nenhum perfil de taxa de bits utilizável encontrado no fluxo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46 </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> O manifesto tem uma assinatura incorreta. Falha no teste de assinatura de manifesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_LOAD_PLAYLIST</span> </td> 
   <td colname="col3"> Não é possível carregar uma lista de reprodução. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48 </td> 
   <td colname="col2"><span class="codeph"> REPLACEMENT_FAILED</span> </td> 
   <td colname="col3"> A substituição especificada em uma API de Inserção não teve êxito. Isso significa que a inserção foi bem-sucedida, mas a substituição não. A substituição poderá falhar se o manifesto que será substituído tiver sido removido da linha do tempo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49 </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_ASYMMETRIC_PROFILE</span> </td> 
   <td colname="col3"> O DRM está alternando para um perfil assimétrico. Espera-se que todos os perfis estejam alinhados em duração. Caso contrário, esse aviso será exibido e poderá haver saltos na reprodução. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_BACKWARD</span> </td> 
   <td colname="col3"> Espera-se que a janela ativa avance somente. Caso contrário, esse aviso será exibido e a janela não será lida. Por causa disso, pode haver saltos (ou parada/pausa longa) na reprodução. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51 </td> 
   <td colname="col2"><span class="codeph"> CURRENT_PERIOD_EXPIRED</span> </td> 
   <td colname="col3"> A janela em tempo real foi movida para além do período atual. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52 </td> 
   <td colname="col2"><span class="codeph"> CONTENT_LENGTH_MISMATCH</span> </td> 
   <td colname="col3"> O comprimento do conteúdo relatado pelo servidor HTTP não correspondia ao tamanho real da mídia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_HOLD</span> </td> 
   <td colname="col3"> O leitor de mídia não pode ler mais porque atingiu o tempo definido pela API setHoldAt. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> LIVE_HOLD </span> </td> 
   <td colname="col3">O leitor de mídia não pode carregar segmentos porque atingiu o fim da janela ativa. O carregamento do segmento será retomado quando o servidor adicionar nova mídia à janela ativa. Normalmente, esse estado é atingido se: 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48">A variável <span class="codeph"> bufferTime</span> é muito alto (igual ou maior que a duração da janela ativa). </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">Uma combinação de uma ou mais APIs de inserção/exclusão substituiu mais mídia do que foi adicionada. </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">O próximo período é um período em tempo real com uma substituição de mídia pendente (devido à chamada da API InsertBy ) </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEAVING </span> </td> 
   <td colname="col3"> O intercalamento de áudio e vídeo na mídia não é feito corretamente. Este é um erro de empacotamento. O aviso é despachado quando a diferença excede dois segundos. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56 </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57 </td> 
   <td colname="col2"><span class="codeph"> PLAYBACK_NOT_AUTHORIZED</span> </td> 
   <td colname="col3"> A reprodução HLS não foi habilitada no Flash Player. Consulte AuthorizedFeatures.enableHLSPlayback. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> O decodificador recebeu uma amostra inválida que não pode ser decodificada. Geralmente, esse não é um erro fatal, mas indica que pode haver falhas no áudio/vídeo. Muitas instâncias desse erro indicam uma codificação incorreta ou um arquivo inválido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> Depois que a reprodução começar, o intervalo Inserir/Substituir não deve conter o indicador de leitura. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60 </td> 
   <td colname="col2"><span class="codeph"> POSTROLL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> Inserções pós-rolagem não são permitidas em uma mídia em tempo real. No entanto, elas são permitidas depois que o servidor marca a mídia como concluída. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> ERRO_INTERNO</span> </td> 
   <td colname="col3"> Uma questão muito rara que nunca deve acontecer. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62 </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> O fluxo não segue a recomendação de empacotamento de sempre colocar H264 SPS/PPS em um AVCC. Problemas de busca/reprodução podem ser vistos. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63 </td> 
   <td colname="col2"><span class="codeph"> PARTIAL_REPLACEMENT</span> </td> 
   <td colname="col3"> A substituição especificada em uma API de Inserção foi feita apenas parcialmente. Isso acontece quando replaceDuration ultrapassa a duração da linha do tempo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64 </td> 
   <td colname="col2"><span class="codeph"> REPRESENTAÇÃO_M3U8_ERRO</span> </td> 
   <td colname="col3"> Erro ao carregar a lista de reprodução de representação. Isso é apenas para o AVE, não para o FlashPlayer. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65 </td> 
   <td colname="col2"><span class="codeph"> NULL_OPERATION</span> </td> 
   <td colname="col3"> A operação não faz nada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66 </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SKIPPED_ON_FAILURE</span> </td> 
   <td colname="col3"> O segmento não pode ser reproduzido e é ignorado na falha. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67 </td> 
   <td colname="col2"><span class="codeph"> INCOMPATIBLE_RENDER_MODE</span> </td> 
   <td colname="col3"> Modo de processamento incompatível. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68 </td> 
   <td colname="col2"><span class="codeph"> PROTOCOLO_NÃO_SUPORTADO </span> </td> 
   <td colname="col3"> O protocolo da Web usado no URL não é compatível. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPATIBLE_VERSION</span> </td> 
   <td colname="col3"> Erro ao analisar o arquivo de mídia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70 </td> 
   <td colname="col2"><span class="codeph"> MANIFEST_FILE_UNEXPECTEDLY_CHANGED</span> </td> 
   <td colname="col3"> O arquivo de manifesto foi alterado de uma maneira inesperada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> Não é possível executar uma operação de divisão em uma linha do tempo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> Não é possível executar uma operação de apagar em uma linha do tempo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73 </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_GET_NEXT_FRAGMENT</span> </td> 
   <td colname="col3"> Não obteve o próximo fragmento. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74 </td> 
   <td colname="col2"><span class="codeph"> NO_TIMELINE</span> </td> 
   <td colname="col3"> Nenhuma linha do tempo presente em uma estrutura de dados interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> LISTENER_NOT_FOUND</span> </td> 
   <td colname="col3"> Nenhum ouvinte encontrado em uma estrutura de dados interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> Não é possível iniciar o áudio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77 </td> 
   <td colname="col2"><span class="codeph"> NO_AUDIO_SINK</span> </td> 
   <td colname="col3"> Nenhum coletor de áudio presente em uma estrutura de dados interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78 </td> 
   <td colname="col2"><span class="codeph"> FILE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Não é possível abrir o arquivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79 </td> 
   <td colname="col2"><span class="codeph"> FILE_WRITE_ERROR</span> </td> 
   <td colname="col3"> Não é possível gravar em um arquivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80 </td> 
   <td colname="col2"><span class="codeph"> FILE_READ_ERROR</span> </td> 
   <td colname="col3"> Não é possível ler de um arquivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81 </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> Ocorreu um erro ao analisar dados de ID3. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> SECURITY_ERROR </span> </td> 
   <td colname="col3"> Falha ao carregar o conteúdo devido a restrições de segurança. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> LINHA DO TEMPO_MUITO_CURTA</span> </td> 
   <td colname="col3"> A duração da linha do tempo é muito curta. Se for um stream ao vivo, buffering frequente pode ocorrer. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> O fluxo foi alternado para um fluxo somente de áudio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> O fluxo foi alternado de somente áudio para um fluxo com vídeo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> CHAVE_NÃO_ENCONTRADA </span> </td> 
   <td colname="col3"> A chave não pode ser encontrada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> INVALID_KEY</span> </td> 
   <td colname="col3"> A chave é inválida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 89 </td> 
   <td colname="col2"> <span class="codeph"> KEY_SERVER_NOT_FOUND</span> </td> 
   <td colname="col3"> O servidor de chaves não retorna uma chave. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 90 </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> Não é possível manipular a atualização do manifesto principal. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91 </td> 
   <td colname="col2"> <span class="codeph"> UNREPORTED_TIME_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> Descontinuidade de tempo não relatado (PTS) encontrada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 92 </td> 
   <td colname="col2"> <span class="codeph"> UNMATCHED_AV_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> Descontinuidade de Áudio e Vídeo sem Correspondência encontrada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 93 </td> 
   <td colname="col2"><span class="codeph"> TRICKPLAY_ENDED_DUE_TO_ERROR</span> </td> 
   <td colname="col3">Ocorreu um erro ao reproduzir a mídia no <i>jogo de truque</i> modo. O modo de reprodução de truques é encerrado e o fluxo é pausado. Chame <span class="codeph"> Play()</span> para reproduzir a mídia no modo normal. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 95 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_AHEAD</span> </td> 
   <td colname="col3"> O reprodutor está fora da janela ativa e deve ir em frente para alcançar o nível desejado. </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: valores de criptografia {#section_39365E545CAC49B9A4D4678657BB2155}

O módulo de criptografia do mecanismo de vídeo Adobe retorna essas notificações no campo `NATIVE_ERROR` objeto de metadados.

| **Valor da chave de metadados NATIVE_ERROR_CODE** | **Valor para a chave de metadados NATIVE_ERROR_NAME** | **Significado** |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | Não há suporte para o algoritmo que está sendo usado. |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | Os dados estão corrompidos. |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | Buffer muito pequeno. |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | Certificado inválido. |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | Atualização do resumo. |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | Término do resumo. |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | Parâmetro inválido. |
