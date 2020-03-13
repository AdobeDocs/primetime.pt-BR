---
description: A regra normalize define uma transformação de URL a ser aplicada a um URL criativo de origem obtido de uma resposta VAST/VMAP.
keywords: normalize rule;creative selection rules
seo-description: A regra normalize define uma transformação de URL a ser aplicada a um URL criativo de origem obtido de uma resposta VAST/VMAP.
seo-title: Normalizar regras
title: Normalizar regras
uuid: eccae85b-907e-4e16-9bb8-6c2be6cb0ab6
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Normalizar regras{#normalize-rules}

A regra normalize define uma transformação de URL a ser aplicada a um URL criativo de origem obtido de uma resposta VAST/VMAP.

**Quadro 2: A regra normalize tem os seguintes atributos e valores possíveis:**

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
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> normalize</span></td> 
   <td>O valor deve ser sempre <span class="codeph"> normalizado</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Atualmente, apenas <span class="codeph"> o host</span> é suportado. Este atributo deve estar presente quando <span class="codeph"> corresponde</span> e <span class="codeph"> valores</span> os atributos são definidos.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td></td> 
   <td></td> 
   <td>Valores possíveis:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - igual</li> 
     <li><span class="codeph"> ne</span> - não é igual</li> 
     <li><span class="codeph"> co</span> - contém</li> 
     <li><span class="codeph"> nc</span> - não contém</li> 
     <li><span class="codeph"> sw</span> - começa com</li> 
     <li><span class="codeph"> ew</span> - termina com</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Matriz</span></td> 
   <td></td> 
   <td>O TVSDK usará o atributo de <span class="codeph"> correspondência</span> no <span class="codeph"> item</span> do anúncio de origem e corresponderá aos valores definidos nesta matriz.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> find</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Uma expressão regular a ser aplicada no URL criativo de origem para corresponder.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> replace</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Uma expressão regular a ser aplicada no URL criativo de origem para substituição com base na correspondência.</td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                ...
                }
                {
                    "
<b>type</b>": "
<b>normalize</b>",
                    "
<b>item</b>": "host",
                    "
<b>matches</b>": "ew",
                    "
<b>values</b>": [
                        "redirector.gvt1.com"
                    ],
                    "
<b>find</b>": "videoplayback/(.*?)/expire/.*?/(.*?)/signature/.*?/",
                    "
<b>replace</b>": "videoplayback/$1/expire//$2/signature//"
                }                
            ]
        }
    }
}
```

