---
description: Use o comando HTTP GET para interagir com o servidor de manifesto.
title: Enviar um comando para o servidor de manifesto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Enviar um comando para o Servidor Manifesto {#send-a-command-to-the-manifest-server}

Use o comando HTTP GET para interagir com o servidor de manifesto.

1. Envie uma solicitação `HTTP GET` para um URL de inicialização construído usando o seguinte padrão:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **** PublisherAssetIDRequired. ID exclusiva do editor para o conteúdo específico.

* **Conteúdo** URLRequired. URL do arquivo M3U8 de conteúdo, Base64 codificado para ser seguro no URL do servidor de manifesto. O URL de conteúdo deve apontar para um arquivo M3U8 de variante, mesmo se houver apenas um fluxo de taxa de bits.

* **Parâmetros** de consultaAlguns são obrigatórios, alguns opcionais. Estas constituem a parte mais variada do pedido. Elas informam ao servidor de manifesto qual tipo de cliente está fazendo a solicitação e o que ele deseja que o servidor de manifesto faça.

   Por exemplo:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **Solicitações HTTP versus HTTPS**

   O servidor manifest cria URLs usando o mesmo protocolo HTTP da solicitação do cliente. Se um reprodutor fizer uma solicitação HTTP (http) não segura, o servidor de manifesto retornará URLs de manifesto e URLs de rastreamento Auditude com o protocolo http. Se um reprodutor faz uma conexão HTTP segura (https), servidor de manifesto, ele retorna URLs de manifesto e URLs de rastreamento Auditude com o protocolo https.

   >[!NOTE]
   >
   >O servidor de manifesto não pode alterar o protocolo (HTTP ou HTTPS) dos segmentos de conteúdo (.ts) e beacons de rastreamento de terceiros. Você deve entrar em contato com o conteúdo e os provedores de anúncios de terceiros para que eles configurem os protocolos desejados.