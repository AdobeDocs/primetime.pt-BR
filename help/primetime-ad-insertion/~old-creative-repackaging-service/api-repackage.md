---
description: Você pode usar a API de reempacotamento do CRS para transcodificar anúncios não HLS antecipadamente, de modo que uma versão do HLS esteja disponível quando precisar executá-la, eliminando o atraso de 2 a 4 minutos associado ao reempacotamento just-in-time (JIT).
title: Reempacotar API
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---


# Reempacotando API {#repackaging-api}

Você pode usar a API de reempacotamento do CRS para transcodificar anúncios não HLS antecipadamente, de modo que uma versão do HLS esteja disponível quando precisar executá-la, eliminando o atraso de 2 a 4 minutos associado ao reempacotamento just-in-time (JIT).

## Solicitação HTTP {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

Envie um comando HTTP POST para o URL especificado para informar ao CRS qual anúncio você deseja transcodificar e quais opções você gostaria que ele usasse. O código de resposta relata o sucesso ou a falha e outras informações.

Esta solicitação requer um nome de usuário e senha. Você pode obtê-los do gerente técnico de conta do Adobe. Se precisar de informações sobre autenticação, entre em contato com seu representante do Adobe Primetime Enablement.

Para enviar uma solicitação de transcodificação para o CRS, envie uma mensagem HTTP da seguinte maneira:

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **Método -** `POST`

* **Auth -** `Digest`

* **Cabeçalho -** `Content-Type: text/xml`

* **Body -** XML como no exemplo a seguir:

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

O bloco `RepackageList` no Corpo pode conter de 1 a 300 blocos `Repackage`. Se o número de blocos `Repackage` no Corpo exceder 300, a Solicitação HTTP falhará com o seguinte erro:

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


Os parâmetros obrigatórios e opcionais em um bloco `Repackage` são os seguintes:

* **`AdSystem`** (Obrigatório) - O servidor de anúncios de origem, por exemplo,  `Auditude`,  `FreeWheel`,  `Apad.tv`. Este é um valor de string que corresponde ao elemento VAST `AdSystem`.

* **`AdId`** (Obrigatório) - Esse é um identificador do servidor de anúncios de terceiros especificado na solicitação. Corresponde ao atributo `id` do elemento `Ad` em uma resposta VAST.

* **`CreativeURL`** (Obrigatório) - O local (URI) do anúncio que será transcodificado. Isso corresponde ao elemento VAST `MediaFile` .

* `CreativeID` (opcional) - o identificador da campanha criativa que deve ser incluído como parte da experiência de anúncio.
* **`Zone`** (Obrigatório) - ID da zona de sua conta (obter do gerente de conta técnico). Este é um valor numérico que corresponde à configuração da plataforma Auditude `publisher_site_id` .

* **`Format`** (opcional) - Parâmetros para controlar como o CRS transcodifica a criação do anúncio:

   * `clientside` - Gere saída compatível com o URL que o TVSDK usa para se comunicar com o CDN.
   >[!IMPORTANT]
   >
   >Você deve fornecer esse parâmetro se desejar que o anúncio reempacotado seja compatível com o Ad Insertion do lado do cliente. Se você não fornecer isso, o anúncio reempacotado só será compatível com o Ad Insertion do servidor.

   * `hls` - Gere um anúncio transcodificado compatível com HLS.
   * `dash` - Gere um anúncio transcodificado compatível com DASH.
   * `id3` - Insira as tags de metadados cronometradas ID3 no anúncio transcodificado.
   * `targetdur` - Duração do segmento (em segundos) para a criação do anúncio transcodificado. O padrão é `targetdur=4`. Esse valor deve corresponder ao valor especificado no manifesto para `<s>` na tag de duração do target: `#EXT-X-TARGETDURATION:<s>`.

   >[!NOTE]
   >
   >Os ativos compatíveis com DASH não são compatíveis com a inserção de anúncios do Adobe Primetime.

>[!IMPORTANT]
>
>Para garantir uma reprodução mais suave, defina `targetdur` para corresponder à duração do segmento de conteúdo.

## Resposta HTTP {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

O CRS responde à solicitação com um dos seguintes códigos de status:

* **HTTP 202**  - Aceito (com corpo vazio). Isso indica sucesso. O CRS carrega o anúncio transcodificado no servidor CDN.
* **HTTP 400**  - Solicitação inválida. O XML publicado é inválido.
* **HTTP 500**  - Erro interno do servidor. O servidor encontrou um problema interno (por exemplo, o servidor não pôde se conectar a um banco de dados).

## Ativos de pré-transcodificação para SSAI ou CSAI {#section_098888BB74FD4DC1AD0BD507B2A48318}

Usando a API de reempacotamento, você pode pré-transcodificar futuros eventos SSAI ou CSAI. Se os ativos forem destinados a serem usados com o SSAI no futuro, verifique se todos os parâmetros nas chamadas do POST são exclusivos. Os parâmetros são: AdSystem, AdId, CreativeURL, Zone, Format. Quaisquer diferenças nesse conjunto de parâmetros, resultarão em uma nova solicitação de transcodificação para SSAI.

Para ativos usados com o CSAI no futuro, a exclusividade do ativo depende do Zone e do CreativeURL. O AdSystem e o AdId não resultam em diferentes ativos transcodificados e estão disponíveis para os clientes.
