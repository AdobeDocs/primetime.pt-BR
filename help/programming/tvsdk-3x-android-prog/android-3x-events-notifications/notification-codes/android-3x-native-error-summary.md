---
title: Detalhes da notificação NATIVE_ERROR
description: Detalhes da notificação NATIVE_ERROR
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '6888'
ht-degree: 2%

---


# Detalhes para a notificação NATIVE_ERROR {#details-for-the-native-error-notification}

Quando o TVSDK trata um erro nativo, ele retorna alguns ou todos os valores de chave de metadados a seguir como strings.

<table id="table_7F713B7A56024D8DA3C84E449D09CC91"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Nome da chave de metadados</b></th> 
   <th colname="col2" class="entry"><b>Valor dos metadados</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR_CODE</span> </td> 
   <td colname="col2"> <p>Código de erro nativo do AVE. </p> <p>Esses códigos representam o seguinte: 
     <ul id="ul_1F33D523DDFE4CE8B4F0DC279FF7E4F8"> 
      <li id="li_07A2D9BEE6364935A61EF3BD4AB6DE27">Erros de DRM (códigos 3300 a 3367). São os mesmos códigos de erro de Flash Player equivalentes </li> 
      <li id="li_433BA22DE3504AEEB623598BB4F939FA">Erros de reprodução de vídeo (-1 a 89) </li> 
      <li id="li_B347CB151DB94DE0A1DDEB1B33D2DABA">Erros de criptografia (300 a 307) </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR</span> </td> 
   <td colname="col2">Breve descrição da notificação (por exemplo, <span class="codeph"> AXS_InvalidVoucher</span> ou <span class="codeph"> DECODER_FAILED</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESCRIÇÃO</span> </td> 
   <td colname="col2"> Descrição longa da notificação (por exemplo, falha na operação de resolução de anúncios). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR_CODE</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.</span> PSDKErrorCodenumeric value como uma cadeia de caracteres (por exemplo, "13"). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.</span> PSDKErrorCodeas uma string (por exemplo,  <span class="codeph"> kECNetworkError</span>). </td> 
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
   <td colname="col2"> URL do servidor DRM ao qual o TVSDK tentou falar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Falha no carregamento do manifesto do anúncio</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_URL</span> </td> 
   <td colname="col2"> URL do conteúdo que falhou ao carregar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_TYPE</span> </td> 
   <td colname="col2">Tipo de anúncio (uma constante do enum <span class="codeph"> MediaResource.Type</span>). </td> 
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
   <td colname="col2"> Descrição do erro durante o download do arquivo manifest. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="col2">Descrição do erro durante o download do fragmento (por exemplo, <span class="codeph"> ts</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Erros de faixa de áudio</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_NAME</span> </td> 
   <td colname="col2"> Nome da faixa de áudio que falhou ao carregar, conforme especificado no manifesto. </td> 
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
   <td colname="col2"> <p>Posição (em milissegundos) desejada (dupla). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Diversos</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDITUDE_ERROR_CODE</span> </td> 
   <td colname="col2"> Código de erro do Auditude (número). </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: Valores de DRM {#section_D240082B93D34902A18C3923C1C717B3}

A interface do Video Encoder do mecanismo de vídeo Adobe retorna essas notificações de DRM no objeto de metadados `NATIVE_ERROR`.

Ao relatar erros de DRM ao Adobe, inclua `NATIVE_SUBERROR_CODE` e `DRM_ERROR_STRING` para obter assistência na solução de problemas.

>[!TIP]
>
>Esta lista fornece informações específicas do TVSDK sobre os erros. Para obter descrições completas, consulte [Referência de ActionScript de Erros de Tempo de Execução do ActionScript para o Adobe Flash Platform](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html#3300).

<table id="table_CD59A859865F4FFDBAA249C89C74770A"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Valor para a chave de metadados NATIVE_- ERROR_CODE</b></th> 
   <th colname="col2" class="entry"><b>Valor da chave de metadados NATIVE_ERROR_NAME</b></th> 
   <th colname="col3" class="entry"><b>Significado</b></th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 3300 </td> 
   <td colname="col2"><span class="codeph"> AXS_InvalidVoucher</span> </td> 
   <td colname="col3"> 
    <ul id="ul_516E4CB32D624B22892DDB9266CB04CA"> 
     <li id="li_348FC0F38B11417994119B61C9244076">O que o software do distribuidor deve fazer: 
      <ul id="ul_7AFD45CF92454BA4927783FAA628FBC4"> 
       <li id="li_0D9CCE61612643648C12DCDDD252E52A">Se você estiver usando o Google Chrome e estiver no modo Incógnito, e sua versão do Flash Player for inferior a 11.6, esse erro poderá ocorrer. <p>Recomendamos que o reprodutor verifique o número de versão do navegador e aconselhe o usuário a sair do modo Incógnito. </p> </li> 
       <li id="li_1DC6B755BD0840D48BEC92568FD330BA">Solicite a licença novamente. <p>Se a solicitação for bem-sucedida, você não precisará registrar ou escalonar. Se a solicitação não for bem-sucedida, registre o conteúdo que causou o erro. <span class="codeph"> </span> subErrorIdentified contém um erro de linha, se presente. </p> </li> 
      </ul> </li> 
     <li id="li_060B5D60C9BB419CBFA7B062FBCF2632">O que o distribuidor deve fazer: 
      <ul id="ul_FADB29DBF0DA4A0E8E54134AEB7DCD8A"> 
       <li id="li_FC5B1C04D21E4AECB0EBD9ADD3198504">Se as tentativas não forem bem-sucedidas em configurações diferentes do Chrome com Flash menor que a versão 11.6, pode ter ocorrido uma falha na embalagem. </li> 
       <li id="li_A720ECE591254021879B335B81B1F76D">Verifique se o problema é específico de determinados conteúdos e repacotes. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3301 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthenticationFailed</span> </td> 
   <td colname="col3"> <p>O servidor falhou ao autenticar ou autorizar o cliente. </p> 
    <ul id="ul_BE77AC1848FB4C09B6318359ACF1B8EE"> 
     <li id="li_6FB37D317D174E8488C5070D20CD241C">O software do distribuidor deve tomar as medidas necessárias para restabelecer as credenciais do usuário ou orientar o usuário a adquirir acesso ao conteúdo. </li> 
     <li id="li_BE071D59805B42D38E3E7650BC936417">O distribuidor deve confirmar que o mecanismo de autorização e autenticação do distribuidor está a funcionar corretamente. <p>Se os distribuidores não planejarem usar os recursos de autenticação ou autorização, deverão verificar se a política do conteúdo ofensivo requer autenticação e consultar Diagnosticando discrepâncias entre a política e a licença. </p> </li> 
    </ul> <p>Para obter mais informações sobre esse código de erro, consulte <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> Erro de DRM 3301 causas e resolução</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3302 </td> 
   <td colname="col2"><span class="codeph"> AAXS_RequireSSL</span> </td> 
   <td colname="col3"> <p>No Access 4.0 e superior, esse erro é lançado no iOS quando o URL da chave remota não usa HTTPS como esquema. HTTPS é necessário. </p> 
    <ul id="ul_3D47777BBCA14B67B107FBBE3E37E40C"> 
     <li id="li_7F7BBB27AE754CC39ABAAF9269739C49">Se o distribuidor estiver usando uma versão anterior ao Access v4, ou a versão pelo menos 4, mas a plataforma não for iOS, o software do distribuidor deverá registrar o erro. <p>O erro é lançado somente no iOS. </p> </li> 
     <li id="li_D83C427D2A0D47408F723EF7195070B6">Se o software do distribuidor for pelo menos o Adobe Access versão 4 e a plataforma for o iOS, os distribuidores devem alterar o URL do servidor de chaves remotas que estão usando para HTTPS. <p>Se estivessem usando apenas HTTP, os distribuidores talvez precisassem configurar um servidor HTTPS. Caso contrário, os distribuidores precisam enviar as informações registradas ao Adobe e escalonar o problema. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3303 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentExpirated</span> </td> 
   <td colname="col3"> <p>O conteúdo que você está visualizando expirou de acordo com as regras definidas pelo provedor de conteúdo. subErrorId contém um erro específico do cliente ou erro de linha. </p> <p> 
     <ul id="ul_1E4B3B8AE87A4E79997553BB2A0E52B9"> 
      <li id="li_EE3F2EEBF73743B9A38E4FCB7531E275">O software do distribuidor deve tentar adquirir novamente uma licença do servidor uma vez para determinar se uma nova licença não expirada está disponível. <p>Se nenhuma licença estiver disponível ou a licença tiver expirado, permita que o usuário adquira uma nova licença ou informe o usuário que o conteúdo não pode ser observado. Se o conteúdo tiver sido empacotado com uma política que tenha uma data de expiração/término expirada, os logs do servidor de licenças relatarão um <span class="codeph"> PolicyEvaluationException</span> e indicarão que a Data final da política terminou (Código de erro do servidor 303). Verifique os arquivos de log do servidor para verificar. </p> <p>Se possível, os clientes devem verificar a política que usaram durante a embalagem para ver se ela expirou. A ferramenta de linha de comando Java é: <code> java&nbsp;-jar&nbsp;libs/AdobePolicyManager.jar&nbsp;&nbsp;&nbsp;detail&nbsp;demo.pol</code> </p> </li> 
      <li id="li_50DBE680D8F04E7DA3E29C65A93188E7">O distribuidor deve confirmar se as datas de expiração da licença estão configuradas conforme pretendido. </li> 
     </ul> </p> <p>Para obter mais informações sobre esse código de erro, consulte <a href="https://forums.adobe.com/thread/1300813" format="https" scope="external"> 3303 (Conteúdo expirado) com AMS/FMS usando um Live Stream?</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3304 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthorizationFailed</span> </td> 
   <td colname="col3">Para obter mais informações sobre esse código de erro, consulte <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> Erro de DRM 3301 causas e resolução</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3305 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerConnectionFailed</span> </td> 
   <td colname="col3"> <p>A conexão com a licença ou os servidores de domínio excedeu o tempo limite, devido ao atraso da rede ou ao cliente estar offline. Normalmente, subErrorId contém código de retorno HTTP. </p> 
    <ul id="ul_938C7D8F07F64B4FA71A09DDF37E2E64"> 
     <li id="li_6648EA0049094E369BD9AE9CCA6B148D">O software do distribuidor deve tentar uma conexão de rede a um servidor em boas condições. <p>Se a tentativa falhar, peça ao usuário para se reconectar à rede. Se a tentativa for bem-sucedida, registre-a. </p> </li> 
     <li id="li_2ECA2C04BA08449DA3AD79A52EFAA229">O distribuidor deve verificar se todas as licenças e servidores de domínio em uso estão online e são visíveis na rede do cliente. </li> 
    </ul> <p>Para obter mais informações sobre esse código de erro, consulte <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> causas e resolução </a> DRM 3305 [ServerConnectionFailed]. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3306 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClientUpdateRequire</span> </td> 
   <td colname="col3"> Use uma versão mais recente do TVSDK para Android. <p>O cliente atual não pode concluir a ação solicitada, mas um cliente atualizado pode ser capaz de concluir a solicitação. </p> <p>Isso pode ter várias causas: 
     <ul id="ul_2EC4D42D5273439FA1AFDA1A2578B3D6"> 
      <li id="li_FCA926F5FAED4E7190BE855545AB6ACF">Foi usado um domínio compartilhado que não está disponível neste cliente. Esse é provavelmente o caso quando a reprodução funciona no Chrome, mas não em qualquer outro navegador e vice-versa. <p> <p>Dica: O Chrome usa uma chave PHDS/PHLS diferente da utilizada pelos outros navegadores. Para obter mais informações, consulte <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </p> </li> 
      <li id="li_3B633FB699234DCEA136E9BE3CC3386D">O aplicativo está tentando adicionar vários DRMSessions ao executar em uma versão do iOS anterior à versão 5.0. </li> 
      <li id="li_F7ED993AF0B941A7A27216B4D587A999">Os metadados têm uma versão de 3 ou superior quando há suporte somente para a versão 2. </li> 
     </ul> </p> 
     <ul id="ul_EE4AE6AD4F1745A5B5623E53B599DB62"> 
      <li id="li_7A83869D4262443DA35FA1DF8D3097DD">O software do distribuidor deve alertar o usuário e suspender a operação. <p>Se o software tiver uma maneira de determinar se uma atualização está disponível, direcione o usuário para essa atualização da maneira apropriada para a plataforma. </p> </li> 
      <li id="li_AF9C2711FDE54DA196EB9D2864632000">Se o problema ocorrer devido a um domínio compartilhado, o distribuidor precisará verificar no Adobe se há um tempo de execução ou uma biblioteca atualizada. <p>Para o tempo de execução do Flash, o distribuidor pode forçar a atualização diretamente em seu aplicativo. No caso de uma biblioteca, o distribuidor precisará obter uma biblioteca atualizada, reconstruir seu aplicativo e implantá-la aos usuários. </p> <p>Se o problema ocorrer devido a vários DRMSessions, o distribuidor precisará atualizar seu aplicativo para verificar o número da versão do iOS antes de adicionar vários DRMSessions. Ou podem restringir a distribuição de seu aplicativo para iOS v5 e superior. </p> <p>se o problema ocorrer porque a versão dos metadados é superior à versão 2, o problema provavelmente está corrompido metadados. Eles podem tentar reconstruir os metadados e observar os resultados. Se eles continuarem a ver o problema, registre o problema e escale para o Adobe. </p> </li> 
     </ul> <p>Para obter mais informações sobre esse código de erro, consulte <a href="https://forums.adobe.com/thread/1266675" format="https" scope="external"> Como corrigir um código de erro 3306 DRMErrorEvent</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3307 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InternalFailure</span> </td> 
   <td colname="col3"> <p>Isso geralmente representa um bug no código do Adobe Access e é inesperado, a menos que haja um bug conhecido, como abaixo. subErrorId contém um erro específico do cliente ou erro de linha. </p> 
    <ul id="ul_79F4A9655A2148519B1E9509C41F78C3"> 
     <li id="li_0E093AB4D6BD489B852279E6C1525A15">Se o navegador for Chrome no Windows e a versão do Flash for 11.6 (SWF versão 19 ou superior), o software do distribuidor deverá assumir que o usuário pressionou <span class="uicontrol"> Negar</span> no infoque e trate o mesmo que um 3368. </li> 
     <li id="li_0215D1089B344861A2C0A73E1067CFEF">Se o 3307 ocorrer quando o navegador não for Chrome ou a versão do Flash não for 11.6, o distribuidor deverá se encaminhar para o Adobe. </li> 
    </ul> <p>Importante: <span class="codeph"> 3307:1107296344 (FailedToGetBrokerHandle)</span> pode acontecer com as versões 24-28 do navegador Chrome. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3308 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WrongLicenseKey</span> </td> 
   <td colname="col3"> <p>Esse erro é lançado sempre que a licença que está sendo usada contém a chave errada para descriptografar o conteúdo. subErrorId contém um erro específico do cliente ou erro de linha. </p> <p>Parece haver apenas duas maneiras de gerar esse erro: 
    <ul id="ul_1C955BD74C7843809D1B5A0CDCA5ED7B"> 
     <li id="li_18F0A7FDA6584887AD9DB3EDE54080D8">O cliente modificou a ferramenta Adobe padrão para geração de licenças (por exemplo, a estrutura Java do servidor do licenciado). <p>Nesse caso, a licença contém uma chave incorreta que pode não corresponder a nenhum conteúdo. </p> </li> 
     <li id="li_21D04ED1F1FA464785BC297D385766FF">O cliente emitiu várias licenças com a mesma ID de licença. <p>Nesse caso, há várias licenças disponíveis no cliente que correspondem aos metadados de conteúdo e o código de acesso selecionou a errada para uso. </p> </li> 
    </ul> </p> 
    <ul id="ul_64AEE62BE36946F290067CF475A36ECA"> 
     <li id="li_9EEB2B11A4DA41E78C5840D8FAA81F0D">O software do distribuidor deve tentar adquirir novamente a licença do servidor. 
      <ul id="ul_ACADC5518B054D0A853AEED2B675DB23"> 
       <li id="li_394835C8731048A5BF7D9370AC12448C">Se nenhuma licença estiver disponível ou a licença tiver expirado, forneça fluxo de trabalho para o usuário adquirir nova licença ou informe o usuário de que o conteúdo não pode ser observado e registre o problema. </li> 
       <li id="li_3FE50518BE53405F9563FA620F7EAD5F">Se esse for um conteúdo vinculado a domínio (para AIR), forneça uma maneira para o usuário ingressar no domínio. </li> 
      </ul> </li> 
     <li id="li_C80B353C1AEA4E9398241420CB491E84">O distribuidor deve: 
      <ul id="ul_B5C50009374C4EED9B2B050B48F5F0F6"> 
       <li id="li_D5E6B760E0BC4B5C949ED1544B398838">Verifique se eles não personalizaram as partes de emissão da licença do servidor de Licenças de Acesso. </li> 
       <li id="li_AA8F4E4B6DDD40BA8807C0920A92186B">Verifique se estão emitindo IDs de licença exclusivas para todas as licenças. </li> 
       <li id="li_A2C53FE779AC4FDDB65E00A2C4F43EC4">Escalone o problema com o Adobe. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3309 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedAdditionalHeader  </span> </td> 
   <td colname="col3"> <p>Isso ocorrerá se o cabeçalho for maior que 65536 bytes. </p> 
    <ul id="ul_82C0F688519B4F43A764D59A891F1903"> 
     <li id="li_E66AC9149A0649E88A79C5289C12C395">O software do distribuidor deve registrar qual parte do conteúdo causou o erro. </li> 
     <li id="li_1C5916A33E7B4DC9968105B9BD20A727">O distribuidor deve confirmar que o erro é reprodutível com partes específicas de conteúdo. Reempacotar conteúdo quebrado. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3310 </td> 
   <td colname="col2"><span class="codeph"> AXS_AppIDMismatch  </span> </td> 
   <td colname="col3">O aplicativo Android não corresponde ao que está em uso. <p>O aplicativo AIR correto ou o SWF do Flash não está sendo usado. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3311 </td> 
   <td colname="col2"><span class="codeph"> AXS_AppVersionMismatch  </span> </td> 
   <td colname="col3"> Não está em uso. Esse problema ainda pode ser gerado pela pilha da versão 1.x no AIR. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3312 </td> 
   <td colname="col2"><span class="codeph"> AXS_LicenseIntegrity  </span> </td> 
   <td colname="col3"> Para corrigir isso, baixe novamente a licença do servidor. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3313 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WriteMicrosafeFailed  </span> </td> 
   <td colname="col3"> <p>Esse problema ocorre quando o sistema não consegue gravar no sistema de arquivos. <span class="codeph"> </span> subErrorIdis contém um erro de linha ou específico do cliente. </p> <p>No Microsoft Windows, o erro 3313 pode ser jogado pelo Ative X ou NPAPI plug flash player quando o conteúdo criptografado tem uma licenseID ou uma policyID muito longa. Isso ocorre devido ao comprimento máximo do caminho no Windows. (O plug-in Pepper não apresenta esse problema.) </p> <p>Ver watson 3549660 </p> 
    <ul id="ul_DFD527D1E1224A439766DF7BED878E3B"> 
     <li id="li_FAF8FD98A4E8478CA7A92F770676ADFC">O software do distribuidor deve solicitar ao usuário que confirme se o diretório do usuário não está bloqueado nem em um volume que está cheio ou bloqueado. </li> 
     <li id="li_6D1136EA750A459BBECEEE5F73F527BB">Se o distribuidor estiver usando o AIR, em vez de Flash, o problema pode ser causado por uma limitação de comprimento do caminho. <p>Os distribuidores devem reduzir o nome da sua aplicação AIR a algo razoável. Além disso, publique conteúdo novamente com uma <span class="codeph"> licenseID</span> mais curta e uma <span class="codeph"> policyID</span> mais curta. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3314 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedDRMMetadata  </span> </td> 
   <td colname="col3"> <p>Esse erro geralmente indica que o conteúdo foi empacotado com certificados PKI de teste e o reprodutor é criado com PKI de produção ou vice-versa. subErrorId contém um erro específico do cliente ou erro de linha. </p> 
    <ul id="ul_A122EF304CAF48A8B4DA1E3F4413E29B"> 
     <li id="li_A9A1A5B23E884C22A71E2DE7535FEB3B">O software do distribuidor deve registrar qual parte do conteúdo causou o erro. </li> 
     <li id="li_7AD7F13A4B1B4998A7E49664E7645815">O distribuidor deve confirmar que o erro é reprodutível com partes específicas de conteúdo. <p>Talvez seja necessário reempacotar conteúdo quebrado. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3315 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PermissionDenied  </span> </td> 
   <td colname="col3"> <p>Há bugs conhecidos nos quais esse código de erro é lançado quando um 3305 é destinado. Para obter mais informações, consulte <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed] causes and resolution</a>. </p> <p>O SWF remoto carregado pelo AIR não tem permissão para acessar a funcionalidade do Flash Access. Esse código de erro também pode ser lançado se ocorrer um erro de segurança durante o acesso à rede. Os exemplos incluem o servidor de destino não o cliente para se conectar usando o cross-domain.xml ou o cross-domain.xml não pode ser acessado. </p> <p>Para obter mais informações, consulte <a href="https://forums.adobe.com/thread/1266592" format="https" scope="external"> Erro de DRM 3315 possível causa raiz e resolução</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3316 </td> 
   <td colname="col2"><span class="codeph"> AXS_NOTUSED_MOVED  </span> </td> 
   <td colname="col3"> Era <span class="codeph"> ADOBECPSHIM_MinorErr_MissingAdobeCPModule</span>. Movido para 3344 devido a conflito com o código de erro de Flash. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3317 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LoadAdobeCPFailed  </span> </td> 
   <td colname="col3"> <p>Importante:  Esse é um erro raro e geralmente não ocorre em um ambiente de produção. </p> <p>Se o erro ocorrer, é possível executar um dos seguintes procedimentos: 
     <ul id="ul_BC435E61623444BB98A86216531DC892"> 
      <li id="li_FA433D0758B642D2AFDCF04906B3FE18">Se estiver usando o AIR, reinstale-o. </li> 
      <li id="li_F08D9AAFF46244F8842DEE5FD9CBBE0A">Se você estiver usando o Flash Player, baixe os módulos <span class="codeph"> AdobeCP</span> novamente. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3318 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncompatívelAdobeCPVersion  </span> </td> 
   <td colname="col3"> Não aplicável para Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3319 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPGetAPI  </span> </td> 
   <td colname="col3"> Não aplicável para Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3320 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HostAuthenticateFailed  </span> </td> 
   <td colname="col3"> Não aplicável para Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3321 </td> 
   <td colname="col2"><span class="codeph"> AXS_I15nFalha  </span> </td> 
   <td colname="col3"> <p>Falha no processo de provisionamento do cliente com chaves. subErrorId contém um erro de linha, específico do servidor ou do cliente. </p> 
    <ul id="ul_98D919B9060A441AACB6106F6D8E8DA7"> 
     <li id="li_DCAB00A8AC4A426CBBD377374B3F71AE">O software do distribuidor deve repetir a operação pelo menos uma vez. <p>Se você estiver usando o Google Chrome no Windows, forneça uma explicação sobre como permitir acesso de plug-in que não esteja em uma sandbox. Para obter mais informações, consulte <a href="https://helpx.adobe.com/adobe-access/kb/error-3321.html" format="html" scope="external"> Acesso à caixa de proteção do Google Chrome negado</a>. </p> </li> 
     <li id="li_7FB7681FE32D444BB1BDBA3E5953A2C3">O distribuidor deve realizar uma das seguintes tarefas: 
      <ul id="ul_486B64F187C44AE3B4775953A6142836"> 
       <li id="li_095B1D4CD051427CB2BFA7082B454056">Se o erro for consistente em todas as plataformas, você deverá encaminhar o problema com o Adobe. </li> 
       <li id="li_0C6EB7B912FA41E59657216498DA3515">Se o erro estiver confinado ao Chrome no Windows, guie o usuário para permitir acesso de plug-in em caixa não restrita. </li> 
      </ul> <p>Os distribuidores devem atualizar seu SWF para a versão 19 ou posterior e, devido ao erro 3321 específico do Chrome, um erro 3368 é lançado. O erro 3368 pode ser tratado mais especificamente pelo software do distribuidor. Essa alteração foi introduzida no canal Chrome Stable versão 26.0.1410.43. </p> <p>Dica: O erro <span class="codeph"> 3321:1090519056</span> pode ocorrer com as versões de Flash Player 11.1 a 11.6. Recomendamos que você atualize para a versão mais recente do Flash Player. </p> </li> 
    </ul> <p>Para obter mais informações, consulte <a href="https://forums.adobe.com/thread/1277138" format="https" scope="external"> Erro de DRM 3321 Causas e Resolução</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Erros de corrupção na loja global</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3322 </td> 
   <td colname="col2"><span class="codeph"> AXS_DeviceBindingFailed  </span> </td> 
   <td colname="col3"> <p>O dispositivo não parece corresponder à configuração que estava presente quando inicializado. subErrorId contém um erro de linha ou específico do cliente. </p> <p>O software do distribuidor deve realizar uma das seguintes tarefas: 
     <ul id="ul_444401051A2E407B95BC44491E9BB71C"> 
      <li id="li_93493EA05DB44CB1AEC368663F1ABA8D"> <p>Se o dispositivo não estiver usando o Flash Player e estiver usando o AIR, iOS e assim por diante, chame <span class="codeph"> DRMManager.resetDRMVouchers()</span>. </p> <p>Se o problema ocorrer no iOS em uma fase de desenvolvimento, peça ao desenvolvedor para confirmar se o problema é observado ao alternar entre builds que foram baixadas de sistemas de distribuição de pré-lançamento de terceiros (por exemplo, HóqueiApp) e uma build local do Xcode. Os atributos de uma instalação anterior não são inteiramente substituídos ao alternar entre uma build distribuída do HóqueiApp e uma build do Xcode. Essa situação pode acionar o erro 3322. </p> <p>Para resolver esse problema, o desenvolvedor deve remover a build mais antiga do dispositivo antes de instalar a nova build. </p> </li> 
      <li id="li_A5C9633F11584C788A2D9A23CC18FA6D">Se o dispositivo estiver usando o Flash Player e ele não puder ser usado a partir de um código de erro 3322 ou 3346, consulte as instruções do Adobe sobre como redefinir programaticamente o armazenamento de licença do DRM em <a href="https://forums.adobe.com/message/5535907#5535907" format="https" scope="external"> Erro do DRM 3322/3346/3368 no Chrome (Problemas da Info-Bar)</a>. </li> 
     </ul> </p> <p>Esse erro não é esperado para ocorrer com frequência. Em ambientes corporativos que usam perfis de roaming, se um usuário estava visualizando conteúdo protegido por DRM, a probabilidade de o erro 3322 ocorrer aumenta à medida que o usuário entra em diferentes máquinas. Se possível, o distribuidor deve tentar obter essas informações do usuário. </p> <p>Se o erro ocorrer com frequência, encaminhe-o para Adobe. Você deve notificar o Adobe se a redefinição do armazenamento de licenças resolveu (ou não) o problema e informar ao Adobe em quais navegadores o erro está ocorrendo. </p> <p>Para obter mais informações, consulte os seguintes artigos: 
     <ul id="ul_C468409D1EA046178CA7F54DCDCB84EA"> 
      <li id="li_20C8CA3853574CE486F21E7A3667DAB9"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> https://forums.adobe.com/message/5520902</a> </li> 
      <li id="li_6E6F1BD6FE7843449B3E2F06F342EFF7"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> https://forums.adobe.com/message/5535911</a> </li> 
      <li id="li_2BE40E513A0C4BAD900C7B69FEF5D690"><a href="https://forums.adobe.com/message/5748618" format="https" scope="external"> https://forums.adobe.com/message/5748618</a> </li> 
      <li id="li_9C2BD122E3874E2893DD43E082A877E0"><a href="https://forums.adobe.com/message/6061165" format="https" scope="external"> https://forums.adobe.com/message/6061165</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3323 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptGlobalStateStore  </span> </td> 
   <td colname="col3"> <p>Os arquivos usados pelo cliente DRM foram modificados inesperadamente. subErrorId contém um erro de linha ou específico do cliente. </p> 
    <ul id="ul_96EA771046CA4B2B9FAE24D493F43FF2"> 
     <li id="li_D2693CD8EFEF46108828BA17E3F54FF6">O software do distribuidor deve guiar o usuário para redefinir da mesma forma que o 3322. </li> 
     <li id="li_0149B82436B64E28AC2B8C9B0EB09898">Se o GlobalStore estiver falhando a uma taxa superior à taxa de falha esperada dos discos rígidos da base de usuários, encaminhe o problema para o Adobe. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3324 </td> 
   <td colname="col2"><span class="codeph"> AXS_MachineTokenInvalid  </span> </td> 
   <td colname="col3"> Redefina o armazenamento local do DRM para este aplicativo. Chame DRMManager.resetDRM. <p>O servidor de licenças talvez não consiga se conectar ao servidor da Lista de Revogação de Certificados (CRL) para atualizar seus arquivos CRL, ou o computador cliente está solicitando uma licença/autenticação que foi revogada pelo servidor de licenças. </p> <p>Nos logs do servidor, um código de erro 111 é MachineTokenInvalid. No entanto, no nível do cliente, o código de erro 111 é traduzido para o código de erro 3324. </p> <p>O administrador do servidor de licenças DRM deve verificar se o servidor de licenças do cliente já conseguiu recuperar os arquivos Adobe CRL. Se o cliente estiver usando o Tomcat, poderá verificar o diretório<span class="filepath"> tomcat/temp/</span> para ver se há 4 arquivos CRL. </p> 
    <ul id="ul_23B7F1A104AF49E79EA87DB8E15E337E"> 
      <li id="li_855D87F251184FE688A8D5FA0F6C9EF5">Se os arquivos estiverem nesse diretório, clique duas vezes nos arquivos no Windows Explorer e no aplicativo do visualizador CRL, determine se algum dos arquivos expirou. </li> 
      <li id="li_58EC4EDA2B5146188A0FF7B33C91E2FD">Se não houver arquivos em tomcat/temp/, pode-se assumir que esse servidor de licença nunca conseguiu acessar o servidor Adobe CRL devido a um problema de firewall/roteamento. Para obter mais informações, consulte <a href="https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_secure_deployment_guidelines.pdf" format="http" scope="external"> Regras de firewall.</a></li>
    </ul> </p> <p>Se os arquivos CRL não estiverem disponíveis ou tiverem expirado, você deverá confirmar se o servidor de licenças pode ser acessado. Abra um sniffer de rede no servidor de licenças do cliente, reinicie o servidor e tenha uma tentativa do cliente de solicitar uma licença do servidor. Você pode observar o tráfego de rede para ver se as chamadas para os seguintes pontos de extremidade de URL são bem-sucedidas: <p>Dica:  Você também pode inserir os seguintes URLs de CRL em um navegador para ver se é possível baixar manualmente cada arquivo. </p> 
    <ul id="ul_9B65C7ABBDEC4AC9BF3755FFD3587971"> 
      <li id="li_6867A9050E8D421C9138AC853D1784C9"><a href="https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl</a> </li> 
      <li id="li_6431689260554EAFAFDA2EC31798DCB5"><a href="https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl</a> </li> 
      <li id="li_2939674D0F854ADEB67E45FD216288A2"><a href="https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessRootCA.crl</a> </li> 
      <li id="li_96386E00BE9D4CB99D100057A5F7C6DD">crl3.adobe.com/AdobeSystemsIncorporated FlashAccessRuntime/LatestCRL.crl</li> 
    </ul> </p> <p>Se as regras de firewall estiverem abertas e não houver erros 3324 atuais, pode ter havido um problema temporário de rede. Verifique os logs do servidor do cliente, que provavelmente estão no diretório <span class="codeph"> /tomcat/logs/</span>, para determinar se ocorreu um erro quando o servidor de licença tentou buscar as Listas de Revogação de Certificado. <p>Importante:  Um erro pode ocorrer quando um grande número (ou uma explosão) de clientes relata um erro 3324 a um problema de rede temporário ao renovar um arquivo CRL. Quando o problema de rede foi resolvido, os 3324 problemas também foram resolvidos. </p> </p> <p>Se todos os 4 arquivos CRL existirem no diretório <span class="filepath"> tomcat/temp/</span> e os clientes ainda estiverem recebendo 3324 códigos de erro, pode haver problemas de acesso a arquivos para os arquivos CRL. Para resolver esse problema, talvez você queira revisar os logs e limpar os arquivos CRL existentes. </p> <p>Se não houver problemas de servidor, solicite que o usuário seja redefinido no, conforme descrito em 3322. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Erros de corrupção na loja de servidores</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
</tr> 
  <tr> 
   <td colname="col1"> 3325 </td> 
   <td colname="col2"><span class="codeph"> AXS_CorruptServerStateStore  </span> </td> 
   <td colname="col3"> <p>Os arquivos usados pelo cliente DRM foram modificados inesperadamente. <span class="codeph"> </span> subErrorIdis contém um erro de linha ou específico do cliente. </p> 
    <ul id="ul_860D2402DA61460AB0D938F1116F6D64"> 
     <li id="li_CF368C43452B4265B62ADA3E223894BA">O software do distribuidor deve repetir a operação, pois o AdobeCP excluiu o armazenamento de servidor ofensivo internamente e uma nova tentativa deve ser bem-sucedida. Se a tentativa falhar, registre o problema. </li> 
     <li id="li_51A5803A1F754970BB4EBD6494F5DC96">Se as tentativas estiverem falhando a uma taxa superior à taxa de falha esperada dos discos rígidos da base de usuários, encaminhe o problema para Adobe. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3326 </td> 
   <td colname="col2"><span class="codeph"> AAXS_StoreTamperingDetected  </span> </td> 
   <td colname="col3"> Chame <span class="codeph"> DRMManager.resetDRM</span>. <p>O License Store foi adulterado/corrompido e não pode mais ser usado. </p> <p>O software do distribuidor deve guiar o usuário para redefinir da mesma forma descrita no 3322. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3327 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClockTamperingDetected  </span> </td> 
   <td colname="col3"> Corrija o relógio ou adquira novamente a licença <span class="codeph"> Authn/Lic/Domain</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Erros de autenticação/licença/servidor de domínio</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3328 </td> 
   <td colname="col2"><span class="codeph"> AXS_ServerErrorTryAgain  </span> </td> 
   <td colname="col3"> <p>Este é um erro do lado do servidor no qual o servidor não pôde concluir a solicitação do cliente. Esse erro pode ocorrer quando, por exemplo, o servidor está ocupado, HTTP/500, o servidor não tem a chave necessária para descriptografar a solicitação e assim por diante. </p> <p>No cliente, não há como determinar o que deu errado. O cliente deve revisar os logs do servidor do Adobe Access, que geralmente são chamados de <span class="codeph"> AdobeFlashAccess.log</span>, para determinar o que deu errado. Sempre há um rastreamento de pilha descritivo no log para indicar o problema. <span class="codeph"> </span> subErrorIdis contém um erro de linha ou específico do servidor. </p> <p>O distribuidor deve consultar os registros do servidor para identificar qual servidor está enviando esse erro. Para erros 3328 que têm um código de suberro 101, o servidor não pode descriptografar a solicitação. O cliente deve validar se os certificados do servidor de licença/transporte instalados no servidor de licenças correspondem aos certificados usados durante o empacotamento. </p> <p>Além disso, se os clientes estiverem usando a Implementação de referência, eles deverão garantir que não haja erros de digitação no arquivo <span class="codeph"> flashaccess-refimpl.properties</span> onde os certificados primários e adicionais são especificados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3329 </td> 
   <td colname="col2"><span class="codeph"> AXS_ApplicationSpecificError  </span> </td> 
   <td colname="col3"> <p>O código de suberro específico do aplicativo não é conhecido pelo Flash Access. <span class="codeph"> </span> subErrorIdentidade contém um erro específico do servidor de licenças personalizadas dos editores. O servidor retornou um erro no namespace específico do aplicativo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3330 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NeedAuthentication  </span> </td> 
   <td colname="col3"> <p>Esse erro ocorre quando o conteúdo é configurado para solicitar que os clientes se autentiquem antes de obter as licenças. </p> 
    <ul id="ul_712D29B8B5A6401FB014C4A283918E32"> 
     <li id="li_2D56905EB50D4FDEAD69CA8EAE38AD1A">O software do distribuidor deve autenticar o usuário e depois adquirir a licença novamente. <p>Se o serviço não pretende usar autenticação, registre a identificação do conteúdo que está causando esse erro. </p> </li> 
     <li id="li_B3BCF899B8BE41C7A4F7CF84B0503483">Esse erro não deve exigir um escalonamento, a menos que o conteúdo não deva ser configurado para exigir autenticação. <p>Nesse caso, reintegre o conteúdo ofensivo com a política adequada. Se o conteúdo estiver empacotado corretamente, consulte Diagnosticando discrepâncias entre a política e a licença. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Erros de imposição de licença não cobertos acima</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
</tr> 
  <tr> 
   <td colname="col1"> 3331 </td> 
   <td colname="col2"><span class="codeph"> AXS_ContentNotYetValid  </span> </td> 
   <td colname="col3"> <p>A licença adquirida ainda não é válida. Para resolver esse problema, verifique se o relógio do cliente não está definido corretamente. Para definir o relógio do cliente, reempacote o conteúdo ou modifique a configuração do servidor de licença. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3332 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CachedLicenseExpirado  </span> </td> 
   <td colname="col3"> Readquira a licença do servidor. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3333 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PlaybackWindowExpirated  </span> </td> 
   <td colname="col3"> <p>Você deve notificar os usuários de que eles não poderão reproduzir esse conteúdo até que a política expire. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3334 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMPlatform  </span> </td> 
   <td colname="col3"> <p>Esta plataforma não tem permissão para reproduzir o conteúdo porque, por exemplo, o provedor de conteúdo configurou o Adobe Access para negar o conteúdo ao Adobe Access em uma plataforma ou uma licença vinculada a um domínio compartilhado é vinculada a um token de domínio compartilhado destinado a uma partição diferente. </p> <p>O CDM pode gerar esse erro se o conteúdo não tiver sido empacotado usando uma certificação apropriada do empacotador (compatível com o recurso CDM). </p> <p>Se o conteúdo for empacotado com um certificado PHDS/PHLS incorreto, ele poderá funcionar no Chrome, mas não em outros navegadores (ou vice-versa). <p>Dica:  Isso ocorre porque o Chrome usa diferentes certificados PHDS/PHLS. </p>Para confirmar qual certificado está sendo usado, descarte os detalhes dos metadados de conteúdo e procure pelos <i>certificados do recipient</i>. Para obter mais informações, consulte <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3335 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMVersion  </span> </td> 
   <td colname="col3"> Atualize para a versão mais recente do TVSDK para Android. <p>Para resolver esse problema, conclua uma das seguintes tarefas: 
     <ul id="ul_BF1742948BC9461CB8686DE70124D3CD"> 
      <li id="li_690D440C94CC45A0AE55EC319B1C4C23">Atualizar o AIR </li> 
      <li id="li_CDD20251C881466E88BE7BBB53D61EBC">Para o Flash Player, atualize o módulo AdobeCP e tente reproduzir. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3336 </td> 
   <td colname="col2"><span class="codeph"> AXS_InvalidRuntimePlatform  </span> </td> 
   <td colname="col3"> <p>Essa plataforma não tem permissão para reproduzir o conteúdo porque, por exemplo, o provedor de conteúdo configurou o Acesso para negar o conteúdo ao FP/AIR em uma plataforma. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3337 </td> 
   <td colname="col2"><span class="codeph"> AXS_InvalidRuntimeVersion  </span> </td> 
   <td colname="col3"> Atualize para a versão mais recente do TVSDK para Android. <p>Isso ocorre se o conteúdo ou o servidor estiver configurado para negar a reprodução para uma versão específica do Flash ou dos tempos de execução do AIR. </p> 
    <ul id="ul_B0732D941256483CABBDD30C9BF43249"> 
     <li id="li_72782B1D638F48C0B87084689FB9C798">Se o usuário estiver em um sistema operacional no qual o Flash possa ser atualizado, o software do distribuidor deverá solicitar que o usuário atualize o Flash e tente novamente. Caso contrário, aconselhe o usuário a usar uma máquina diferente. </li> 
     <li id="li_1E3FD93CE39E43F2B7D961299B1211DA">Se o erro 3337s for suspeito, identifique se ele está ocorrendo para um conteúdo específico e reempacote esse conteúdo. Se o conteúdo estiver empacotado corretamente, consulte Diagnosticando discrepâncias entre a política e a licença </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3338 </td> 
   <td colname="col2"><span class="codeph"> AXS_UnknownConnectionType  </span> </td> 
   <td colname="col3"> <p>Não é possível detectar o tipo de ligação e a política requer que ative a Proteção de Saída. Esse problema é esperado somente se o conteúdo for empacotado para exigir proteção de saída digital ou analógica. </p> <p>Um problema nas versões do Flash Player anteriores à versão 11.8.800.168 causou ocasionalmente o erro 3338 no conteúdo para o qual a política indicou que a proteção de conteúdo é <span class="codeph"> USE IF DISPONÍVEL</span>. Esse problema é corrigido na versão 11.8.800.168 e posterior. </p> 
    <ul id="ul_4B6CA26A53F84838B5B95400925464D4"> 
     <li id="li_CBD890F467E449EBB5116E1561252058">O software do distribuidor seleciona uma variante do conteúdo que não requer proteção de saída (por exemplo, variante SD de um fluxo HD). <p>Se o erro 3338 estiver ocorrendo no conteúdo <span class="codeph"> USE_IF_AVAILABLE </span>, verifique o número da versão do reprodutor. Se a versão do reprodutor for inferior a 11.8.800.168, aconselhe o usuário a atualizar o Flash Player. Se o erro 3338 estiver ocorrendo em versões acima de 11.8.800.168, registre qual conteúdo causou o erro. </p> </li> 
     <li id="li_62886C1D96264B129928A7E29E6C70E1">O distribuidor deve verificar qual conteúdo está causando esse erro e validar se a política do conteúdo está definindo <span class="codeph"> NO_PROTECTION</span> ou <span class="codeph"> USE_IF_AVAILABLE</span> para saídas analógicas e digitais. <p>Se o conteúdo for inadvertidamente empacotado com <span class="codeph"> NO_OUTPUT</span> ou <span class="codeph"> OBRIGATÓRIO</span>, reempacote o conteúdo. Se o conteúdo for empacotado corretamente, consulte Diagnosticando discrepâncias entre a política e a licença. Caso contrário, escale para Adobe. </p> </li> 
    </ul> <p>Para obter mais informações, consulte <a href="https://forums.adobe.com/message/5518688" format="https" scope="external"> Recebendo erros 3338 inesperados quando sua política de DRM está definida como USE_IF_AVAILABLE?</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3339 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogPlaybackAllowed  </span> </td> 
   <td colname="col3"> Não é possível reproduzir no dispositivo analógico. Para resolver o problema, conecte um dispositivo digital. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3340 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogProtectionAvail  </span> </td> 
   <td colname="col3"> Não é possível reproduzir o conteúdo porque o dispositivo de exibição externo analógico (monitor/TV) conectado não tem os recursos corretos (por exemplo, o dispositivo não tem Macrovision ou ACP). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3341 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalPlaybackAllowed  </span> </td> 
   <td colname="col3"> Não é possível reproduzir conteúdo em um dispositivo digital. <p>Importante:  Esse problema não deve ocorrer em um ambiente de produção, pois os editores de conteúdo não devem impedir a reprodução digital. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3342 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalProtectionAvail  </span> </td> 
   <td colname="col3"> O dispositivo de vídeo externo digital conectado (monitor/TV) não tem os recursos corretos. Por exemplo, o dispositivo não tem HDCP. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3343 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IntegrityCheckFailed  </span> </td> 
   <td colname="col3"> <p>Não aplicável para Android. </p> <p>Esse erro é conhecido inicialmente depois que uma nova versão do Flash é lançada. Isso ocorre porque o Flash foi atualizado enquanto o Flash estava aberto, o que coloca o Flash em um estado incorreto até que o navegador seja reiniciado. </p> 
    <ul id="ul_A0AC4A77550E40409A04BD33748EA987"> 
     <li id="li_F41C1ABD838D41ABB0DF65093E664A29">O software do distribuidor deve realizar as seguintes tarefas: 
      <ul id="ul_79B2AB1372074D448F129851AA24F985"> 
       <li id="li_B93EDD263D78434FAF198A01938D3508">Recomendamos que o usuário feche ou saia de todos os navegadores e abra novamente. </li> 
       <li id="li_ADFBCFA66AD849E18DB390455458528E">Verifique se a versão do Flash é atual. <p>Se a versão não for atual, aconselhe o cliente a atualizar, fechar todas as guias do navegador e reabrir. </p> </li> 
      </ul> </li> 
     <li id="li_281B54582B5949AEA7D166246917EE41">Se um erro aparecer após uma reinicialização bem-sucedida do navegador, escale para Adobe. <p>Quando uma nova versão for lançada, recomendamos que você entre em contato com o Suporte do Adobe para verificar se o problema de atualizações em segundo plano foi corrigido. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3344 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPModule  </span> </td> 
   <td colname="col3"> Não aplicável para Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3345 </td> 
   <td colname="col2"><span class="codeph"> AXS_DRMNoAccessError  </span> </td> 
   <td colname="col3"> <p>Não aplicável para Android. </p> <p>Esse erro ocorre quando parte do Flash ou do AIR não foi instalada corretamente. </p> <p>O software do distribuidor deve executar um dos seguintes procedimentos: 
     <ul id="ul_D1188E2D4FDF4BD89A04F5629D75D981"> 
      <li id="li_B33FBCA5D4534D668B86A5E93DB3A809">Peça ao usuário para desinstalar e reinstalar o AIR. </li> 
      <li id="li_B7D2388E9FA84C26AF1C87B48AF9EF16">Para Flash Player, chame <span class="codeph"> System.update</span>. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3346 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MigrationFailed  </span> </td> 
   <td colname="col3"> 
    <ul id="ul_518AD4931CC64EB3A962DD451E6C5067"> 
     <li id="li_3C44F0740B08490E9C62D89C40B57DC2">O software do distribuidor deve executar um dos seguintes procedimentos: 
      <ul id="ul_7D90526684BF4EB2BBADCF598AA13086"> 
       <li id="li_D15B4BEDAF7340F6B9BC886DF6E346EC">Se estiver usando o AIR, chame <span class="codeph"> DRMManager.resetDRMVouchers()</span> </li> 
       <li id="li_40A51D35408249CFA28DBC49FDA3408B">Se o Flash tiver um código de erro inutilizável devido aos erros 3322 ou 3346, os usuários devem ir para <a href="https://forums.adobe.com/message/5535907#5535907" format="http" scope="external"> https://forums.adobe.com/message/5535907#5535907</a> e seguir as instruções do artigo do Adobe para redefinir programaticamente seu armazenamento de licença de DRM. </li> 
      </ul> </li> 
     <li id="li_0464471E4A094C80BF2986694341921A">Se esse erro ocorrer com frequência, o distribuidor deve fornecer os detalhes sobre a versão do reprodutor de frequência e a versão do navegador para o Adobe. </li> 
    </ul> <p>Para obter mais informações, consulte os seguintes artigos do fórum: 
     <ul id="ul_44E0077FEAA749CC9549BF3846065304"> 
      <li id="li_2BE3B2443380415DA73B7AA3B6547B31"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Erro de DRM 3322/3346/3368 no Chrome (problemas da Info-Bar)</a> </li> 
      <li id="li_4E5C7414756644E1AB78BE7B8112228C"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> Erro 3322 ou 3346 após alteração de hardware</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3347 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InsuficienteDeviceCapabilites  </span> </td> 
   <td colname="col3"> <p>O principal significado desse erro é que a licença tem uma restrição que o certificado de DRM dos clientes indica que não pode atender. Os seguintes "recursos de hardware" são definidos quando o certificado de DRM de clientes é emitido: 
     <ul id="ul_1EB6F1469C244CF0BA52C212495C053D"> 
      <li id="li_646043CE045C4DE2BBC939E1F4963DFE"><b>Barramento não acessível ao usuário</b>. Se <b>true</b>, a mídia descriptografada nunca fluirá através de um barramento ou para a memória principal, onde um aplicativo pode acessá-la. <p>Se <b>false</b>, o conteúdo pode ser acessível ao aplicativo após a descriptografia. </p> </li> 
      <li id="li_02AAECAF4D35447BA10554541B46DE67"><b>Raiz de Hardware da Confiança</b>. Se <b>true</b>, todo o software carregado no momento da inicialização no dispositivo foi validado em relação a uma chave ou um resumo que só está disponível no hardware. <p>Ambas as restrições são verificadas no lado do cliente quando a licença é aberta em relação ao certificado DRM para o cliente e a falha é imediata. Essas restrições também podem ser verificadas no lado do servidor antes da emissão da licença. </p> </li> 
     </ul> </p> <p>O significado secundário deste erro é que a licença tem o conjunto de políticas "Execução de Jailbreak" e uma interrupção de jailbreak foi detectada no dispositivo. Essa verificação é feita periodicamente no lado do cliente e não pode ser verificada no lado do servidor. </p> <p>Os distribuidores podem atualizar as políticas e remover as restrições. Para políticas de capacidade de dispositivo, emita o comando de atualização da política com o sinalizador <span class="codeph"> -devCapabilitiesV1</span> e sem argumentos. Para imposição de quebra de maré, defina <span class="codeph"> policy.enforceJailbreak=false</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3348 </td> 
   <td colname="col2"><span class="codeph"> AXS_HardStopIntervalExpirated  </span> </td> 
   <td colname="col3"> Intervalo de parada permanente expirado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3349 </td> 
   <td colname="col2"><span class="codeph"> AXS_ServerVersionTooHigh  </span> </td> 
   <td colname="col3"> O servidor está sendo executado em uma versão superior à mais alta que é compatível com o cliente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3350 </td> 
   <td colname="col2"><span class="codeph"> AXS_ServerVersionTooLow  </span> </td> 
   <td colname="col3"> O servidor está sendo executado em uma versão inferior à versão mínima suportada pelo cliente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3351 </td> 
   <td colname="col2"><span class="codeph"> AXS_DomainTokenInvalid  </span> </td> 
   <td colname="col3"> O token de domínio era inválido. Para resolver esse problema, registre-se novamente no domínio . </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3352 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooOld  </span> </td> 
   <td colname="col3"> O token de domínio é anterior ao token exigido pela licença. Para resolver o problema, registre-se novamente no domínio . </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3353 </td> 
   <td colname="col2"><span class="codeph"> AXS_DomainTokenTooNew  </span> </td> 
   <td colname="col3"> O token de domínio é mais recente do que o token exigido pela licença. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3354 </td> 
   <td colname="col2"><span class="codeph"> AXS_DomainTokenExpirado  </span> </td> 
   <td colname="col3"> O token de domínio expirou. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3355 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainJoinFailed  </span> </td> 
   <td colname="col3"> Falha na associação do domínio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3356 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCorrespondingRoot  </span> </td> 
   <td colname="col3"> Não foi encontrada uma licença raiz para uma licença V3 leaf. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3357 </td> 
   <td colname="col2"><span class="codeph"> AXS_NoValidEmbeddedLicense  </span> </td> 
   <td colname="col3"> Nenhuma licença incorporada válida foi encontrada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3358 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoACPPprotectionAvail  </span> </td> 
   <td colname="col3"> Não é possível reproduzir porque o dispositivo analógico ligado não tem proteção ACP. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3359 </td> 
   <td colname="col2"><span class="codeph"> AXS_NoCGMSAPprotectionAvail  </span> </td> 
   <td colname="col3"> Não é possível reproduzir porque o dispositivo analógico ligado não tem proteção CGMS-A. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3360 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainRegistrationRequired  </span> </td> 
   <td colname="col3"> O conteúdo requer registro de domínio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3361 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NotRegisteredToDomain  </span> </td> 
   <td colname="col3"> O computador não está registrado no domínio para os metadados especificados. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3362 </td> 
   <td colname="col2"><span class="codeph"> AXS_OperationTimeoutError  </span> </td> 
   <td colname="col3"> A operação assíncrona levou mais do que <span class="codeph"> maxOperationTimeout</span>. Retornado somente pelo iOS DRMNative Framework. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3363 </td> 
   <td colname="col2"><span class="codeph"> AXS_UnsupportedIOSPlaylistError  </span> </td> 
   <td colname="col3"> A lista de reprodução M3U8 transmitida tinha conteúdo não compatível. Retornado somente pelo iOS DRMNative Framework. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3364 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDeviceId  </span> </td> 
   <td colname="col3"> <p>A estrutura solicitou a ID do dispositivo, mas o valor retornado estava vazio. </p> <p>O usuário não deve marcar a caixa de seleção <span class="uicontrol"> Permitir identificadores para conteúdo protegido</span> nas configurações do Chrome. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3365 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncognitoModeNotAllowed  </span> </td> 
   <td colname="col3"> <p>Essa combinação navegador/plataforma não permite reprodução protegida por DRM no modo Incógnito. </p> <p>O software do distribuidor deve aconselhar o usuário a sair do modo Incognito ou usar um navegador diferente. Para obter mais informações, consulte <a href="https://forums.adobe.com/thread/1266622" format="https" scope="external"> Erro de DRM 3365 causa e resolução</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3366 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadParameter  </span> </td> 
   <td colname="col3"> <p>O tempo de execução do host chamou a biblioteca de acesso com um parâmetro incorreto. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3367 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadSignature  </span> </td> 
   <td colname="col3"> Falha na assinatura do manifesto m3u8. Retornado somente pelo iOS DRMNative Framework ou AVE. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3368 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UserSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>O usuário cancelou a operação ou inseriu configurações que não permitem acesso ao sistema. </p> <p>Esse erro é lançado somente quando a versão do SWF é 19 ou posterior. Para compatibilidade com versões anteriores, 3321 é lançado quando o SWF é versão 18 ou anterior. </p> <p>O software do distribuidor deve guiar o usuário para uma explicação de como permitir o acesso de plug-in em caixa não restrita. Para obter mais informações, consulte <a href="https://helpx.adobe.com/adobe-access/kb/error-3321.html" format="html" scope="external"> Acesso à caixa de proteção do Google Chrome negado</a> e <a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Erro de DRM 3322/3346/3368 no Chrome (Problemas da Barra de Informações)</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3369 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InterfaceNotAvailable</span> </td> 
   <td colname="col3"> <p>Uma interface de navegador necessária não está disponível. Esse problema ocorre somente na Pepper. Pode haver uma incompatibilidade entre o plug-in do Flash e a versão do navegador. </p> <p>O software do distribuidor deve guiar o usuário para garantir que ele tenha a versão mais recente do navegador instalado. </p> <p> Se as incidências desse erro estiverem aumentando e corresponderem a uma atualização do navegador sendo lançada, escale para Adobe. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3370 </td> 
   <td colname="col2"><span class="codeph"> AXS_ContentIdSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>O usuário desabilitou a configuração <span class="uicontrol"> Permitir identificadores para conteúdo protegido</span>. </p> <p>Dica:  Este erro apareceu com as versões Pepper 13.0.0.x ou superior. </p> <p>O software do distribuidor deve guiar o usuário para ativar a configuração <span class="uicontrol"> Permitir identificadores para conteúdo protegido</span>. </p> <p>A equipe de operações do distribuidor deve guiar o usuário para ativar a configuração <span class="uicontrol"> Permitir identificadores para conteúdo protegido</span>. </p> <p>Para obter mais informações, consulte <a href="https://forums.adobe.com/message/6518323#6518323" format="https" scope="external"> https://forums.adobe.com/message/6518323#6518323</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3371 </td> 
   <td colname="col2"><span class="codeph"> AAXS_</span><span class="codeph"> NoOPConstraintInPixelConstraints</span> </td> 
   <td colname="col3"> <p>Resolução malformada com base nas restrições de proteção de saída na licença. </p> <p>O software do distribuidor deve exibir uma mensagem de erro. Peça ao usuário para relatar o problema ao distribuidor com um título de conteúdo. </p> <p>O distribuidor deve reempacotar o conteúdo com uma política válida. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3372 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ResolutionLargerThanMaxResolution</span> </td> 
   <td colname="col3"> <p>A resolução do conteúdo é maior que a resolução máxima especificada na restrição de proteção de saída. </p> <p>Se a equipe de operações do distribuidor detectar esse erro em seus registros, ele deverá revisar a política de proteção de saída baseada em resolução e, se necessário, reempacotar o conteúdo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3373 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_DisplayResolutionLargerThanConstrim</span> </td> 
   <td colname="col3"> <p>A resolução do conteúdo é maior do que a resolução especificada pela restrição de proteção de saída atualmente ativa. </p> <p>Se a equipe de operações do distribuidor detectar esse erro em seus registros, ele deverá revisar a política de proteção de saída baseada em resolução e, se necessário, reempacotar o conteúdo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3374 </td> 
   <td colname="col2"><span class="codeph"> AXS_MinorErr_ClientCommProcessFailed</span> </td> 
   <td colname="col3"> <p>Falha durante o processamento de comunicação no lado do cliente, por exemplo, geração de solicitação, processamento de resposta, token de autenticação incorreto e assim por diante. </p> <p>Se a equipe de operações do distribuidor detectar esse erro em seus registros, ele deverá revisar a política de proteção de saída baseada em resolução e, se necessário, reempacotar o conteúdo. </p> </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: Valores de reprodução de vídeo {#section_7079501250C2487499639F92EC774525}

A interface do Video Encoder do AVE retorna essas notificações de reprodução de vídeo no objeto de metadados `NATIVE_ERROR` .

<table id="table_5EEB1F60E5854452A8B0BABBE9B32651"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Valor da chave de metadados NATIVE_ERROR_CODE</b></th> 
   <th colname="col2" class="entry"><b>Valor da chave de metadados NATIVE_ERROR_NAME</b></th> 
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
   <td colname="col1"> 3 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> Operação assíncrona. A solicitação de operação foi feita. As informações de sucesso/falha estarão disponíveis mais tarde. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> A operação não é possível devido à condição de fim de arquivo (EOF). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> DECODER_FAILED</span> </td> 
   <td colname="col3"> O decodificador falhou no tempo de execução. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> DEVICE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Falha ao abrir o decodificador de hardware. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> FILE_NOT_FOUND  </span> </td> 
   <td colname="col3"> Não é possível localizar o recurso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> GENERIC_ERROR  </span> </td> 
   <td colname="col3"> Erro genérico. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> IRRECOVERABLE_ERROR  </span> </td> 
   <td colname="col3"> Uma condição de erro da qual o Mecanismo de vídeo não pode se recuperar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERABLE  </span> </td> 
   <td colname="col3"> Erro de rede, tentando recuperar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> NO_FIXED_SIZE  </span> </td> 
   <td colname="col3"> O tamanho do recurso não pode ser determinado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10º </td> 
   <td colname="col2"><span class="codeph"> NOT_IMPLEMENTED  </span> </td> 
   <td colname="col3"> Recurso não implementado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11º </td> 
   <td colname="col2"><span class="codeph"> OUT_OF_MEMORY  </span> </td> 
   <td colname="col3"> Memória insuficiente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12º </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR  </span> </td> 
   <td colname="col3"> Erro ao analisar o arquivo de mídia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13º </td> 
   <td colname="col2"><span class="codeph"> SIZE_UNKNOWN  </span> </td> 
   <td colname="col3"> O recurso tem um tamanho, mas é desconhecido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14. </td> 
   <td colname="col2"><span class="codeph"> SOB_FLUXO  </span> </td> 
   <td colname="col3"> Condição de subfluxo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15. </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_CONFIG  </span> </td> 
   <td colname="col3"> A configuração não é suportada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16º </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_OPERATION  </span> </td> 
   <td colname="col3"> Operação não suportada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17º </td> 
   <td colname="col2"><span class="codeph"> WAITING_FOR_INIT  </span> </td> 
   <td colname="col3"> Ainda não inicializado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18º </td> 
   <td colname="col2"><span class="codeph"> INVALID_PARAMETER  </span> </td> 
   <td colname="col3"> Parâmetro inválido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 19º </td> 
   <td colname="col2"><span class="codeph"> INVALID_OPERATION</span> </td> 
   <td colname="col3"> Operação não permitida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 20º </td> 
   <td colname="col2"><span class="codeph"> OP_ONLY_ALLOWED_IN_PAUSED_STATE</span> </td> 
   <td colname="col3"> A operação só é permitida durante uma pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21º </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> A operação não pode ser usada somente em arquivos de áudio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22º </td> 
   <td colname="col2"><span class="codeph"> PREVIOUS_STEP_SEEK_IN_PROGRESS</span> </td> 
   <td colname="col3"> A operação de busca anterior ainda está em andamento. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23º </td> 
   <td colname="col2"><span class="codeph"> SOURCE_NOT_SPECIFIED  </span> </td> 
   <td colname="col3"> Recurso não especificado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24º </td> 
   <td colname="col2"><span class="codeph"> RANGE_ERROR</span> </td> 
   <td colname="col3"> O valor especificado está fora do intervalo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25. </td> 
   <td colname="col2"><span class="codeph"> INVALID_SEEK_TIME</span> </td> 
   <td colname="col3"> Tempo de busca inválido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26º </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> O arquivo especificado não está em conformidade com a sintaxe esperada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27º </td> 
   <td colname="col2"><span class="codeph"> COMPONENT_CREATION_FAILURE</span> </td> 
   <td colname="col3"> Não foi possível criar um componente essencial. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28º </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> Falha ao criar contexto DRM. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29º </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORTED  </span> </td> 
   <td colname="col3"> Não há suporte para o tipo de contêiner. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30º </td> 
   <td colname="col2"><span class="codeph"> SEEK_FAILED</span> </td> 
   <td colname="col3"> Falha na busca. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31º </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Codec não suportado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32º </td> 
   <td colname="col2"><span class="codeph"> NETWORK_UNAVAILABLE</span> </td> 
   <td colname="col3"> A rede não está disponível. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33º </td> 
   <td colname="col2"><span class="codeph"> NETWORK_ERROR</span> </td> 
   <td colname="col3"> Erro ao obter dados da Rede. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34º </td> 
   <td colname="col2"><span class="codeph"> SOBREFLUXO</span> </td> 
   <td colname="col3"> Estouro. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35º </td> 
   <td colname="col2"><span class="codeph"> VIDEO_PROFILE_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Perfil de vídeo não suportado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36º </td> 
   <td colname="col2"><span class="codeph"> PERIOD_NOT_LOADED</span> </td> 
   <td colname="col3"> Tentou-se uma operação em um período de espera ou em um período que ainda não foi carregado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37º </td> 
   <td colname="col2"><span class="codeph"> INVALID_REPLACE_DURATION</span> </td> 
   <td colname="col3"> A duração de substituição especificada é inválida ou ultrapassa o fim do fluxo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38º </td> 
   <td colname="col2"><span class="codeph"> CALLED_FROM_WRONG_THREAD</span> </td> 
   <td colname="col3"> A API não pode ser chamada do thread errado. Principalmente para elementos de API que devem ser chamados somente do thread principal. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39º </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> Erro de leitura do fragmento. Não há failover presente. O mecanismo tentará ler o próximo fragmento. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40º </td> 
   <td colname="col2"><span class="codeph"> ABORTADO</span> </td> 
   <td colname="col3"> A operação foi abortada por uma chamada Cancelar ou Destruir explícita. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41º </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_HLS_VERSION</span> </td> 
   <td colname="col3"> Não é possível reproduzir esta versão da mídia HLS. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42º </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> Não é possível fazer failover. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43º </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> O download HTTP atingiu o tempo limite. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44º </td> 
   <td colname="col2"><span class="codeph"> NETWORK_DOWN  </span> </td> 
   <td colname="col3"> A conexão de rede do usuário está inativa. A reprodução pode parar a qualquer momento e será retomada quando a conexão estiver disponível. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45º </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> Nenhum perfil de taxa de bits utilizável encontrado no fluxo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46º </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> O manifesto tem uma assinatura incorreta. Falha no teste de assinatura do manifesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47º </td> 
   <td colname="col2"><span class="codeph"> CANNOT_LOAD_PLAYLIST</span> </td> 
   <td colname="col3"> Não é possível carregar uma lista de reprodução. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48º </td> 
   <td colname="col2"><span class="codeph"> REPLACEMENT_FAILED</span> </td> 
   <td colname="col3"> A substituição especificada em uma API de inserção não pôde ser bem-sucedida. Isso significa que a inserção foi bem-sucedida, mas a substituição não foi bem-sucedida. A substituição pode falhar se o manifesto a ser substituído tiver sido removido da linha do tempo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49º </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_ASYMMETRIC_PROFILE</span> </td> 
   <td colname="col3"> O DRM está alternando para um perfil assimétrico. Espera-se que todos os perfis estejam alinhados na duração. Caso contrário, esse aviso será lançado e poderá haver saltos na reprodução. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50º </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_BACKWARD</span> </td> 
   <td colname="col3"> Espera-se que a janela ativa avance apenas. Caso contrário, esse aviso será lançado e a janela não será lida. Por causa disso, pode haver saltos (ou parada/pausa longa) na reprodução. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51º </td> 
   <td colname="col2"><span class="codeph"> CURRENT_PERIOD_EXPIRED</span> </td> 
   <td colname="col3"> Janela ativa movida para além do período atual. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52º </td> 
   <td colname="col2"><span class="codeph"> CONTENT_LENGTH_MISMATCH</span> </td> 
   <td colname="col3"> O comprimento do conteúdo relatado pelo servidor HTTP não correspondia ao tamanho real da mídia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53º </td> 
   <td colname="col2"><span class="codeph"> PERIOD_HOLD</span> </td> 
   <td colname="col3"> O leitor de mídia não pode ler mais porque atingiu o tempo definido pela API setholdAt. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> LIVE_HOLD  </span> </td> 
   <td colname="col3">O leitor de mídia não pode carregar segmentos porque atingiu o fim da janela ativa. O carregamento do segmento será retomado quando o servidor adicionar nova mídia à janela ativa. Esse estado geralmente é alcançado se: 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48">O <span class="codeph"> bufferTime</span> é muito alto (igual ou superior à duração da janela ativa). </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">Uma combinação de uma ou mais API de inserção/exclusão substituiu mais mídia do que adicionou. </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">O próximo período é um período em tempo real com uma substituição de mídia pendente (devido à chamada à API InsertBy) </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEAVING  </span> </td> 
   <td colname="col3"> A intercalação de áudio e vídeo na mídia não é feita corretamente. Este é um erro de empacotamento. O aviso é despachado quando a diferença excede dois segundos. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56º </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57º </td> 
   <td colname="col2"><span class="codeph"> PLAYBACK_NOT_AUTHORIZED</span> </td> 
   <td colname="col3"> A reprodução de HLS não foi ativada no Flash Player. Consulte AuthorizedFeatures.enableHLSPlayback. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78º </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> O decodificador recebeu uma amostra inválida que não pode ser decodificada. Geralmente, esse não é um erro fatal, mas indica que pode haver falhas no áudio/vídeo. Muitas instâncias desse erro indicam uma codificação incorreta ou um arquivo inválido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> Após o início da reprodução, o intervalo Inserir/Substituir não deve conter o cabeçalho de leitura. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60º </td> 
   <td colname="col2"><span class="codeph"> POSTROLL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> As inserções posteriores não são permitidas em uma mídia ao vivo. No entanto, eles são permitidos depois que o servidor marcar a mídia como concluída. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81º </td> 
   <td colname="col2"><span class="codeph"> INTERNAL_ERROR</span> </td> 
   <td colname="col3"> Um assunto muito raro que nunca deveria acontecer. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62º </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> O fluxo não segue a recomendação de embalagem de sempre colocar H264 SPS/PPS em um AVCC. Problemas de busca/reprodução podem ser vistos. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63º </td> 
   <td colname="col2"><span class="codeph"> PARAL_REPLACEMENT</span> </td> 
   <td colname="col3"> A substituição especificada em uma API de inserção foi feita apenas parcialmente. Isso acontece quando replaceDuration passa pela duração da linha do tempo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64º </td> 
   <td colname="col2"><span class="codeph"> RENDITION_M3U8_ERROR</span> </td> 
   <td colname="col3"> Erro ao carregar a lista de reprodução de representação. Isso é somente para AVE, não para FlashPlayer. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65º </td> 
   <td colname="col2"><span class="codeph"> NULL_OPERATION</span> </td> 
   <td colname="col3"> A operação não faz nada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66º </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SKIPPED_ON_FAILURE</span> </td> 
   <td colname="col3"> O segmento não pode ser reproduzido e é ignorado na falha. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67º </td> 
   <td colname="col2"><span class="codeph"> INCOMPATIBLE_RENDER_MODE</span> </td> 
   <td colname="col3"> Modo de renderização incompatível. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68º </td> 
   <td colname="col2"><span class="codeph"> PROTOCOL_NOT_SUPPORTED  </span> </td> 
   <td colname="col3"> Não há suporte para o protocolo Web usado no URL. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69º </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPATIBLE_VERSION</span> </td> 
   <td colname="col3"> Erro ao analisar o arquivo de mídia. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70º </td> 
   <td colname="col2"><span class="codeph"> MANIFEST_FILE_UNEXPECTEDLY_CHANGED</span> </td> 
   <td colname="col3"> O arquivo de manifesto foi alterado de maneira inesperada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71º </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> Não é possível executar uma operação de divisão em uma linha do tempo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72º </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> Não é possível executar uma operação de apagamento em uma linha do tempo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73º </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_GET_NEXT_FRAGMENT</span> </td> 
   <td colname="col3"> Não recebeu o próximo fragmento. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74º </td> 
   <td colname="col2"><span class="codeph"> NO_TIMELINE</span> </td> 
   <td colname="col3"> Nenhuma linha do tempo presente em uma estrutura de dados interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> LISTENER_NOT_FOUND</span> </td> 
   <td colname="col3"> Nenhum ouvinte encontrado em uma estrutura de dados interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76º </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> Não é possível iniciar o áudio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77º </td> 
   <td colname="col2"><span class="codeph"> NO_AUDIO_SINK</span> </td> 
   <td colname="col3"> Nenhum dissipador de áudio presente em uma estrutura de dados interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78º </td> 
   <td colname="col2"><span class="codeph"> FILE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Não é possível abrir o arquivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79º </td> 
   <td colname="col2"><span class="codeph"> FILE_WRITE_ERROR</span> </td> 
   <td colname="col3"> Não é possível gravar em um arquivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80º </td> 
   <td colname="col2"><span class="codeph"> FILE_READ_ERROR</span> </td> 
   <td colname="col3"> Não é possível ler a partir de um ficheiro. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81º </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> Erro ao analisar os dados do ID3. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> SECURITY_ERROR  </span> </td> 
   <td colname="col3"> Falha ao carregar o conteúdo devido a restrições de segurança. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> TIMELINE_TOO_SHORT</span> </td> 
   <td colname="col3"> A duração da linha do tempo é muito curta. Se esse for um stream ao vivo, pode haver buffering frequente. </td> 
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
   <td colname="col2"><span class="codeph"> KEY_NOT_FOUND  </span> </td> 
   <td colname="col3"> Não é possível localizar a chave. </td> 
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
   <td colname="col1"> 90º </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> Não é possível processar a atualização do manifesto principal. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91º </td> 
   <td colname="col2"> <span class="codeph"> UNREPORTED_TIME_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> Descontinuidade de tempo não relatado (PTS) encontrada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 92 </td> 
   <td colname="col2"> <span class="codeph"> UNMATCHED_AV_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> Descontinuidade de áudio e vídeo inigualável encontrada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 93 </td> 
   <td colname="col2"><span class="codeph"> TRICKPLAY_ENDED_DUE_TO_ERROR</span> </td> 
   <td colname="col3">Erro ao reproduzir mídia no modo <i>trick play</i>. O modo Trick play é encerrado e o fluxo é pausado. Chame <span class="codeph"> Play()</span> para reproduzir a mídia no modo normal. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 95 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_AHEAD</span> </td> 
   <td colname="col3"> O reprodutor está fora da janela ao vivo e deve procurar para recuperar o atraso. </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: Valores de criptografia {#section_39365E545CAC49B9A4D4678657BB2155}

O módulo de criptografia do mecanismo de vídeo do Adobe retorna essas notificações no objeto de metadados `NATIVE_ERROR` .

| **Valor da chave de metadados NATIVE_ERROR_CODE** | **Valor da chave de metadados NATIVE_ERROR_NAME** | **Significado** |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | O algoritmo que está sendo usado não é suportado. |
| 301º | `CRYPTO_ERROR_CORRUPTED_DATA` | Os dados estão corrompidos. |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | Buffer muito pequeno. |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | Certificado incorreto. |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | Atualização do resumo. |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | Término do resumo. |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | Parâmetro incorreto. |
