---
description: Os fluxos HLS e DASH fornecem codificações (perfis) de taxa de bits diferentes para a mesma intermitência curta de vídeo. O TVSDK pode selecionar o nível de qualidade para cada intermitência com base na largura de banda disponível.
title: Taxas de bits adaptáveis (ABR) para qualidade de vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Taxas de bits adaptáveis (ABR) para qualidade de vídeo{#adaptive-bit-rates-abr-for-video-quality}

Os fluxos HLS e DASH fornecem codificações (perfis) de taxa de bits diferentes para a mesma intermitência curta de vídeo. O TVSDK pode selecionar o nível de qualidade para cada intermitência com base na largura de banda disponível.

O TVSDK monitora constantemente a taxa de bits para garantir que o conteúdo seja reproduzido na taxa de bits ideal para a conexão de rede atual.

Você pode definir a política de switching ABR (taxa de bits adaptável) e as taxas de bits inicial, mínima e máxima para um fluxo MBR (taxa de vários bits). O TVSDK alterna automaticamente para a taxa de bits que fornece a melhor experiência de reprodução na configuração especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Taxa de bits inicial </td> 
   <td colname="col2"> <p>A taxa de bits de reprodução desejada (em bits por segundo) para o primeiro segmento. Quando a reprodução começa, o perfil mais próximo, que é igual ou maior que a taxa de bits inicial, é usado para o primeiro segmento. </p> <p> Se uma taxa de bits mínima for definida e a taxa de bits inicial for menor que a taxa mínima, o TVSDK selecionará o perfil com a taxa de bits mais baixa acima da taxa de bits mínima. Se a taxa inicial estiver acima da taxa máxima, o TVSDK selecionará a taxa mais alta abaixo da taxa máxima. </p> <p>Se a taxa de bits inicial for zero ou indefinida, a taxa de bits inicial será determinada pela política ABR. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Taxa de bits mínima </td> 
   <td colname="col2"> <p>A taxa de bits mais baixa permitida para a qual o ABR pode alternar. A switching ABR ignora perfis com uma taxa de bits inferior a essa taxa de bits. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Taxa de bits máxima </td> 
   <td colname="col2"> <p>A taxa de bits mais alta permitida para a qual o ABR pode alternar. A switching ABR ignora perfis com uma taxa de bits superior a essa taxa de bits. </p> </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se das seguintes informações:

* O TVSDK não despacha eventos da switching de taxa de bits.
* Você pode alterar as configurações do ABR a qualquer momento e o reprodutor alterna para usar o perfil que melhor corresponde às configurações mais recentes.

Por exemplo, se um fluxo tiver os seguintes perfis:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se você especificar um intervalo de 300000 a 2000000, o TVSDK considerará somente os perfis 1, 2 e 3. Isso permite que os aplicativos se ajustem a várias condições de rede, como alternar do WiFi para 3G ou para vários dispositivos, como um telefone, um tablet ou um desktop.

## Configurar taxas de bits adaptáveis {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

Para configurar parâmetros de taxa de bits adaptáveis do TVSDK:

1. Configurar uma instância de `PTABRControlParameters` para definir as configurações de taxa de bits inicial, mínima e máxima.

   Os valores padrão são exibidos no seguinte trecho de código, mas o aplicativo pode definir qualquer valor inteiro para cada um desses parâmetros.

   >[!IMPORTANT]
   >
   >Especifique as configurações de taxa de bits em bits por segundo (bps).

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
   
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. Atualize seu `PTMediaPlayer` instância com o configurado `PTABRControlParameters` instância.

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

Lembre-se do seguinte:

* O aplicativo deve definir a variável `abrControlParameters` propriedade em `PTMediaPlayer` antes de configurar um `PTMediaPlayerItem` para que as configurações de taxa de bits inicial e mínima entrem em vigor.

  Depois que a reprodução do conteúdo é iniciada, a configuração de uma nova instância afeta apenas a configuração da taxa de bits máxima.

* Para atualizar a configuração de taxa máxima de bits durante a reprodução, crie um novo `PTABRControlParameters` instância e defina-a na instância do reprodutor.
* Você pode atualizar a configuração de taxa máxima de bits durante a reprodução somente no iOS 8.0 e versões posteriores. Para versões anteriores, a variável `maxBitrate` que foi definido antes de ser usada a reprodução do conteúdo.
