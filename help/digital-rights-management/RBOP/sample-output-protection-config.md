---
description: Esta seção apresenta um exemplo de configuração que ilustra os conceitos e a forma da configuração.
title: Exemplo de configuração de RBOP
exl-id: 0f40be83-9c7f-482b-ac42-9aa4e3f46f58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Exemplo de configuração de RBOP {#sample-rbop-configuration}

Esta seção apresenta um exemplo de configuração que ilustra os conceitos e a forma da configuração.

O exemplo de configuração JSON a seguir define uma política de saída em pixels que especifica o seguinte:

* Restringir a descriptografia do vídeo a resoluções de 1080 ou inferiores
* Impor restrições específicas para resoluções de 720 e 480:

   * Para resolução de 720: exigem HDCP para saída digital; exigem *Sistema de Gerenciamento da Geração de Cópias - Analógico* (CGMS-A) para saída analógica.
   * Para resolução 480: requer HDCP para saída digital; não requer proteção para analógica

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

Observe o seguinte sobre a configuração de exemplo acima:

* A variável `pixelCount` especificações estão um nível abaixo na estrutura JSON, dentro do intervalo `pixelConstraints` seção.

* Dentro de cada especificação de contagem de pixels, a proteção de saída é especificada para saída digital e analógica.
* Nas especificações de saída digital, as versões de HDCP são especificadas, embora o cliente não suporte atualmente o controle de versão de HDCP. Consulte as Perguntas frequentes para obter mais informações.
