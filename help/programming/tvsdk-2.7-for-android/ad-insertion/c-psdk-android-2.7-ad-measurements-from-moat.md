---
description: O TVSDK coleta informações do FreeWheel e de outros servidores de anúncios, fornecendo respostas VAST. O FreeWheel fornece, dentro das respostas VAST, informações do serviço Mate. O serviço Mat conta impressões e com uma precisão que mostra melhor se os criativos capturam ou negligenciam interesses de audiências.
seo-description: O TVSDK coleta informações do FreeWheel e de outros servidores de anúncios, fornecendo respostas VAST. O FreeWheel fornece, dentro das respostas VAST, informações do serviço Mate. O serviço Mat conta impressões e com uma precisão que mostra melhor se os criativos capturam ou negligenciam interesses de audiências.
seo-title: Medições de anúncios do Moat
title: Medições de anúncios do Moat
uuid: b89f900f-50ab-4152-9c0f-11f82d92bffa
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# Medições de anúncios do Moat{#ad-measurements-from-moat}

O TVSDK coleta informações do FreeWheel e de outros servidores de anúncios, fornecendo respostas VAST. O FreeWheel fornece, dentro das respostas VAST, informações do serviço Mate. O serviço Mat conta impressões e com uma precisão que mostra melhor se os criativos capturam ou negligenciam interesses de audiências.

Moat é um serviço que mede e exibe diversos usos, de navegadores a aplicativos internos. O Moat gera dados de análise de marketing em tempo real em várias plataformas.

O XML de resposta VAST tem uma propriedade e um elemento que seu código pode ler, a propriedade mais externa `Ad id` e o elemento mais externo `Extension`. De qualquer forma, seu código pode usar o TVSDK para salvar as informações `Ad id` e `Extension`, em seguida, organizar as informações em uma estrutura em árvore. Com essa organização, seu código pode coletar os dados de qualquer nível e passá-los para onde for necessário. O valor da propriedade mais externa `Ad id` permite que seu código coordene informações da campanha associada.

Por exemplo, o FreeWheel pode retornar dados em um elemento Extensões. Abaixo está um elemento de amostra.

```xml
<?xml version="1.0"?> 
<Extensions> 
  <Extension type="FreeWheel"> 
    <Parameter name="moat"> 
      <MeasurementInfo renditionID="6398737" type="MediaFile"> 
        <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
      </MeasurementInfo> 
      <MeasurementInfo renditionID="6398739" type="MediaFile"> 
        <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
      </MeasurementInfo> 
    </Parameter> 
  </Extension> 
</Extensions> 
```

O FreeWheel também pode definir a propriedade `id` no elemento `Ad`, conforme mostrado na amostra abaixo.

```xml
<Ad id="118566" sequence="1">
```

Para obter informações sobre a API, consulte a documentação da API para a classe [NetworkAdInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/)
