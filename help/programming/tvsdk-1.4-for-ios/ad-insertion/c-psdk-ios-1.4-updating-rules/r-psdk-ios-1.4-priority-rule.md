---
description: A regra de prioridade define a ordem de prioridade dos anúncios que serão selecionados para reprodução a partir de uma resposta VAST/VMAP.
keywords: priority rule;creative selection rules
seo-description: A regra de prioridade define a ordem de prioridade dos anúncios que serão selecionados para reprodução a partir de uma resposta VAST/VMAP.
seo-title: Regras de prioridade
title: Regras de prioridade
uuid: a0924b3e-45cb-45ca-8a98-ed7d42aaed14
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---


# Regras de prioridade{#priority-rules}

A regra de prioridade define a ordem de prioridade dos anúncios que serão selecionados para reprodução a partir de uma resposta VAST/VMAP.

## Uma regra de Prioridade tem os seguintes atributos e valores possíveis:

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"> Principal</th> 
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
   <td> Uma matriz de tipos mímicos minúsculos que definem a prioridade na qual as criações de origem devem ser selecionadas para reprodução.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Atualmente, apenas <span class="codeph"> host</span> é suportado. Este atributo deve estar presente quando os atributos <span class="codeph"> correspondem</span> e <span class="codeph"> valores</span> estiverem definidos.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> multiple</span></td> 
   <td>Valores possíveis:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - igual</li> 
     <li><span class="codeph"> ne</span> - não é igual</li> 
     <li><span class="codeph"> co</span> - contém</li> 
     <li><span class="codeph"> nc</span> - não contém</li> 
     <li><span class="codeph"> sw</span> - start com</li> 
     <li><span class="codeph"> ew</span>  - termina com</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> prioridade</span></td> 
   <td>O valor deve ser sempre <span class="codeph"> priority</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Matriz</span></td> 
   <td></td> 
   <td> <p>O TVSDK usará o atributo <span class="codeph"> corresponde</span> no <span class="codeph"> item</span> do criativo de origem e corresponderá aos valores definidos nesta matriz</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> stream</span></td> 
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

