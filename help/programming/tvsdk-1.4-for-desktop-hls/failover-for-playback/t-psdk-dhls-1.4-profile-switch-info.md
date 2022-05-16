---
description: Quando o reprodutor de mídia alterna seu perfil atual para um novo perfil, você pode recuperar informações sobre o switch, incluindo quando ele mudou, informações de largura e altura ou por que uma taxa de bits diferente foi usada.
title: Obter informações sobre a troca de perfis
exl-id: b46909fe-666a-4730-8922-15c3eb7a1cba
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Obter informações sobre a troca de perfis{#get-information-about-profile-switch}

Quando o reprodutor de mídia alterna seu perfil atual para um novo perfil, você pode recuperar informações sobre o switch, incluindo quando ele mudou, informações de largura e altura ou por que uma taxa de bits diferente foi usada.

1. Escute o `ProfileEvent.PROFILE_CHANGED` evento.

   O reprodutor de mídia TVSDK despacha esse evento quando seu algoritmo de switching de taxa de bits adaptável muda para outro perfil devido às condições da rede ou da máquina. (Quando a taxa de bits ou o período muda).
1. Quando o evento ocorrer, verifique as seguintes propriedades para obter informações sobre o switch:

   * `profile`: Identificador para o novo perfil que está sendo usado.
   * `time`: A hora do fluxo em que o switch ocorreu.
   * `description`: Descrição textual do motivo para uma alteração na taxa de bits, como uma sequência de pares de chave/valor separados por ponto e vírgula. Inclui no máximo um `Reason` e um `Bitrate`. Se as informações não estiverem disponíveis ou a taxa de bits não tiver sido alterada, essa string ficará vazia.

      <table id="table_E400FD9C57FF40CBAC14AF6847CD8301"> 
       <thead> 
         <tr> 
         <th colname="col1" class="entry"> Nome da chave </th> 
         <th colname="col2" class="entry"> Valores possíveis </th> 
         </tr> 
       </thead>
       <tbody> 
         <tr> 
         <td colname="col1"> <span class="codeph"> Motivo </span> </td> 
         <td colname="col2"> 
          <ul id="ul_37DDE3F297634ED6B47DF5D73F969369"> 
          <li id="li_E374B029E1AF40689D70A9D30E057C5B">Adaptação de Rede </li> 
          <li id="li_753862EEF1C9474EA8E20C89F5EF5D8D">Busca </li> 
          <li id="li_EC14923F92CF4D11A47928A8D2DE6D8B">Perfil não suportado </li> 
          <li id="li_695AB4A89C9D4833AF6D8B6424FC912B">Failover </li> 
          </ul> </td> 
         </tr> 
         <tr> 
         <td colname="col1"> <span class="codeph"> Taxa de bits </span> </td> 
         <td colname="col2"> 
          <ul id="ul_1B49BD90A91147359712E1AFD8877E23"> 
          <li id="li_1C8E593C65D34742B14A8D0EAD43E0A9"> <span class="codeph"> up </span>: A taxa de bits aumentou </li> 
          <li id="li_B1A00E3985A849B6855E15CF70D79BB8"> <span class="codeph"> down </span>: A taxa de bits diminuiu </li> 
          </ul> </td> 
         </tr> 
       </tbody> 
       </table>

      Estes são alguns exemplos de retorno `description` strings:

      ```
      "Bitrate::=up;Reason::=Network Adaptation;" 
      
      "Bitrate::=down;Reason::=Failover;"
      ```

   * `width`: Número inteiro que indica a largura em pixels.
   * `height`: Número inteiro que indica a altura em pixels.

      >[!NOTE]
      >
      >Os dados de largura e altura só estão disponíveis quando estão incluídos na variável `RESOLUTION` no manifesto M3U8. Se as informações não forem incluídas no M3U8, as propriedades de largura e altura serão definidas como 0, pois não fazem parte das informações do perfil.

<!--<a id="example_A713D420AE2E4E3CB7B78C6BC732BE90"></a>-->

Por exemplo:

```
_player.addEventListener(ProfileEvent.PROFILE_CHANGED, onProfileChange); 
private function onProfileChange(event:ProfileEvent):void { 
    _logger.info("#onProfileChange Current profile/bitrate has changed.  
      {0} for reason {1} of resolution [ {2} , {3} ]",  
      event.profile, event.description, event.width, event.height); 
}
```
