---
description: Os fluxos HLS e DASH fornecem codificações (perfis) de taxa de bits diferentes para a mesma sequência curta de vídeo. O TVSDK pode selecionar o nível de qualidade para cada rajada com base na largura de banda disponível.
seo-description: Os fluxos HLS e DASH fornecem codificações (perfis) de taxa de bits diferentes para a mesma sequência curta de vídeo. O TVSDK pode selecionar o nível de qualidade para cada rajada com base na largura de banda disponível.
seo-title: Taxas de bits adaptáveis (ABR) para qualidade de vídeo
title: Taxas de bits adaptáveis (ABR) para qualidade de vídeo
uuid: a9b9a6a8-4098-4952-90e7-684e64800b3f
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d

---


# Taxas de bits adaptáveis (ABR) para qualidade de vídeo {#adaptive-bit-rates-abr-for-video-quality}

Os fluxos HLS e DASH fornecem codificações (perfis) de taxa de bits diferentes para a mesma sequência curta de vídeo. O TVSDK pode selecionar o nível de qualidade para cada rajada com base na largura de banda disponível.

O TVSDK monitora constantemente a taxa de bits para garantir que o conteúdo seja reproduzido na taxa de bits ideal para a conexão de rede atual.

Você pode definir a política de switching de taxa de bits adaptável (ABR) e as taxas de bits inicial, mínima e máxima para um fluxo de taxa de bits múltipla (MBR). O TVSDK muda automaticamente para a taxa de bits que fornece a melhor experiência de reprodução na configuração especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Taxa de bits inicial </td> 
   <td colname="col2"> <p>A taxa de bits de reprodução desejada (em bits por segundo) para o primeiro segmento. Quando a reprodução é iniciada, o perfil mais próximo, que é igual ou maior à taxa de bits inicial, é usado para o primeiro segmento. </p> <p> Se uma taxa de bits mínima for definida e a taxa de bits inicial for inferior à taxa mínima, o TVSDK selecionará o perfil com a taxa de bits mais baixa acima da taxa de bits mínima. Se a taxa inicial estiver acima da taxa máxima, o TVSDK selecionará a taxa mais alta abaixo da taxa máxima. </p> <p>Se a taxa de bits inicial for zero ou indefinida, a taxa de bits inicial será determinada pela política ABR. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Taxa mínima de bits </td> 
   <td colname="col2"> <p>A menor taxa de bits permitida para a qual o ABR pode alternar. A alternância ABR ignora perfis com uma taxa de bits inferior a essa taxa de bits. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Taxa máxima de bits </td> 
   <td colname="col2"> <p>A maior taxa de bits permitida para a qual o ABR pode alternar. A alternância ABR ignora perfis com uma taxa de bits superior a essa taxa de bits. </p> </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se das seguintes informações:

* O TVSDK não despacha eventos de alternância de taxa de bits.
* Você pode alterar as configurações de ABR a qualquer momento, e o player muda para usar o perfil que mais corresponde às configurações mais recentes.

Por exemplo, se um fluxo tiver os seguintes perfis:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se você especificar um intervalo de 300000 a 2000000, o TVSDK considerará somente os perfis 1, 2 e 3. Isso permite que os aplicativos se ajustem a várias condições de rede, como mudar de WiFi para 3G ou para vários dispositivos, como telefone, tablet ou desktop.

## Configurar taxas de bits adaptáveis {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

Para configurar parâmetros adaptáveis de taxa de bits do TVSDK:

1. Configure uma instância do para definir `PTABRControlParameters` as configurações iniciais, mínimas e máximas de taxa de bits.

   Os valores padrão são exibidos no trecho de código a seguir, mas seu aplicativo pode definir qualquer valor inteiro para cada um desses parâmetros.

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

1. Atualize sua `PTMediaPlayer` instância com a `PTABRControlParameters` instância configurada.

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

Lembre-se do seguinte:

* O aplicativo deve definir a propriedade `abrControlParameters` em `PTMediaPlayer` antes de configurar uma `PTMediaPlayerItem` instância para que as configurações iniciais e mínimas de taxa de bits entrem em vigor.

   Após o início da reprodução do conteúdo, a configuração de uma nova instância afeta apenas a configuração máxima de taxa de bits.

* Para atualizar a configuração de taxa de bits máxima durante a reprodução, crie uma nova `PTABRControlParameters` instância e defina-a na instância do player.
* Você pode atualizar a configuração de taxa de bits máxima durante a reprodução somente no iOS 8.0 e posterior. Para versões anteriores, o `maxBitrate` valor definido antes da reprodução do conteúdo começar é usado.