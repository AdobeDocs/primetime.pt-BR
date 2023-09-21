---
description: A regra de prioridade define a ordem de prioridade das criações de anúncios que serão selecionadas para reprodução a partir de uma resposta VAST/VMAP.
keywords: regra de prioridade;regras de seleção criativa
title: Regras de prioridade
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Regras de prioridade{#priority-rules}

A regra de prioridade define a ordem de prioridade das criações de anúncios que serão selecionadas para reprodução a partir de uma resposta VAST/VMAP.

## Uma regra de prioridade tem os seguintes atributos e valores possíveis:

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"> Chave</th> 
   <th class="entry"> Tipo</th> 
   <th class="entry"> Valores</th> 
   <th class="entry"> Descrição</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> prioridade</span></td> 
   <td><span class="codeph"> Matriz</span></td> 
   <td></td> 
   <td> Uma matriz de tipos MIME em letras minúsculas que define a prioridade na qual as criações de origem devem ser selecionadas para reprodução.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Somente no momento <span class="codeph"> host</span> é compatível. Este atributo deve estar presente quando <span class="codeph"> corresponde a</span> e <span class="codeph"> valores</span> atributos são definidos.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> corresponde a</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> múltiplo</span></td> 
   <td>Valores possíveis:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - igual a</li> 
     <li><span class="codeph"> ne</span> - não é igual</li> 
     <li><span class="codeph"> co</span> - contém</li> 
     <li><span class="codeph"> nc</span> - não contém</li> 
     <li><span class="codeph"> sw</span> - começa com</li> 
     <li><span class="codeph"> Novo</span> - termina com</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> prioridade</span></td> 
   <td>O valor deve ser sempre <span class="codeph"> prioridade</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> valores</span></td> 
   <td><span class="codeph"> Matriz</span></td> 
   <td></td> 
   <td> <p>O TVSDK usará o <span class="codeph"> corresponde a</span> atributo no <span class="codeph"> item</span> da criação de origem e corresponder aos valores definidos nessa matriz</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> fluxo</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td></td> 
   <td> <p>O valor pode ser <span class="codeph"> vod</span> ou <span class="codeph"> live</span></p> </td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                    "
<b>type</b>": "
<b>priority</b>",
                    "
<b>stream</b>": "vod",
                    "
<b>priority</b>": [
                        "application/x-mpegurl",
                        "application/vnd.apple.mpegurl",
                        "application/x-shockwave-flash",
                        "video/mp4",
                        "video/m4v",
                        "video/x-flv",
                        "video/webm"
                    ]
                },
                {
                    ...
                },
            ]
        }
    }
}
```
