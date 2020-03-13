---
seo-title: Referência de propriedades do servidor
title: Referência de propriedades do servidor
uuid: 24a187fe-9b7d-411f-a358-d10c70a5dd0e
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Referência de propriedades do servidor{#server-properties-reference}

<!--<a id="section_EC8810492A454BDBA6013FE376360F4E"></a>-->

## Servidor de individualização

<table id="table_ats_tk2_jr">  
 <thead> 
  <tr> 
   <th class="entry"> Configuração </th> 
   <th class="entry"> Descrição </th> 
   <th class="entry"> Exemplo </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> Credencial de transporte </td> 
   <td>A credencial de transporte é usada para descriptografar solicitações recebidas do cliente e assinar as respostas enviadas de volta. Certifique-se de configurar o arquivo <span class="filepath"> AdobeInitial.properties</span> adequadamente com o caminho para o arquivo de credencial de transporte, bem como a senha PKCS12 criptografada. </td> 
   <td> 
    <ul id="ul_itx_fl2_jr"> 
     <li id="li_A2E65253F37245268A41E6B9C958C8DF"><span class="codeph"> cert.i15n.transport.file = </span> [arquivo PKCS12 contendo o certificado e a chave de transporte de individualização] </li> 
     <li id="li_28CDFC0B3D684795AF4708B6D26DF83F"><span class="codeph"> cert.i15n.transport.password =</span> [Senha criptografada para o arquivo PKCS12] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Credencial da CA de individualização </td> 
   <td>O servidor de individualização usa a credencial da CA de individualização para assinar os certificados da máquina que emite. Certifique-se de configurar o arquivo <span class="filepath"> AdobeInitial.properties</span> adequadamente com o caminho para o arquivo de credencial CA I15N, bem como a senha PKCS12 criptografada. </td> 
   <td> 
    <ul id="ul_xsj_nl2_jr"> 
     <li id="li_5A770D8A482F41A4A9AB63CA52C2EB90"><span class="codeph"> cert.i15n.ica.file =</span> [arquivo PKCS12 contendo o certificado e a chave da AC de individualização] </li> 
     <li id="li_C3C4A2D9AA2A4F86B6DDCFFD9CB55CBB"><span class="codeph"> cert.i15n.ica.password =</span> [Senha criptografada para o arquivo PKCS12] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Credencial de criptografia de individualização </td> 
   <td> O servidor de individualização usa a credencial de criptografia para criptografar arquivos confidenciais que precisam ser transmitidos aos servidores de individualização. Por exemplo, este certificado suporta a migração de licença e também é usado para criptografar as chaves privadas do DRM para os servidores de individualização. </td> 
   <td> 
    <ul id="ul_nbr_kpd_w5"> 
     <li id="li_4226AD6CC85740669DAF467EFD00BBBE"><span class="codeph"> cert.i15n.decryption.file=i15n_transport.pfx</span> </li> 
     <li id="li_F51BDD94F4724FA58CEF9470B6FEE33B"><span class="codeph"> cert.i15n.decryption.password=password</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Cache de conteúdo </td> 
   <td>Essas configurações controlam o local a partir do qual o servidor de individualização baixa o conteúdo e onde o conteúdo é armazenado em cache no disco. O servidor de individualização verificará o novo conteúdo no servidor de conteúdo uma vez na inicialização e, em seguida, na frequência/tempo especificado por essas propriedades. <p>Para o On Premise Individualization Server, incluímos um conjunto inicial de dados de cache de conteúdo. Certifique-se de copiar o <i>CONTEÚDO</i> da pasta de cache (não a pasta de cache propriamente dita) para o local configurado do AdobeInitial.properties <span class="filepath"></span> contentServer.localDirectory <span class="codeph"></span> . </p> </td> 
   <td> 
    <ul id="ul_r4n_1r2_jr"> 
     <li id="li_CA5F562577B04B4A9966EF46E039A137"><span class="codeph"> contentServer.localDirectory =</span> [Diretório no qual armazenar conteúdo local (normalmente tomcat/temp)] </li> 
     <li id="li_9A78FBD6C54D47708226378340B46E8E"><span class="codeph"> contentServer.server =</span> [Servidor Web para entrar em contato com informações ECI (<i>não suportado nesta versão</i>)] </li> 
     <li id="li_4E7D7F76085D411688B5003E855F860B"><span class="codeph"> contentServer.timeout =</span> [Tempo limite da conexão, em segundos] </li> 
     <li id="li_4B751F238A1643A7AC730CD9354887B6"><span class="codeph"> contentServer.pollFrequency =</span> [Com que frequência pesquisar o servidor, em dias (o mínimo é 1 dia)] </li> 
     <li id="li_8E23C3C6E7EF46B0AFDD7993DE79F142"><span class="codeph"> contentServer.pollTime =</span> [Hora do dia para pesquisar o servidor, em minutos desde a meia-noite] </li> 
    </ul> <p>Leia a seção Arquivos <i></i> CRL e ECI sobre como manter o cache atualizado. </p> </td> 
  </tr> 
  <tr> 
   <td> CRL da CA de individualização </td> 
   <td> <p>Este ponto de distribuição da Lista de Revogação de Certificado (CRL) está incluído em cada certificado de máquina emitido pelo servidor de Individualização. Durante a validação do certificado da máquina no servidor de licenças, a CRL será baixada do ponto de distribuição listado no certificado (ou lida do cache, se já tiver sido baixada) e verificada a certeza de que o certificado não foi revogado. É recomendável executar essa alteração na configuração do servidor após passar pelo processo de criação e implantação da CRL da CA de individualização. Reinicie o servidor Individualization após qualquer alteração de configuração. </p> <p>Para definir o URL do ponto de distribuição CRL, é necessário definir o campo <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> cert.machine.crldp</span> . </p> </td> 
   <td> 
    <ul id="ul_eq3_lv2_jr"> 
     <li id="li_5E37A9E318D742B6A5E1035120888819"><span class="codeph"> cert.machine.crldp =</span> [ponto de distribuição CRL] </li> 
    </ul> <p>Por exemplo: </p>
    <p> <code>
      cert.machine.crldp__DEV=<span>tps://onprem-individualization.com</span>CRL/onprem-individualization-ca.crl
     </code></p>
     <p>O License Server deve baixar automaticamente esta CRL, assim que uma solicitação de licença for processada. </p> <p importance="high">Observação: Este ponto de distribuição <i>não</i> foi verificado pelo Primetime DRM para a validade. Você deve verificar se este URL é válido. Os erros resultantes de um URL inválido não serão exibidos até que os erros de validação apareçam do servidor de licenças. </p> </td> 
  </tr> 
  <tr> 
   <td> Registro </td> 
   <td>Configure o <span class="filepath"> AdobeInitial.properties</span> para registro, conforme necessário. </td> 
   <td> 
    <ul id="ul_j1v_kw2_jr"> 
     <li id="li_B60002B33A3042FCBE1F694454966469"><span class="codeph"> adobe.weblogs.loc =</span> [Diretório no qual os arquivos de log serão criados] </li> 
     <li id="li_2DD4406FBBF047589BAAAE1C9082D8B3"><span class="codeph"> log.Level =</span> [O nível mais baixo das mensagens de log que podem aparecer nos logs <span class="codeph"> [DEBUG]| INFORMAÇÕES]</span> ] </li> 
     <li id="li_610FAF239A554CE59DAC455174F0CF0A"><span class="codeph"> log.FileName =</span> [Prefixo para arquivos de log. Data/hora e extensão ".log" serão adicionadas ao nome do arquivo] </li> 
     <li id="li_1F2913B209BE4A0E8207FAAD052D1764"><span class="codeph"> log.RollInterval =</span> [Especifica a frequência de rolagem dos logs.] </li> 
     <li id="li_3F46C15488114BB5B41035F710E7A19F"><span class="codeph"> log.RollSize =</span> [Roll the logs quando atingirem esse tamanho (os logs serão rolados quando o <span class="codeph"> RollInterval</span> ou o <span class="codeph"> RollSize</span> for atingido, o que ocorrer primeiro)] </li> 
     <li id="li_DA32E862F7B0413885DA20633B682484"><span class="codeph"> log.ReportLogging.Enabled =</span>[ [true| false ] Especifica se um arquivo separado deve ser gerado e que contenha dados usados pela Adobe para gerar relatórios de Individualização.] </li> 
     <li id="li_465CC6D81B8A484CBF4E7A39F7AF86AA"><span class="codeph"> log.ReportLogging.FileName =</span> [Prefixo para arquivos de log de relatório. A data/hora e a extensão <span class="filepath"> .log</span> serão adicionadas ao nome do arquivo. A propriedade l<span class="codeph"> og.Level</span> não se aplica a esse arquivo de log, mas <span class="codeph"> log.RollInterval</span> e <span class="codeph"> log.RollSize</span> se aplicam.] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Outros </td> 
   <td></td> 
   <td> 
    <ul id="ul_b3b_g1f_jr"> 
     <li id="li_FACF07CB332D416E91FD34DE48152FAA"><span class="codeph"> deviceinfo.key =</span> [Chave codificada Base64 criptografada usada para informações do dispositivo HMAC antes de incluí-la no token da máquina. A chave pode ser diferente para os ambientes de Desenvolvimento/armazenamento temporário/produção, mas deve ser a mesma para todos os servidores em um ambiente específico. ] </li> 
     <li id="li_B19C77FD6F91496294DBF836A1922EE1"><span class="codeph"> keys.kgs.server =</span> [Localização do Key Gen Server (um único host/porta, representando um pool de servidores chave)] </li> 
     <li id="li_5DA3C89770804B148EF6FAF01A5AD958"><span class="codeph"> keys.MinQueueSize =</span> [Procure outro lote de chaves do KGS quando houver tantas chaves restantes na fila] </li> 
     <li id="li_0C2E5F2FDB824182A6BE418B041D2F28"><span class="codeph"> status.Timeout =</span> [A página Status fará o ping no KGS para determinar se ele pode acessar o servidor. O tempo limite expirará se uma resposta não for recebida novamente no período especificado.] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Servidor de geração de chave {#section_37FA8EEBA258461F8CFA3ADF37714577}

<table id="table_ats_tk2_js"> 
 <thead> 
  <tr> 
   <th class="entry"> Configuração </th> 
   <th class="entry"> Descrição </th> 
   <th class="entry"> Exemplo </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> Geração de chave </td> 
   <td></td> 
   <td> 
    <ul id="ul_nlj_ydf_jr"> 
     <li id="li_E4347D572F004BF0B237A662BFE7F3ED"><span class="codeph"> kgs.Threads =</span> [Número de threads a serem usados para gerar chaves (deve ser igual ao número de processadores disponíveis na máquina)] </li> 
     <li id="li_EDBC2535D48E4A66AEB240DB337187FC"><span class="codeph"> kgs.BatchSize =</span> [Número de chaves a serem geradas por lote] </li> 
     <li id="li_07B41546D94F42349103BF8AF4605E14"><span class="codeph"> kgs.KeyDirectory =</span> [Diretório no qual armazenar arquivos de lote de chaves] </li> 
     <li id="li_F4962C97DC3D491DA7FAC826E38A4459"><span class="codeph"> kgs.MaxQueueSize =</span> [Número máximo de arquivos de lote de chaves a serem gerados] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Registro </td> 
   <td></td> 
   <td> 
    <ul id="ul_kwq_12f_jr"> 
     <li id="li_5E5D34FE5EB44BB898090494C7DDEBD8"><span class="codeph"> adobe.weblogs.loc =</span> [Diretório no qual os arquivos de log serão criados] </li> 
     <li id="li_0E34CD32CD5E47729B69B50414F93678"><span class="codeph"> log.FileName =</span> [Prefixo para arquivos de log. Data/hora e extensão <span class="filepath"> .log</span> serão adicionadas ao nome do arquivo] </li> 
     <li id="li_8AB15ACEC39041A2A04C7301154C6EDB"><span class="codeph"> log.Level =</span> [O nível mais baixo das mensagens de log que podem aparecer nos logs] </li> 
     <li id="li_A17E84DA3ED243F381FF3A6184A3CAA0"><span class="codeph"> log.RollInterval =</span> [Especifica a frequência de rolagem dos logs.] </li> 
     <li id="li_C2B3D111608945DA9D1428BE98D61664"><span class="codeph"> log.RollSize =</span> [Roll the logs quando atingirem esse tamanho (os logs serão rolados quando o <span class="codeph"> RollInterval</span> ou o <span class="codeph"> RollSize</span> for atingido, o que ocorrer primeiro)] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
