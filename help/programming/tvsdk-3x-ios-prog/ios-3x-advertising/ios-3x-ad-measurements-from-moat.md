---
description: O TVSDK obtém informações do FreeWheel e de outros adservers fornecendo respostas VAST. O FreeWheel fornece, dentro das respostas VAST, informações do serviço Moat. O serviço de Mat conta impressões de anúncios com uma precisão que mostra melhor que os criadores capturam ou negligenciam os interesses de um público-alvo.
title: Medições de anúncios do Fosso
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Medições de anúncios do Fosso {#ad-measurements-from-moat}

O TVSDK obtém informações do FreeWheel e de outros adservers fornecendo respostas VAST. O FreeWheel fornece, dentro das respostas VAST, informações do serviço Moat. O serviço de Mat conta impressões de anúncios com uma precisão que mostra melhor que os criadores capturam ou negligenciam os interesses de um público-alvo.

O Mat é um serviço de medição e visualização em vários usos, desde navegadores até dentro de aplicativos. O Mat gera dados de análise de marketing em tempo real em várias plataformas.

O XML de resposta VAST tem uma propriedade e um elemento que seu código pode ler, a propriedade de id do anúncio mais externo e o elemento de extensão mais externo. De qualquer maneira, seu código pode usar o TVSDK para salvar as informações da ID do anúncio e as informações da extensão e organizar as informações em uma estrutura de árvore. Com essa organização, seu código pode coletar os dados de qualquer nível e transmiti-los para onde for necessário. O valor da propriedade de id do anúncio mais externo permite que o código coordene as informações da campanha associada.

Por exemplo, o FreeWheel pode retornar dados em um elemento Extensions. Abaixo está uma amostra de elemento.

```xml
<Extensions> 
   <Extension type="FreeWheel"> 
    <Parameter name="moat"> 
     <MeasurementInfo renditionID="6398737" type="MediaFile"> 
      <MoatID> 
       <![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]]]> 
       <![CDATA[> 
        </MoatID> 
      </MeasurementInfo> 
      <MeasurementInfo renditionID="6398739" type="MediaFile"> 
        <MoatID> 
        <![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]]]> 
        <![CDATA[> 
        </MoatID> 
      </MeasurementInfo> 
    </Parameter> 
  </Extension> 
</Extensions>
```

A Freewheel também pode definir a propriedade id no elemento Ad, como mostrado na amostra abaixo.

```
<Ad id="118566" sequence="1">
```

Consulte a documentação da API da classe `PTNetworkAdInfo` in `PTAdAsset`.
