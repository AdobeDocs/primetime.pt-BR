---
description: Perguntas frequentes sobre o uso da proteção de saída com base em resolução.
seo-description: Perguntas frequentes sobre o uso da proteção de saída com base em resolução.
seo-title: Perguntas frequentes sobre RBOP
title: Perguntas frequentes sobre RBOP
uuid: 7dcd337c-369a-474c-8768-409c48b5cee5
translation-type: tm+mt
source-git-commit: fa9e89dd63c8b4c9d6eee78258957cfd30c29088
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---


# Perguntas frequentes sobre RBOP {#rbop-faq}

Perguntas frequentes sobre o uso da proteção de saída com base em resolução.

* **Q.** *Ao definir um requisito de saída digital para uma restrição de pixel, recebo erros de análise/formatação quando deixo a versão HDCP fora, mas não tenho nenhum requisito HDCP. Como devo configurar meu requisito de saída digital neste caso?* **A.** Como a verificação de versão HDCP não é suportada atualmente no cliente, o Adobe recomenda definir a versão HDCP como `1.0`. Isso garantirá que sua configuração esteja formatada corretamente e seja semântica consistente no futuro quando a verificação de versão HDCP for suportada. O trecho a seguir ilustra uma configuração com esse valor HDCP.

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

* **Q.** *As restrições de pixel de RBOP são discretas ou baseadas em intervalo?* **A.** As restrições de pixel de RBOP são diferenciadas com base em intervalos. Cada contagem de pixels define os requisitos para todas as contagens de pixels menores ou iguais à contagem especificada ou até a maior contagem menor que esse valor se houver mais de uma restrição de pixel. Simplificando, os valores se aplicam como limites máximos para cada contagem vertical de pixels.

   Suponhamos que um fluxo MBR com resoluções verticais de 240, 480, 600, 720 e 1080 seja passado ao seu player com as seguintes configurações de RBOP.

   **Configurações da política de RBOP:**

   * 720P - HDCP necessário
   * 480P - No OP

   As regras a seguir serão aplicadas a cada variante.

   **Fluxos:**

   * 240, 480: Ambos são &lt;= 480; não é necessário um OP e os fluxos serão carregados com ou sem HDCP presente.
   * 600, 720: Ambos são &lt;= 720; HDCP é necessário para reprodução
   * 1080: > 720; o fluxo é listado em bloco (erro retornado), pois não foi encontrado nas regras acima.


* **Q.** Em alguns dos meus dispositivos Android, as restrições de contagem de pixels que defini não estão sendo aplicadas exatamente como definido. O que está acontecendo?

   **A.** Alguns dispositivos Android têm tamanhos de quadros de relatórios ligeiramente superiores ao tamanho normal. Para corrigir essa situação, ajuste os tamanhos de quadro ( `maxPixel` e `pixelCount` configurações) para cima em 20 pixels. Por exemplo, ajuste as configurações de tamanho do quadro para cima, de:

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

   em geral, para todos os casos de `maxPixel` e `pixelCount`.

