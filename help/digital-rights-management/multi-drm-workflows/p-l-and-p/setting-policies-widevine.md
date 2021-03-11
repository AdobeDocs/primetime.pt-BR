---
title: Usando Políticas de Proteção de Saída
description: Usando Políticas de Proteção de Saída
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Usando Políticas de Proteção de Saída{#using-output-protection-policies}

**Políticas de proteção de saída de viúvas**

A viúva suporta nativamente restrições de proteção de saída analógica e digital. Consulte a documentação do seu provedor de serviços Widevine sobre como anexar essas políticas a licenças geradas.

Se você usar Expressplay como o provedor de serviço Widevine, anexe políticas de proteção de saída digital no momento da geração de token por meio do sinalizador hdcpOutputControl :
Os valores permitidos são 0, 1, 2, onde 0 = HDCP_NONE, 1 = HDCP_V1, 2 = HDCP_V2. HDCP_V1 e HDCP_V2 impõem HDCP versão 1.X e 2.X, respectivamente.

Atualmente, o Express não suporta a anexação de restrições de saída analógicas

**Políticas de proteção de saída PlayReady**

PlayReady também suporta nativamente restrições de proteção de saída analógica e digital. Os valores do nível de proteção de saída que você pode definir. A página [Níveis de Proteção de Saída](https://msdn.microsoft.com/en-us/library/dn468831.aspx) documenta os valores que você pode definir e seu comportamento de cliente esperado.

Se você usar o Expressplay, anexe valores de nível de proteção de saída no tempo de geração de token por meio do sinalizador compressedDigitalAudioOPL, uncompressedDigitalAudioOPL, compressedDigitalVideoOPL, uncompressedVideoOPL e unknownOutputBehavior . Elas estão documentadas em [Solicitação de Token de Licença PlayReady](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
