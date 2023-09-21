---
description: Os fluxos HLS e DASH fornecem codificações (perfis) de taxa de bits diferentes para a mesma intermitência curta de vídeo. O TVSDK pode selecionar o nível de qualidade para cada intermitência com base na largura de banda disponível.
title: Taxas de bits adaptáveis (ABR) para qualidade de vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---

# Taxas de bits adaptáveis (ABR) para qualidade de vídeo{#adaptive-bit-rates-abr-for-video-quality}

Os fluxos HLS e DASH fornecem codificações (perfis) de taxa de bits diferentes para a mesma intermitência curta de vídeo. O TVSDK pode selecionar o nível de qualidade para cada intermitência com base na largura de banda disponível.

O TVSDK monitora constantemente a taxa de bits para garantir que o conteúdo seja reproduzido na taxa de bits ideal para a conexão de rede atual.

Você pode definir a política de switching ABR (taxa de bits adaptável) e as taxas de bits inicial, mínima e máxima para um fluxo MBR (taxa de vários bits). O TVSDK alterna automaticamente para a taxa de bits que fornece a melhor experiência de reprodução na configuração especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Taxa de bits inicial </td> 
   <td colname="col2"> <p>A taxa de bits de reprodução desejada (em bits por segundo) para o primeiro segmento. Quando a reprodução começa, o perfil mais próximo, que é igual ou maior que a taxa de bits inicial, é usado para o primeiro segmento. </p> <p> Se uma taxa de bits mínima for definida e a taxa de bits inicial for menor que a taxa mínima, o TVSDK selecionará o perfil com a taxa de bits mais baixa acima da taxa de bits mínima. Se a taxa inicial estiver acima da taxa máxima, o TVSDK selecionará a taxa mais alta abaixo da taxa máxima. </p> <p>Se a taxa de bits inicial for zero ou indefinida, a taxa de bits inicial será determinada pela política ABR. </p> <p> <span class="apiname"> ABRInitialBitRate </span> retorna um valor inteiro que representa o perfil byte por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Taxa de bits mínima </td> 
   <td colname="col2"> <p>A taxa de bits mais baixa permitida para a qual o ABR pode alternar. A switching ABR ignora perfis com uma taxa de bits inferior a essa taxa de bits. </p> <p> <span class="apiname"> ABRMinBitRate </span> retorna um valor inteiro que representa o perfil de bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Taxa de bits máxima </td> 
   <td colname="col2"> <p>A taxa de bits mais alta permitida para a qual o ABR pode alternar. A switching ABR ignora perfis com uma taxa de bits superior a essa taxa de bits. </p> <p> <span class="apiname"> ABRMaxBitRate </span> retorna um valor inteiro que representa o perfil de bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Política de comutação ABR </td> 
   <td colname="col2"> A reprodução alterna gradualmente para o perfil com a taxa de bits mais alta, quando possível. Você pode definir a política de switching ABR, que determina a rapidez com que o TVSDK alterna entre perfis. O padrão é <span class="codeph"> MODERATE_POLICY </span>. <p>Quando o TVSDK decide mudar para uma taxa de bits mais alta, o player seleciona o perfil de taxa de bits ideal para mudar com base na política ABR atual: 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> CONSERVATIVE_POLICY </span>: Alterna para o perfil com a próxima taxa de bits mais alta quando a largura de banda for 50% mais alta do que a taxa de bits atual. </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MODERATE_POLICY </span>: Alterna para o próximo perfil de taxa de bits mais alta quando a largura de banda for 20% mais alta do que a taxa de bits atual. </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> POLÍTICA_AGRESSIVA </span>: Alterna imediatamente para o perfil de taxa de bits mais alta quando a largura de banda for maior que a taxa de bits atual. </li> 
     </ul> </p> <p>Se a taxa de bits inicial for zero ou não for especificada, mas uma política for especificada, a reprodução começará com o perfil de taxa de bits mais baixa para conservador, o perfil mais próximo da taxa de bits mediana dos perfis disponíveis para moderado e o perfil de taxa de bits mais alta para agressivo. </p> <p>A política funciona nas restrições das taxas de bits mínima e máxima, se essas taxas forem especificadas. </p> <p> <span class="codeph"> ABRPolicy </span> retorna a configuração atual da variável <span class="codeph"> ABRControlParameters </span> enum: CONSERVATIVE_POLICY, MODERATE_POLICY ou AGGRESSIVE_POLICY. </p> </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se das seguintes informações:

