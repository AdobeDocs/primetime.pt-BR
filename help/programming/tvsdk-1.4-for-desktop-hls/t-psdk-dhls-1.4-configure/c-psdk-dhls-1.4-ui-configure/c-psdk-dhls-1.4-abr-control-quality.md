---
description: Os fluxos HLS e DASH fornecem codificações (perfis) de taxa de bits diferentes para a mesma sequência curta de vídeo. O TVSDK pode selecionar o nível de qualidade para cada rajada com base na largura de banda disponível.
seo-description: Os fluxos HLS e DASH fornecem codificações (perfis) de taxa de bits diferentes para a mesma sequência curta de vídeo. O TVSDK pode selecionar o nível de qualidade para cada rajada com base na largura de banda disponível.
seo-title: Taxas de bits adaptáveis (ABR) para qualidade de vídeo
title: Taxas de bits adaptáveis (ABR) para qualidade de vídeo
uuid: e3d5ef90-067d-48e0-a025-081de931d842
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Taxas de bits adaptáveis (ABR) para qualidade de vídeo{#adaptive-bit-rates-abr-for-video-quality}

Os fluxos HLS e DASH fornecem codificações (perfis) de taxa de bits diferentes para a mesma sequência curta de vídeo. O TVSDK pode selecionar o nível de qualidade para cada rajada com base na largura de banda disponível.

O TVSDK monitora constantemente a taxa de bits para garantir que o conteúdo seja reproduzido na taxa de bits ideal para a conexão de rede atual.

Você pode definir a política de switching de taxa de bits adaptável (ABR) e as taxas de bits inicial, mínima e máxima para um fluxo de taxa de bits múltipla (MBR). O TVSDK muda automaticamente para a taxa de bits que fornece a melhor experiência de reprodução na configuração especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Taxa de bits inicial </td> 
   <td colname="col2"> <p>A taxa de bits de reprodução desejada (em bits por segundo) para o primeiro segmento. Quando a reprodução é iniciada, o perfil mais próximo, que é igual ou maior à taxa de bits inicial, é usado para o primeiro segmento. </p> <p> Se uma taxa de bits mínima for definida e a taxa de bits inicial for inferior à taxa mínima, o TVSDK selecionará o perfil com a taxa de bits mais baixa acima da taxa de bits mínima. Se a taxa inicial estiver acima da taxa máxima, o TVSDK selecionará a taxa mais alta abaixo da taxa máxima. </p> <p>Se a taxa de bits inicial for zero ou indefinida, a taxa de bits inicial será determinada pela política ABR. </p> <p> <span class="apiname"> ABRInitialBitRate </span> retorna um valor inteiro que representa o perfil byte por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Taxa mínima de bits </td> 
   <td colname="col2"> <p>A menor taxa de bits permitida para a qual o ABR pode alternar. A alternância ABR ignora perfis com uma taxa de bits inferior a essa taxa de bits. </p> <p> <span class="apiname"> ABRMinBitRate </span> retorna um valor inteiro que representa o perfil bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Taxa máxima de bits </td> 
   <td colname="col2"> <p>A maior taxa de bits permitida para a qual o ABR pode alternar. A alternância ABR ignora perfis com uma taxa de bits superior a essa taxa de bits. </p> <p> <span class="apiname"> ABRMaxBitRate </span> retorna um valor inteiro que representa o perfil bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Política de comutação ABR </td> 
   <td colname="col2"> A reprodução alterna gradualmente para o perfil de taxa de bits mais alta quando possível. Você pode definir a política para a alternância ABR, que determina a velocidade de alternância de TVSDK entre perfis. O padrão é <span class="codeph"> MODERATE_POLICY </span>. <p>Quando o TVSDK decide alternar para uma taxa de bits mais alta, o player seleciona o perfil de taxa de bits ideal para alternar com base na política ABR atual: 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> CONSERVATIVE_POLICY </span>: Alterna para o perfil com a próxima taxa de bits mais alta quando a largura de banda for 50% mais alta do que a taxa de bits atual. </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MODERATE_POLICY </span>: Alterna para o próximo perfil de taxa de bits mais alta quando a largura de banda for 20% mais alta do que a taxa de bits atual. </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> AGRESSIVE_POLICY </span>: Alterna imediatamente para o perfil de taxa de bits mais alto quando a largura de banda for maior que a taxa de bits atual. </li> 
     </ul> </p> <p>Se a taxa de bits inicial for zero ou não for especificada, mas uma política for especificada, a reprodução começará com o perfil de taxa de bits mais baixo para conservador, o perfil mais próximo da taxa de bits mediana dos perfis disponíveis para moderado e o perfil de taxa de bits mais alto para agressivo. </p> <p>A política funciona nas restrições das taxas de bits mínimas e máximas, se essas taxas forem especificadas. </p> <p> <span class="codeph"> ABRPolicy </span> retorna a configuração atual da enumeração <span class="codeph"> ABRControlParameters </span> : CONSERVATIVE_POLICY, MODERATE_POLICY ou AGRESSIVE_POLICY. </p> </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se das seguintes informações:

* O mecanismo de failover TVSDK pode substituir suas configurações, pois o TVSDK favorece uma experiência de reprodução contínua em vez de seguir rigorosamente seus parâmetros de controle.
* Quando a taxa de bits muda, o TVSDK é despachado `ProfileEvent.PROFILE_CHANGED`.
* Você pode alterar as configurações de ABR a qualquer momento, e o player muda para usar o perfil que mais corresponde às configurações mais recentes.

Por exemplo, se um fluxo tiver os seguintes perfis:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se você especificar um intervalo de 300000 a 2000000, o TVSDK considerará somente os perfis 1, 2 e 3. Isso permite que os aplicativos se ajustem a várias condições de rede, como mudar de wi-fi para 3G ou para vários dispositivos, como telefone, tablet ou desktop.

Para definir parâmetros de controle ABR, siga um destes procedimentos:

* Use a classe `ABRControlParameterBuilder` helper para definir qualquer subconjunto dos parâmetros (opera em segundo plano `ABRControlParameter` )

* Defina os parâmetros na `ABRControlParameter` classe.

## Configure as taxas de bits adaptáveis usando ABRControlParametersBuilder {#section_3DDE397A7CE445E1832EBAA46CE5C069}

Usar a classe `ABRControlParametersBuilder` helper é a maneira mais simples e eficiente de definir parâmetros ABR.

* O `ABRControlParametersBuilder` construtor define todos os parâmetros ABR como valores padrão no `ABRControlParameters` objeto subjacente.

* Você pode redefinir parâmetros ABR individuais durante o tempo de execução, desde que mantenha uma referência à mesma `ABRControlParametersBuilder` instância.

Essa classe também inclui o método `toABRControlParameters()` helper. Use esse método para obter uma instância do `ABRControlParameters` e defini-la na `mediaPlayer.ABRControlParameters` propriedade. Isso faz com que suas configurações entrem em vigor no player.

1. Instancie a classe `ABRControlParametersBuilder` helper e defina os parâmetros no Media Player.

   >[!NOTE]
   >
   >Por exemplo, a amostra a seguir inicializa todos os parâmetros para os padrões, em seguida, define somente a política como conservadora e restringe a taxa de bits máxima para 1000000:    >
   >
   >
   ```>
   >var abrBuilder:ABRControlParametersBuilder =  
   >   new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >   abrBuilder.toABRControlParameters();
   >```   >
   >



1. Modifique os parâmetros ABR individuais em tempo de execução.

   Para modificar parâmetros individuais deixando o restante dos parâmetros como eram:

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   Para manter as configurações anteriores, é necessário manter uma referência à mesma `ABRControlParametersBuilder` instância criada na Etapa 1.

## Configure as taxas de bits adaptáveis usando ABRControlParameters {#section_02161FD0A73F40ED9CAE17F9AF850483}

Você pode definir valores de controle ABR somente com `ABRControlParameters`, mas pode criar um novo a qualquer momento.

Essa capacidade de definir parâmetros ABR era suportada antes da existência da `ABRControlParametersBuilder` classe, mas essa capacidade ainda é eficaz para definir parâmetros ABR no momento da construção. No entanto, para alterar parâmetros individuais após a construção, você deve usar a `ABRControlParametersBuilder` classe.

As seguintes condições aplicam-se a `ABRControlParameters`:

* Você deve fornecer valores para todos os parâmetros no momento da construção.
* Não é possível alterar valores individuais após o tempo de construção.
* Se os parâmetros especificados estiverem fora do intervalo permitido, um `ArgumentError` será lançado.

1. Decida sobre as taxas de bits inicial, mínima e máxima.
1. Determine a política ABR:

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. Defina os valores dos parâmetros ABR no `ABRControlParameters` construtor e atribua-os ao Media Player.

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```

