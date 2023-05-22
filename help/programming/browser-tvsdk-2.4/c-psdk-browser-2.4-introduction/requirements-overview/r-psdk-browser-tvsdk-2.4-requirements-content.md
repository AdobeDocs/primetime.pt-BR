---
description: Verifique as restrições e os requisitos para fluxos e listas de reprodução (manifestos).
title: Requisitos de conteúdo e manifesto
exl-id: 53fdd771-06ea-496f-9591-6ed4d5011f8d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# Requisitos de conteúdo e manifesto{#content-and-manifest-requirements}

Verifique as restrições e os requisitos para fluxos e listas de reprodução (manifestos).

<table id="table_D7C38CD3B4D24C3D9A3B55D8CEFE7366"> 
 <tbody> 
  <tr> 
   <td colname="col1"> Duração do segmento de conteúdo </td> 
   <td colname="col2"> A duração de um segmento não deve exceder a duração de destino especificada no arquivo de manifesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Requisito de conteúdo </td> 
   <td colname="col2"> Cada segmento TS deve começar com um quadro principal. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Conteúdo HLS </td> 
   <td colname="col2"> <p>Lembre-se do seguinte: 
     <ul id="ul_B226605345EA46F69DA1380E16826117"> 
      <li id="li_6564DC0E879544BB8513DD2D1CFBA8DE">O áudio AAC-SSR não é compatível. </li> 
      <li id="li_B73CAEBE4347406EA4DB25551B444BDA">Os codecs de áudio AC3 e Enhanced AC3 não são suportados. </li> 
      <li id="li_5986DD33C0FE485D99D4C00E2E6012CA">Fluxos HLS com descontinuidade, mas não há suporte para marcadores de descontinuidade. </li> 
      <li id="li_FED8686372DF4A39BAABC531BA4EB137">O HLS Live não oferece suporte à sobreposição de carimbo de data/hora. </li> 
      <li id="li_565CFBEAD9874BA48F6E25B0893BF131">Os anúncios na janela DVR de transmissões HLS Live não são resolvidos. </li> 
      <li id="li_7D22EA32C94240D79EDDA96D9E72FE8F">O intervalo de bytes não é compatível com o conteúdo criptografado AES-128. </li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Conteúdo de TRAÇO </td> 
   <td colname="col2"> <p>Lembre-se do seguinte: 
     <ul id="ul_9D33C2418F9F49DEAE0E642301726F89"> 
      <li id="li_74C69A21A7BD4831B92F0D57900E1CB1">Para transmissões ao vivo - O perfil ao vivo com tipo dinâmico é compatível. </li> 
      <li id="li_0C8743DB152047819D23C9F180998AD7">Para fluxos VOD — o perfil ativo com tipo estático é compatível. </li> 
      <li id="li_FBC6828663FB413798A4BDAF0B9831AA">Para fluxos de VOD - O perfil sob demanda não é certificado para fluxos de trabalho de anúncios. </li> 
      <li id="li_4393B9B1F6144BDEAE484C879750ED23">Não há suporte para a reprodução de fluxos DASH com vários períodos. </li> 
      <li id="li_6A2CEC4E974C4D44A45F5503A1A9D8D0">As Legendas incorporadas (608/708), sinalizadas por meio da tag de acessibilidade, são compatíveis. </li> 
      <li id="li_EDE93DF4F3A64A53BA80877F701A8F0D">Arquivos VTT fragmentados/segmentados não são compatíveis. </li> 
      <li id="li_8897F73611194030A490A4FF1178364C">Fluxos com tags personalizadas em banda não são certificados. </li> 
     </ul></p> </td> 
  </tr> 
 </tbody> 
</table>
