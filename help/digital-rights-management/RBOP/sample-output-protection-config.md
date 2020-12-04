---
description: Esta seção apresenta uma configuração de amostra que ilustra os conceitos e a forma da configuração.
seo-description: Esta seção apresenta uma configuração de amostra que ilustra os conceitos e a forma da configuração.
seo-title: Exemplo de configuração de RBOP
title: Exemplo de configuração de RBOP
uuid: fa5ead93-36c5-4ad1-947b-c4f1f2632d9b
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Exemplo de configuração de RBOP {#sample-rbop-configuration}

Esta seção apresenta uma configuração de amostra que ilustra os conceitos e a forma da configuração.

A seguinte configuração JSON de exemplo define uma política de saída de pixel que especifica o seguinte:

* Restringir a descriptografia do vídeo a resoluções de 1080 ou inferior
* Impor restrições específicas às resoluções 720 e 480:

   * Para a resolução 720: Exigir HDCP para saída digital; requer a proteção *Copy Generation Management System - Analog* (CGMS-A) para saída analógica.
   * Para a resolução 480: Exigir HDCP para saída digital; não requer proteção para analógico

```
{ 
  "pixelConstraints":  
    [ 
      { 
        "pixelCount": 720, 
        "digital": 
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "REQUIRED_CGMSA"} 
      }, 
      { 
        "pixelCount": 480, 
        "digital":  
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "NO_PROTECTION"} 
      } 
    ], 
  "maxPixel": 1080 
}
```

Observe o seguinte sobre a configuração de amostra acima:

* As especificações `pixelCount` estão um nível abaixo na estrutura JSON, dentro da seção `pixelConstraints`.

* Dentro de cada especificação de contagem de pixels, a proteção de saída é especificada para saída digital e analógica.
* Nas especificações de saída digital, as versões HDCP são especificadas, embora o cliente não suporte atualmente o controle de versão HDCP. Consulte as Perguntas frequentes para obter mais informações.

