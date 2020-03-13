---
description: O TVSDK coleta informações do FreeWheel e de outros servidores que fornecem respostas VAST. O FreeWheel fornece, dentro das respostas VAST, informações do serviço Mate. O serviço Mat conta impressões e com uma precisão que mostra melhor que as criações capturam ou negligenciam os interesses de um público-alvo.
seo-description: O TVSDK coleta informações do FreeWheel e de outros servidores que fornecem respostas VAST. O FreeWheel fornece, dentro das respostas VAST, informações do serviço Mate. O serviço Mat conta impressões e com uma precisão que mostra melhor que as criações capturam ou negligenciam os interesses de um público-alvo.
seo-title: Medições de anúncios do Moat
title: Medições de anúncios do Moat
uuid: 520d33b0-2218-4f74-9689-b9dc520f29cc
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Medições de anúncios do Moat {#ad-measurements-from-moat}

O TVSDK coleta informações do FreeWheel e de outros servidores que fornecem respostas VAST. O FreeWheel fornece, dentro das respostas VAST, informações do serviço Mate. O serviço Mat conta impressões e com uma precisão que mostra melhor que as criações capturam ou negligenciam os interesses de um público-alvo.

Moat é um serviço que mede e exibe diversos usos, de navegadores a aplicativos internos. O Moat gera dados de análise de marketing em tempo real em várias plataformas.

O XML de resposta VAST tem uma propriedade e um elemento que seu código pode ler, a propriedade de id de anúncio mais externa e o elemento de extensão mais externo. De qualquer forma, seu código pode usar o TVSDK para salvar as informações da ID do anúncio e da extensão e organizar as informações em uma estrutura em árvore. Com essa organização, seu código pode coletar os dados de qualquer nível e passá-los para onde for necessário. O valor da propriedade de id de anúncio mais externa permite que seu código coordene informações da campanha associada.

Por exemplo, o FreeWheel pode retornar dados em um elemento Extensões. Abaixo está um elemento de amostra.

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

O FreeWheel também pode definir a propriedade id no elemento Anúncio, como mostrado na amostra abaixo.

```
<Ad id="118566" sequence="1">
```

Consulte a documentação da API da classe `PTNetworkAdInfo` em `PTAdAsset`.