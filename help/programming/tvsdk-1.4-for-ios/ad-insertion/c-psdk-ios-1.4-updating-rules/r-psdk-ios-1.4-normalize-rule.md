---
description: A regra de normalização define uma transformação de URL a ser aplicada a um URL criativo de origem obtido de uma resposta VAST/VMAP.
keywords: normalizar regra;regras de seleção criativa
title: Normalizar regras
exl-id: 0d9669bf-8d64-49da-b917-5a6d6c3ca776
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Normalizar regras{#normalize-rules}

A regra de normalização define uma transformação de URL a ser aplicada a um URL criativo de origem obtido de uma resposta VAST/VMAP.

## A regra de normalização tem os seguintes atributos e valores possíveis:

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
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> normalizar</span></td> 
   <td>O valor deve ser sempre <span class="codeph"> normalizar</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Somente no momento <span class="codeph"> host</span> é compatível. Este atributo deve estar presente quando <span class="codeph"> corresponde a</span> e <span class="codeph"> valores</span> atributos são definidos.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> corresponde a</span></td> 
   <td></td> 
   <td></td> 
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
   <td><span class="codeph"> valores</span></td> 
   <td><span class="codeph"> Matriz</span></td> 
   <td></td> 
   <td>O TVSDK usará o <span class="codeph"> corresponde a</span> atributo no <span class="codeph"> item</span> da criação de origem e corresponder aos valores definidos nessa matriz.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> localizar</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Uma expressão regular a ser aplicada ao URL de criação de origem para correspondência.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> replace</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Uma expressão regular a ser aplicada no URL criativo de origem a ser substituído com base na correspondência.</td> 
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
