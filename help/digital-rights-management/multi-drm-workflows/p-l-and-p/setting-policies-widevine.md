---
title: Usando Políticas de Proteção de Saída
description: Usando Políticas de Proteção de Saída
copied-description: true
exl-id: d91c9181-a6b2-4982-a3ba-57c4b56428eb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Usando Políticas de Proteção de Saída{#using-output-protection-policies}

**Políticas de proteção de saída do Widevine**

O Widevine suporta nativamente restrições de proteção de saída analógica e digital. Consulte a documentação do seu provedor de serviços Widevine sobre como anexar essas políticas a licenças geradas.

Se você usar o Expressplay como provedor de serviços Widevine, anexe políticas de proteção de saída digital no momento da geração do token por meio do sinalizador hdcpOutputControl: os valores permitidos são 0, 1, 2, em que 0 = HDCP_NONE, 1 = HDCP_V1, 2 = HDCP_V2. O HDCP_V1 e o HDCP_V2 aplicam o HDCP versão 1.X e 2.X, respectivamente.

No momento, a expressão não oferece suporte à anexação de restrições de saída analógicas

**Políticas de proteção de saída PlayReady**

O PlayReady também suporta nativamente restrições de proteção de saída analógica e digital. Os valores do nível de proteção de saída que você pode definir. A página [Níveis de proteção de saída](https://msdn.microsoft.com/en-us/library/dn468831.aspx) O documenta os valores que você pode definir e o comportamento esperado do cliente.

Se você usar o Expressplay, anexe valores de nível de proteção de saída no tempo de geração do token por meio do sinalizador compressedDigitalAudioOPL, uncompressedDigitalAudioOPL, compressedDigitalVideoOPL, uncompressedDigitalVideoOPL e unknownOutputBehavior. Eles estão documentados em [Solicitação de token de licença do PlayReady](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