* O mecanismo de failover do TVSDK pode substituir suas configurações, pois o TVSDK favorece uma experiência de reprodução contínua em vez de seguir estritamente os parâmetros de controle.
* Quando a taxa de bits muda, o TVSDK envia `ProfileEvent.PROFILE_CHANGED`.
* Você pode alterar as configurações do ABR a qualquer momento e o reprodutor alterna para usar o perfil que melhor corresponde às configurações mais recentes.

Por exemplo, se um fluxo tiver os seguintes perfis:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se você especificar um intervalo de 300000 a 2000000, o TVSDK considerará somente os perfis 1, 2 e 3. Isso permite que os aplicativos se ajustem a várias condições de rede, como alternar de wi-fi para 3G ou para vários dispositivos, como um telefone, um tablet ou um desktop.

Para definir parâmetros de controle ABR, siga um destes procedimentos:

* Use o `ABRControlParameterBuilder` classe auxiliar para definir qualquer subconjunto dos parâmetros (opera em `ABRControlParameter` nos bastidores)

* Defina os parâmetros no `ABRControlParameter` classe.

## Configurar taxas de bits adaptáveis usando ABRControlParametersBuilder {#section_3DDE397A7CE445E1832EBAA46CE5C069}

Usar o `ABRControlParametersBuilder` A classe auxiliar é a maneira mais simples e eficiente de definir parâmetros ABR.

* A variável `ABRControlParametersBuilder` construtor define todos os parâmetros ABR para valores padrão na base `ABRControlParameters` objeto.

* Você pode redefinir parâmetros ABR individuais durante o tempo de execução, desde que mantenha uma referência à mesma `ABRControlParametersBuilder` instância.

Esta classe inclui também a `toABRControlParameters()` método auxiliar. Use este método para obter uma instância de `ABRControlParameters` e defina-o no `mediaPlayer.ABRControlParameters` propriedade. Isso faz com que suas configurações entrem em vigor no reprodutor.

1. Instanciar o `ABRControlParametersBuilder` e defina os parâmetros no reprodutor de mídia.

   >[!NOTE]
   >
   >Por exemplo, a amostra a seguir inicializa todos os parâmetros para os padrões e, em seguida, define apenas a política como conservadora e restringe a taxa máxima de bits a 1000000:
   >
   >```
   >var abrBuilder:ABRControlParametersBuilder =  
   >   new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >   abrBuilder.toABRControlParameters();
   >```
   >

1. Modificar parâmetros ABR individuais em tempo de execução.

   Para modificar parâmetros individuais, deixando o restante dos parâmetros como estavam:

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   Para manter as configurações anteriores, é necessário manter uma referência à mesma `ABRControlParametersBuilder` criada na Etapa 1.

## Configurar taxas de bits adaptáveis usando ABRControlParameters {#section_02161FD0A73F40ED9CAE17F9AF850483}

Você pode definir valores de controle ABR somente com `ABRControlParameters`, mas é possível construir um novo a qualquer momento.

Esta capacidade de definir parâmetros ABR era suportada antes da existência do `ABRControlParametersBuilder` classe, mas essa capacidade ainda é eficaz para definir parâmetros ABR no momento da construção. No entanto, para alterar parâmetros individuais após a construção, você deve usar o `ABRControlParametersBuilder` classe.

As seguintes condições se aplicam a `ABRControlParameters`:

* Você deve fornecer valores para todos os parâmetros no momento da construção.
* Não é possível alterar valores individuais após o tempo de construção.
* Se os parâmetros especificados estiverem fora do intervalo permitido, uma variável `ArgumentError` é lançado.

1. Decida sobre as taxas de bits inicial, mínima e máxima.
1. Determine a política ABR:

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. Defina os valores do parâmetro ABR no `ABRControlParameters` e atribua-os ao reprodutor de mídia.

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```
