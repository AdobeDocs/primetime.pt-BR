---
description: Perguntas frequentes sobre o uso da proteção de saída com base em resolução.
title: PERGUNTAS FREQUENTES SOBRE RBOP
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# PERGUNTAS FREQUENTES SOBRE RBOP {#rbop-faq}

Perguntas frequentes sobre o uso da proteção de saída com base em resolução.

* **P.** *Ao definir um requisito de saída digital para uma restrição de pixel, estou recebendo erros de análise/formatação quando deixo a versão HDCP de fora, mas não tenho nenhum requisito HDCP. Como devo configurar meu requisito de saída digital neste caso?* **A.** Como a verificação de versão HDCP não é suportada atualmente no cliente, o Adobe recomenda configurar a versão HDCP como `1.0`. Isso garantirá que sua configuração esteja formatada corretamente e seja semanticamente consistente no futuro quando a verificação de versão HDCP for suportada. O trecho a seguir ilustra uma configuração com esse valor HDCP.

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

* **P.** *As restrições de pixel RBOP são discretas ou baseadas em intervalo?* **A.** As restrições de pixel RBOP são baseadas em intervalos. Cada contagem de pixels define os requisitos para todas as contagens de pixels inferiores ou iguais à contagem fornecida ou até a maior contagem menor que esse valor se existir mais de uma restrição de pixels. Simplificando, os valores se aplicam como limites máximos para cada contagem de pixels vertical.

  Suponhamos que um fluxo MBR com resoluções verticais de 240, 480, 600, 720 e 1080 seja passado para o seu reprodutor com as seguintes configurações de RBOP.

  **Configurações de Política RBOP:**

   * 720P - HDCP necessário
   * 480P - Sem OP

  As regras a seguir serão aplicadas a cada variante.

  **Fluxos:**

   * 240, 480: Ambos são &lt;= 480; nenhum OP será necessário e os fluxos serão carregados com ou sem HDCP presente.
   * 600, 720: Ambos são &lt;= 720; HDCP é necessário para reprodução
   * 1080: > 720; o fluxo está listado em bloco (erro retornado), pois não foi encontrado nas regras acima.

* **P.** Em alguns dos meus dispositivos Android, as restrições de contagem de pixels que defini não estão sendo aplicadas exatamente como definido. O que está acontecendo?

  **A.** Alguns dispositivos Android estão relatando tamanhos de quadros ligeiramente maiores que o tamanho normal. Para solucionar essa situação, ajuste o tamanho dos quadros ( `maxPixel` e `pixelCount` ) 20 pixels para cima. Por exemplo, ajuste as configurações de tamanho de quadro para cima, de:

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

  em todo o, para todas as instâncias do `maxPixel` e `pixelCount`.
