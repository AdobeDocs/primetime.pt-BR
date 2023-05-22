---
description: O TVSDK obtém informações do FreeWheel e de outros servidores de anúncios que fornecem respostas do VAST. O FreeWheel fornece, dentro das respostas VAST, informações do serviço Moat. O serviço de Mat conta impressões de anúncios com uma precisão que mostra melhor se os criadores capturam ou negligenciam os interesses de um público.
title: Medições de anúncios do Fosso
exl-id: c480f152-c09c-49fe-a8fb-d199bbfb0393
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# Medições de anúncios do Fosso {#ad-measurements-from-moat}

O TVSDK obtém informações do FreeWheel e de outros servidores de anúncios que fornecem respostas do VAST. O FreeWheel fornece, dentro das respostas VAST, informações do serviço Moat. O serviço de Mat conta impressões de anúncios com uma precisão que mostra melhor se os criadores capturam ou negligenciam os interesses de um público.

O Mat é um serviço de medição e visualização em vários usos, desde navegadores até dentro de aplicativos. O Mat gera dados de análise de marketing em tempo real em várias plataformas.

O XML de resposta VAST tem uma propriedade e um elemento que seu código pode ler, o mais externo `Ad id` propriedade e os mais `Extension` elemento. De qualquer maneira, seu código pode usar o TVSDK para salvar as `Ad id` informações e a `Extension` informações e, em seguida, organize as informações em uma estrutura em árvore. Com essa organização, seu código pode coletar os dados de qualquer nível e transmiti-los para onde for necessário. O valor da região mais `Ad id` permite que seu código coordene informações da campanha associada.

Por exemplo, o FreeWheel pode retornar dados em um elemento Extensions. Abaixo está uma amostra de elemento.

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

O Freewheel também pode definir a `id` propriedade na `Ad` como mostrado na amostra abaixo.

```xml
<Ad id="118566" sequence="1">
```

Para obter informações sobre APIs, consulte a documentação da classe `NetworkAdInfo`.
