---
description: A regra normalizar define uma transformação de URL para aplicar a um URL criativo de origem obtido de uma resposta VAST/VMAP.
keywords: normalizar regra, regras de seleção criativa
title: Normalizar regras
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

---


# Normalizar regras {#normalize-rules}

A regra normalizar define uma transformação de URL para aplicar a um URL criativo de origem obtido de uma resposta VAST/VMAP.

**Quadro 2: A regra de normalização tem os seguintes atributos e valores possíveis:**

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"><b>Chave</b></th> 
   <th class="entry"><b>Tipo</b></th> 
   <th class="entry"><b>Valores</b></th> 
   <th class="entry"><b>Descrição</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> normalizar</span></td> 
   <td>O valor deve ser sempre <span class="codeph"> normalize</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Atualmente, somente <span class="codeph"> host</span> é suportado. Esse atributo deve estar presente quando <span class="codeph"> corresponder a</span> e <span class="codeph"> valores</span> forem definidos.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td></td> 
   <td></td> 
   <td>Valores possíveis:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span>  - igual</li> 
     <li><span class="codeph"> ne</span>  - não é igual</li> 
     <li><span class="codeph"> co</span> - contém</li> 
     <li><span class="codeph"> nc</span>  - não contém</li> 
     <li><span class="codeph"> sw</span>  - começa com</li> 
     <li><span class="codeph"> ew</span>  - termina com</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Matriz</span></td> 
   <td></td> 
   <td>O TVSDK usará o atributo <span class="codeph"> corresponde</span> no <span class="codeph"> item</span> do criativo de origem e corresponderá aos valores definidos nessa matriz.</td> 
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
   <td> Uma expressão regular a ser aplicada no URL criativo de origem para substituir com base na correspondência.</td> 
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
