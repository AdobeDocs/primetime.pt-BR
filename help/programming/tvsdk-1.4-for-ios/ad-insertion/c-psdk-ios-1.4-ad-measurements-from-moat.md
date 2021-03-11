---
description: O TVSDK obtém informações do FreeWheel e de outros servidores de publicidade, fornecendo respostas VAST. O FreeWheel fornece, dentro das respostas VAST, informações do serviço Mat. O serviço Mat conta impressões e exibe uma precisão que mostra melhor que as criações capturam ou negligenciam os interesses de um público-alvo.
title: Medições de anúncios do Moat
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Medições de anúncio do Moat{#ad-measurements-from-moat}

O TVSDK obtém informações do FreeWheel e de outros servidores de publicidade, fornecendo respostas VAST. O FreeWheel fornece, dentro das respostas VAST, informações do serviço Mat. O serviço Mat conta impressões e exibe uma precisão que mostra melhor que as criações capturam ou negligenciam os interesses de um público-alvo.

O Moat é um serviço que avalia e visualiza em vários usos, desde navegadores até dentro de aplicativos. O Moat gera dados de análise de marketing em tempo real em várias plataformas.

O XML de resposta VAST tem uma propriedade e um elemento que seu código pode ler, a propriedade de id de anúncio mais externa e o elemento de extensão mais externo. De qualquer forma, seu código pode usar o TVSDK para salvar as informações da ID de anúncio e as informações da extensão e organizar as informações em uma estrutura de árvore. Com essa organização, seu código pode coletar os dados de qualquer nível e transmiti-los para onde for necessário. O valor da propriedade de id de anúncio mais externa permite que o código coordene informações da campanha associada.

Por exemplo, o FreeWheel pode retornar dados em um elemento de Extensões. Abaixo está um elemento de amostra.

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

O Freewheel também pode definir a propriedade id no elemento Anúncio, como mostrado na amostra abaixo.

```
<Ad id="118566" sequence="1">
```

Consulte a documentação da API para a classe `PTNetworkAdInfo` em `PTAdAsset`.
