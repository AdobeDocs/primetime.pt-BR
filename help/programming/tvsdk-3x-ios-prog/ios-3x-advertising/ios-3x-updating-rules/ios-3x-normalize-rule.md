---
description: A regra de normalização define uma transformação de URL a ser aplicada a um URL criativo de origem obtido de uma resposta VAST/VMAP.
keywords: normalizar regra;regras de seleção criativa
title: Normalizar regras
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Normalizar regras {#normalize-rules}

A regra de normalização define uma transformação de URL a ser aplicada a um URL criativo de origem obtido de uma resposta VAST/VMAP.

**Tabela 2: A regra de normalização tem os seguintes atributos e valores possíveis:**

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
