---
title: Identificação de recursos protegidos
description: Identificação de recursos protegidos
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# Identificação de recursos protegidos {#identifying-protected-resources}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#overview}

Cada pedido de autorização (ou pedido para verificar a autorização) deve conter um identificador único para o recurso protegido ao qual o utilizador está a pedir acesso. Um recurso protegido pode ser qualquer nível de conteúdo autorizado, conforme acordado entre um MVPD e programadores participantes. Os potenciais recursos protegidos devem se encaixar nesta estrutura em árvore de granularidade cada vez mais específica:

- Rede
   - Canal
      - Mostrar
         - Episódio
            - Ativo\
                

</br>

## Formato RSS de mídia {#media_rss}

Os recursos podem ser identificados por uma string simples (um identificador exclusivo para um canal) ou podem ser representados no formato RSS de mídia (MRSS), conforme acordado entre o Adobe (ou um parceiro autorizado de autenticação da Adobe Primetime) e os MVPDs e Programadores participantes. A sequência de caracteres de RSS usada como um especificador de recursos pode incluir informações adicionais, como classificações e metadados de controle dos pais.\
 

Se você usar um identificador de recurso simples, como &quot;TNT&quot;, assume-se que representa um canal e é traduzido neste especificador de recurso RSS:

```RSS
    <rss version="2.0"> 
        <channel>
            <title>TNT</title>
        </channel>
    </rss>
```
 

Um especificador mais complexo pode incluir, por exemplo, informações adicionais de classificação. Você pode passar toda a cadeia de caracteres de RSS para funções do Ativador de Acesso que exigem uma ID de recurso, como [`getAuthorization()`](/help/authentication/rest-api-reference.md):

```rss
    var resource = 
        '<rss version="2.0" xmlns:media="http://search.yahoo.com/mrss/"> 
             <channel>
                 <title>TNT</title>
                 <media:rating scheme="urn:mpaa">pg</media:rating>
             </channel>
         </rss>'; 
    getAuthorization(resource);
```

Os especificadores de recursos são opacos para a autenticação da Adobe Primetime; são simplesmente passados para o MVPD. Se o MVPD não reconhecer ou não puder analisar o especificador de recursos, ele retornará um erro para a autenticação da Adobe Primetime, que retornará o erro ao seu `tokenRequestFailed()` retorno de chamada.

<!--
## Related Information {#related}

-  User Metadata
-  Preflight Authorization
-->