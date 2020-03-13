---
description: Use o comando HTTP GET para interagir com o servidor manifest.
seo-description: Use o comando HTTP GET para interagir com o servidor manifest.
seo-title: Enviar um comando para o servidor de manifesto
title: Enviar um comando para o servidor de manifesto
uuid: e9680563-d268-406d-87ce-1521a677e9ec
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Enviar um comando para o servidor de manifesto {#send-a-command-to-the-manifest-server}

Use o comando HTTP GET para interagir com o servidor manifest.

1. Envie uma `HTTP GET` solicitação para um URL de inicialização construído com o seguinte padrão:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **PublisherAssetID** obrigatório. ID exclusiva do editor para o conteúdo específico.

* **URL** do conteúdo obrigatório. URL do arquivo M3U8 de conteúdo, Base64 codificado para ser seguro dentro do URL do servidor manifest. O URL do conteúdo deve apontar para um arquivo M3U8 variante, mesmo se houver apenas um fluxo de taxa de bits.

* **Parâmetros** de consulta Alguns são obrigatórios, alguns opcionais. Estes constituem a parte mais variada do pedido. Eles informam ao servidor manifest qual tipo de cliente está fazendo a solicitação e o que ele deseja que o servidor manifest faça.

   Por exemplo:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **Solicitações HTTP vs. HTTPS**

   O servidor manifest cria URLs usando o mesmo protocolo HTTP da solicitação do cliente. Se um player fizer uma solicitação HTTP não segura (http), o servidor manifest retornará URLs de manifesto e URLs de rastreamento Auditude com o protocolo http. Se um player fizer uma conexão segura HTTP (https), servidor manifest, ele retornará URLs de manifesto e URLs de rastreamento Auditude com o protocolo https.

   >[!NOTE]
   >
   >O servidor manifest não pode alterar o protocolo (HTTP ou HTTPS) de segmentos de conteúdo (.ts) e beacons de rastreamento de terceiros. Você deve entrar em contato com o conteúdo e os provedores de anúncios de terceiros para que eles configurem os protocolos desejados.