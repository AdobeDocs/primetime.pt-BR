---
description: Perguntas frequentes sobre o uso da proteção de saída baseada em resolução.
title: Perguntas frequentes sobre RBOP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Perguntas frequentes sobre RBOP {#rbop-faq}

Perguntas frequentes sobre o uso da proteção de saída baseada em resolução.

* **P.** *Ao definir um requisito de saída digital para uma restrição de pixel, estou recebendo erros de análise/formatação ao deixar a versão HDCP de fora, mas não tenho nenhum requisito HDCP. Como devo configurar meu requisito de saída digital neste caso?* **R.** Como a verificação da versão HDCP não é suportada atualmente no cliente, o Adobe recomenda definir a versão HDCP para  `1.0`. Isso garantirá que sua configuração esteja formatada corretamente e seja semanticamente consistente no futuro quando a verificação de versão HDCP for suportada. O trecho a seguir ilustra uma configuração com este valor HDCP.

   ```
   { "pixelConstraints":  
     [  
       { "pixelCount": 720, "digital":  
         [  
           {  
             "output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}  
           }  
         ]  
       }  
     ]  
   }
   ```

* **P.** *As restrições de pixel de RBOP são discretas ou baseadas em intervalo?* **A.** As restrições de pixel de RBOP são diferenciadas com base em intervalos. Cada contagem de pixels define os requisitos para todas as contagens de pixels inferiores ou iguais à contagem fornecida ou até a maior contagem menor que esse valor, se houver mais de uma restrição de pixel. Simplificando, os valores se aplicam como limites máximos para cada contagem de pixels verticais.

   Suponhamos que um fluxo MBR com resoluções verticais de 240, 480, 600, 720 e 1080 seja passado para o seu player com as seguintes configurações de RBOP.

   **Configurações da Política de RBOP:**

   * 720P - HDCP necessário
   * 480P - Sem OP

   As regras a seguir serão aplicadas a cada variante.

   **Fluxos:**

   * 240, 480: Ambos são &lt;= 480; não é necessário um OP e os fluxos serão carregados com ou sem HDCP presente.
   * 600, 720: Ambos são &lt;= 720; HDCP é necessário para reprodução
   * 1080: > 720; o fluxo é listado em bloco (erro retornado), pois não é encontrado nas regras acima.


* **P.** Em alguns dos meus dispositivos Android, as restrições de contagem de pixels que defini não estão sendo aplicadas exatamente como definido. O que está acontecendo?

   **R.** Alguns dispositivos Android estão relatando tamanhos de quadros ligeiramente superiores ao tamanho normal. Para corrigir esta situação, ajuste os tamanhos do seu quadro ( `maxPixel` e `pixelCount` configurações) para cima em 20 pixels. Por exemplo, ajuste as configurações de tamanho do quadro para cima, de:

   ```
   { 
       "maxPixel": 800, 
       "pixelConstraints": [ 
           { "pixelCount": 532, 
             "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
             "analog": {"output": "REQUIRED"} 
           }, 
   ... 
   ```

   para:

   ```
   { 
       "maxPixel": 820, 
       "pixelConstraints": [ 
           { "pixelCount": 552, 
             "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
             "analog": {"output": "REQUIRED"} 
           }, 
   ... 
   ```

   em geral, para todas as instâncias de `maxPixel` e `pixelCount`.

