---
description: Esta seção apresenta uma configuração de amostra que ilustra os conceitos e a forma da configuração.
title: Exemplo de configuração de RBOP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---


# Exemplo de configuração de RBOP {#sample-rbop-configuration}

Esta seção apresenta uma configuração de amostra que ilustra os conceitos e a forma da configuração.

A seguinte configuração JSON de amostra define uma política de saída de pixel que especifica o seguinte:

* Restringir a descriptografia do vídeo a resoluções de 1080 ou inferior
* Impor restrições específicas às resoluções de 720 e 480:

   * Para a resolução 720: Exigir HDCP para saída digital; requerem proteção *Copy Generation Management System - Analog* (CGMS-A) para saída analógica.
   * Para a resolução 480: Exigir HDCP para saída digital; não exige proteção para analógico

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

