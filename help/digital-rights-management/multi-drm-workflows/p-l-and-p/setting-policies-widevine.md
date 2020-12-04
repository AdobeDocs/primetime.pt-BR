---
seo-title: Usando Políticas de Proteção de Saída
title: Usando Políticas de Proteção de Saída
uuid: f00d2a97-0036-41a6-ab44-391cc40b146e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Usando Políticas de Proteção de Saída{#using-output-protection-policies}

**Políticas de proteção de saída de largura**

A widevine suporta nativamente as restrições de proteção de saída analógica e digital. Consulte a documentação do provedor de serviço do Widevine sobre como anexar essas políticas às licenças geradas.

Se você usar o Expressplay como o provedor de serviço Widevine, anexe as políticas de proteção de saída digital no tempo de geração do token por meio do sinalizador hdcpOutputControl:
Os valores permitidos são 0, 1, 2, onde 0 = HDCP_NONE, 1 = HDCP_V1, 2 = HDCP_V2. HDCP_V1 e HDCP_V2 aplicam HDCP versão 1.X e 2.X respectivamente.

Atualmente, o Express não suporta a anexação de restrições de saída analógicas

**Políticas de proteção de saída PlayReady**

O PlayReady também oferece suporte nativo a restrições de proteção de saída analógica e digital. Os valores de nível de proteção de saída que você pode definir. A página [Níveis de Proteção de Saída](https://msdn.microsoft.com/en-us/library/dn468831.aspx) documentos os valores que você pode definir e seu comportamento de cliente esperado.

Se você usar o Expressplay, anexe valores de nível de proteção de saída no tempo de geração do token por meio do sinalizador compactadoDigitalAudioOPL, descompactadoDigitalAudioOPL, compactadoDigitalVideoOPL, descompactadoDigitalVideoOPL e desconhecidoOutputBehavior. Eles estão documentados em [Solicitação de token de licença PlayReady](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
