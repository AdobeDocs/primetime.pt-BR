---
description: Você pode usar a API de reempacotamento do CRS para transcodificar anúncios não HLS antecipadamente, de modo que uma versão HLS está disponível quando você precisa executá-la, eliminando o atraso de 2 a 4 minutos associado ao reempacotamento just-in-time (JIT).
seo-description: Você pode usar a API de reempacotamento do CRS para transcodificar anúncios não HLS antecipadamente, de modo que uma versão HLS está disponível quando você precisa executá-la, eliminando o atraso de 2 a 4 minutos associado ao reempacotamento just-in-time (JIT).
seo-title: API de reempacotamento
title: API de reempacotamento
uuid: 03cd2428-510a-4b99-8496-059a48d5abba
translation-type: tm+mt
source-git-commit: 5c026bfc678bafc08f93ad056823e36fd77a8a25

---


# API de reempacotamento {#repackaging-api}

Você pode usar a API de reempacotamento do CRS para transcodificar anúncios não HLS antecipadamente, de modo que uma versão HLS está disponível quando você precisa executá-la, eliminando o atraso de 2 a 4 minutos associado ao reempacotamento just-in-time (JIT).

## Solicitação HTTP {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

Envie um comando HTTP POST para o URL especificado para informar ao CRS qual anúncio você deseja transcodificar e quais opções você gostaria que ele usasse. O código de resposta informa sucesso ou falha e outras informações.

Esta solicitação requer um nome de usuário e senha. Você pode obtê-los do seu gerente técnico de contas da Adobe. Se precisar de informações sobre autenticação, entre em contato com seu representante do Adobe Primetime Enablement.

Para enviar uma solicitação de transcodificação ao CRS, envie uma mensagem HTTP da seguinte maneira:

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **Método -**`POST`

* **Ago -**`Digest`

* **Cabeçalho -**`Content-Type: text/xml`

* **Body -** XML, como no exemplo a seguir:

   ```xml
   <RepackageList>
       <Repackage>
           <AdSystem>Auditude</AdSystem>
           <AdID>AUD1</AdID>
           <CreativeID>AUD-CR1</CreativeID>
           <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
           <Zone>3</Zone>
       </Repackage>
       <Repackage>
           <AdSystem>Auditude</AdSystem>
           <AdID>AUD2</AdID>
           <CreativeID>AUD-CR1</CreativeID>
           <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
           <Format>id3 targetdur=5</Format>
           <Zone>3</Zone>
       </Repackage>
   </RepackageList>
   ```

O `RepackageList` bloco no Corpo pode conter de 1 a 300 `Repackage` blocos. Se o número de `Repackage` blocos no Corpo exceder 300, a Solicitação HTTP falhará com o seguinte erro:

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


Os parâmetros obrigatórios e opcionais em um `Repackage` bloco são os seguintes:

* **`AdSystem`** (Obrigatório) - O servidor de anúncio de origem, por exemplo, `Auditude`, `FreeWheel`, `Apad.tv`. Esse é um valor de string que corresponde ao elemento VAST `AdSystem`.

* **`AdId`** (Obrigatório) - Esse é um identificador do servidor de anúncios de terceiros especificado na solicitação. Corresponde ao `id` atributo do `Ad` elemento em uma resposta VAST.

* **`CreativeURL`** (Obrigatório) - O local (URI) do anúncio a ser transcodificado. Isso corresponde ao `MediaFile` elemento VAST.

* `CreativeID` (opcional) - o identificador do anúncio que deve ser incluído como parte da experiência do anúncio.
* **`Zone`** (Obrigatório) - ID da zona da sua conta (obter do seu gerente técnico de contas). Este é um valor numérico que corresponde à configuração da plataforma Auditude `publisher_site_id` .

* **`Format`** (opcional) - Parâmetros para controlar como o CRS transcodifica o anúncio criativo:

   * `clientside` - Gerar saída compatível com o URL que o TVSDK usa para se comunicar com o CDN.
   >[!IMPORTANT]
   >
   >Você deve fornecer esse parâmetro se desejar que o anúncio reempacotado seja compatível com a inserção do anúncio no lado do cliente. Se você não fornecer isso, o anúncio reempacotado só será compatível com a inserção do anúncio no lado do servidor.

   * `hls` - Gerar um anúncio transcodificado compatível com HLS.
   * `dash` - Gerar um anúncio transcodificado compatível com DASH.
   * `id3` - Injete tags de metadados cronometradas ID3 no anúncio transcodificado.
   * `targetdur` - Duração do segmento (em segundos) para o anúncio transcodificado. O padrão é `targetdur=4`. Esse valor deve corresponder ao valor especificado no manifesto para `<s>` a tag de duração de destino: `#EXT-X-TARGETDURATION:<s>`.
   >[!NOTE]
   >
   >Os ativos compatíveis com DASH não são compatíveis com a inserção de anúncios do Adobe Primetime.

>[!IMPORTANT]
>
>Para garantir uma reprodução mais suave, defina `targetdur` para corresponder à duração do bloco de conteúdo.

## Resposta HTTP {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

O CRS responde à solicitação com um dos seguintes códigos de status:

* **HTTP 202** - Aceito (com corpo vazio). Isso indica sucesso. O CRS carrega o anúncio transcodificado no servidor CDN.
* **HTTP 400** - Solicitação incorreta. O XML publicado é inválido.
* **HTTP 500** - Erro interno do servidor. O servidor encontrou um problema interno (por exemplo, o servidor não pôde se conectar a um banco de dados).

## Ativos de pré-transcodificação para SSAI ou CSAI {#section_098888BB74FD4DC1AD0BD507B2A48318}

Usando a API de reempacotamento, você pode pré-transcodificar futuros eventos SSAI ou CSAI. Se os ativos forem destinados a serem usados com o SSAI no futuro, verifique se todos os parâmetros nas chamadas POST são exclusivos. Os parâmetros são: AdSystem, AdId, CreativeURL, Zone, Format. Quaisquer diferenças neste conjunto de parâmetros resultarão em uma nova solicitação de transcodificação para SSAI.

Para ativos usados com CSAI no futuro, a exclusividade do ativo depende de Zone e CreativeURL. AdSystem e AdId não resultam em ativos transcodificados diferentes e estão disponíveis para clientes.
