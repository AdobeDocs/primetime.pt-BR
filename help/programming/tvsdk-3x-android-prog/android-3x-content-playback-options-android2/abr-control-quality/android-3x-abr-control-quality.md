---
description: Os fluxos HLS e DASH fornecem codificações (perfis) de taxa de bits diferentes para a mesma intermitência curta de vídeo. O TVSDK pode selecionar o nível de qualidade para cada intermitência com base no nível de buffer atual e na largura de banda disponível.
title: Taxas de bits adaptáveis (ABR) para qualidade de vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# Visão geral {#adaptive-bit-rates-abr-for-video-quality-overview}

Os fluxos HLS e DASH fornecem codificações (perfis) de taxa de bits diferentes para a mesma intermitência curta de vídeo. O TVSDK pode selecionar o nível de qualidade para cada intermitência com base no nível de buffer atual e na largura de banda disponível.

O TVSDK monitora constantemente a taxa de bits para garantir que o conteúdo seja reproduzido na taxa de bits ideal para a conexão de rede atual. Você pode definir a política de switching ABR (taxa de bits adaptável) e as taxas de bits inicial, mínima e máxima para um fluxo MBR (taxa de vários bits). O TVSDK alterna automaticamente para a taxa de bits que fornece a melhor experiência de reprodução na configuração especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Taxa de bits inicial </td> 
   <td colname="col2"> <p>A taxa de bits de reprodução desejada (em bits por segundo) para o primeiro segmento. </p> <p>Quando a reprodução começa, o perfil mais próximo, que é igual ou maior que a taxa de bits inicial, é usado para o primeiro segmento. Se uma taxa de bits mínima for definida e a taxa de bits inicial for menor que a taxa mínima, o TVSDK selecionará o perfil com a taxa de bits mais baixa acima da taxa de bits mínima. Se a taxa inicial estiver acima da taxa máxima, o TVSDK selecionará a taxa mais alta abaixo da taxa máxima. Se a taxa de bits inicial for zero ou indefinida, a taxa de bits inicial será determinada pela política ABR. </p> <p><span class="codeph"> getABRInitialBitRate</span> retorna um valor inteiro que representa o perfil byte por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Taxa de bits mínima </td> 
   <td colname="col2"> <p>A taxa de bits mais baixa permitida para a qual o ABR pode alternar. </p> <p>A switching ABR ignora perfis com uma taxa de bits inferior a essa taxa de bits. <span class="codeph"> getABRMinBitRate</span> retorna um valor inteiro que representa o perfil de bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Taxa de bits máxima </td> 
   <td colname="col2"> <p>A taxa de bits mais alta permitida para a qual o ABR pode alternar. </p> <p>A switching ABR ignora perfis com uma taxa de bits superior a essa taxa de bits. <span class="codeph"> getABRMaxBitRate</span> retorna um valor inteiro que representa o perfil de bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Política de comutação ABR </td> 
   <td colname="col2"> <p>A reprodução alterna gradualmente para o perfil com a taxa de bits mais alta, quando possível. Você pode definir a política de switching ABR, que determina a rapidez com que o TVSDK alterna entre perfis. O padrão é <span class="codeph"> ABR_MODERATE</span>. </p> <p>Quando o TVSDK decide mudar para uma taxa de bits mais alta, o player seleciona o perfil de taxa de bits ideal para mudar com base na política ABR atual: 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_CONSERVATIVE</span>: Alterna para o perfil com a próxima taxa de bits mais alta quando a largura de banda for 50% mais alta do que a taxa de bits atual. </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>: Alterna para o próximo perfil de taxa de bits mais alta quando a largura de banda for 20% mais alta do que a taxa de bits atual. </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_AGRESSIVO</span>: Alterna imediatamente para o perfil de taxa de bits mais alta quando a largura de banda for maior que a taxa de bits atual. </li> 
     </ul> </p> <p>Se a taxa de bits inicial for zero ou não for especificada, mas uma política for especificada, a reprodução começará com o perfil de taxa de bits mais baixa para uma política conservadora, o perfil mais próximo da taxa de bits mediana dos perfis disponíveis para uma política moderada e o perfil de taxa de bits mais alta para uma política agressiva. </p> <p>A política funciona nas restrições das taxas de bits mínima e máxima, se essas taxas forem especificadas. </p> <p> <span class="codeph"> getABRPolicy</span> retorna a configuração atual da variável <span class="codeph"> ABRControlParameters</span> enum: <span class="codeph"> ABR_CONSERVATIVE</span>, <span class="codeph"> ABR_MODERATE</span>ou <span class="codeph"> ABR_AGRESSIVO</span>. </p> <p>Para obter mais informações, consulte o documento API de parâmetros de controle ABR. </p> </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se das seguintes informações:

* O mecanismo de failover do TVSDK pode substituir suas configurações, pois o TVSDK favorece uma experiência de reprodução contínua em vez de seguir estritamente os parâmetros de controle.
* Quando a taxa de bits muda, o TVSDK envia `onProfileChanged` eventos em `PlaybackEventListener`.

* Você pode alterar as configurações do ABR a qualquer momento e o reprodutor alterna para usar o perfil que melhor corresponde às configurações mais recentes.

Por exemplo, se um fluxo tiver os seguintes perfis:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se você especificar um intervalo de 300000 a 2000000, o TVSDK considerará somente os perfis 1, 2 e 3. Isso permite que os aplicativos se ajustem a várias condições de rede, como alternar de wi-fi para 3G ou para vários dispositivos, como um telefone, um tablet ou um desktop.

Para definir parâmetros de controle ABR, defina os parâmetros no `ABRControlParameter` classe.
