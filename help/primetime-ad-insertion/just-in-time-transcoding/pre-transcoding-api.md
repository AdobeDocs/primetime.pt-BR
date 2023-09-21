---
title: API de pré-transcodificação
description: Você pode usar a API de reempacotamento just-in-time para transcodificar anúncios criados antecipadamente, de modo que versões compatíveis com o conteúdo estejam disponíveis quando necessário, eliminando o atraso de 2 a 4 minutos associado ao reempacotamento just-in-time (JIT).
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# API de pré-transcodificação e reempacotamento {#pre-transcoding-api}

O Primetime Ad Insertion oferece uma API de pré-transcodificação para situações em que os URLs criativos são conhecidos antecipadamente, como para grandes eventos vendidos diretamente.  Isso elimina o atraso de 2 a 4 minutos associado à transcodificação just-in-time.

## Solicitação HTTP {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

Envie um comando HTTP POST para o URL especificado para informar ao CRS qual anúncio criativo você deseja transcodificar e quais opções você deseja que ele use. O código de resposta informa o sucesso ou a falha e outras informações.

Esta solicitação requer um nome de usuário e senha. Você pode obtê-las em seu gerente técnico de conta da Adobe. Se precisar de informações sobre autenticação, entre em contato com o representante de Ativação da Adobe Primetime.

Para enviar uma solicitação de transcodificação para o CRS, envie uma mensagem HTTP da seguinte maneira:

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **Método -** `POST`

* **Autenticação -** `Digest`

* **Cabeçalho -** `Content-Type: text/xml`

* **Corpo -** XML, como no exemplo a seguir:

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

A variável `RepackageList` bloco no corpo pode conter de 1 a 300 `Repackage` blocos. Se o número de `Repackage` no Corpo exceder 300, então a Solicitação HTTP falhará com o seguinte erro:

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


Os parâmetros obrigatórios e opcionais em um `Repackage` bloco são os seguintes:

* **`AdSystem`** (Obrigatório) - O servidor de anúncios de origem, por exemplo, `Auditude`, `FreeWheel`, `Apad.tv`. Este é um valor de string que corresponde ao elemento VAST `AdSystem`.

* **`AdId`** (Obrigatório) - É um identificador para o servidor de anúncios de terceiros especificado na solicitação. Corresponde à `id` atributo de `Ad` elemento em uma resposta VAST.

* **`CreativeURL`** (Obrigatório) - O local (URI) do criativo do anúncio a ser transcodificado. Isso corresponde ao VAST `MediaFile` elemento.

* `CreativeID` (opcional) - O identificador do criativo do anúncio que deve ser incluído como parte da experiência do anúncio.
* **`Zone`** (Obrigatório) - ID de zona da sua conta (obtenha uma do gerente técnico de conta). Este é um valor numérico que corresponde à plataforma Auditude `publisher_site_id` configuração.

* **`Format`** (opcional) - Parâmetros para controlar como o CRS transcodifica a criação de anúncio:

   * `clientside` - Gerar saída compatível com o URL que o TVSDK usa para se comunicar com o CDN.

  >[!IMPORTANT]
  >
  >Você deve fornecer esse parâmetro se quiser que o anúncio reempacotado seja compatível com o Ad Insertion do lado do cliente. Se você não fornecer isso, o anúncio reempacotado será compatível somente com o Ad Insertion do lado do servidor.

   * `hls` - Gerar um anúncio transcodificado compatível com HLS e criativo.
   * `dash` - Gerar um anúncio transcodificado e criativo compatível com DASH.
   * `id3` - Insira tags de metadados com tempo de ID3 na campanha de criação de anúncios transcodificados.
   * `targetdur` - Duração do segmento (em segundos) para o anúncio transcodificado e criativo. O padrão é `targetdur=4`. Este valor deve corresponder ao valor especificado no manifesto para `<s>` na tag de duração do target: `#EXT-X-TARGETDURATION:<s>`.

  >[!NOTE]
  >
  >Os ativos compatíveis com DASH não são compatíveis com a inserção de anúncios no Adobe Primetime.

>[!IMPORTANT]
>
>Para garantir uma reprodução mais suave, defina `targetdur` para corresponder à duração do bloco de conteúdo.

## Resposta HTTP {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

O CRS responde à solicitação com um dos seguintes códigos de status:

* **HTTP 202** - Aceita (com corpo vazio). Isso indica sucesso. O CRS faz upload do anúncio transcodificado no servidor CDN.
* **HTTP 400** - Solicitação inválida. O XML publicado é inválido.
* **HTTP 500** - Erro interno do servidor. O servidor encontrou um problema interno (por exemplo, o servidor não pôde se conectar a um banco de dados).

## Ativos pré-transcodificados para SSAI ou CSAI {#section_098888BB74FD4DC1AD0BD507B2A48318}

Usando a API de reempacotamento, você pode pré-transcodificar futuros eventos SSAI ou CSAI. Se os ativos forem destinados a serem usados com SSAI no futuro, verifique se todos os parâmetros nas chamadas de POST são exclusivos. Os parâmetros são: AdSystem, AdId, CreativeURL, Zone, Format. Quaisquer diferenças nesse conjunto de parâmetros resultam em uma nova solicitação de transcodificação para o SSAI.

Para ativos usados com o CSAI no futuro, a exclusividade do ativo depende da Zona e do CreativeURL. O AdSystem e o AdId não resultam em ativos transcodificados diferentes e eles estão disponíveis para clientes.
