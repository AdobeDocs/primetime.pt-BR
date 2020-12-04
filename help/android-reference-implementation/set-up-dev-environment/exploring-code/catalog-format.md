---
description: A implementação de referência Primetime usa um formato de feed baseado em JSON para respostas. Este formato é analisado usando uma implementação da interface IFeedItemAdapter.
seo-description: A implementação de referência Primetime usa um formato de feed baseado em JSON para respostas. Este formato é analisado usando uma implementação da interface IFeedItemAdapter.
seo-title: Formato do catálogo
title: Formato do catálogo
uuid: 6e1a526f-c0bb-403d-a792-666caf5479a5
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---


# Formato de catálogo {#catalog-format}

A implementação de referência Primetime usa um formato de feed baseado em JSON para respostas. Este formato é analisado usando uma implementação da interface IFeedItemAdapter.

>[!NOTE]
>
>Esse formato de feed é o formato de amostra que a implementação de referência usa e serve como um exemplo de como o formato pode ser analisado e mapeado para a interface de feed. Você pode usar seu próprio formato de feed de entrada com suas próprias implementações de interface de feed.

Em um nível alto, o formato consiste em uma matriz de entradas de conteúdo. Cada entrada representa um conteúdo de vídeo publicado ao vivo ou VOD:

```
{
    "entries": [
        {
        },
        {
        },
        ...
    ]
}
```

Cada entrada de feed é um objeto JSON com um determinado conjunto de atributos:

```
{
    "entries": [
        
            "id": "episode1",
            "title": "My episode1",
            "description": "This is an episode.",
            "categories": "documentary, educational, children",
            "keywords": "List, of, comma, separated, keywords",
            "isLive": false,
            "content":  [
                
                },
                
                },
            ],
            "thumbnails": [
                
                },
                
                }
            ]
            "metadata": 
            } 
        }
    ]
}
```

| Propriedade | Descrição |
|---|---|
| `id` | Um identificador/guia exclusivo para o conteúdo, conforme definido pelo sistema de publicação de feed. |
| `title` | Um título para o conteúdo. |
| `description` | Uma descrição do conteúdo. |
| `categories` | Uma lista de categorias marcada para o conteúdo que pode ser usada pelo aplicativo para aprimorar a experiência do usuário. Leia as propriedades do conteúdo. |
| `keywords` | Uma lista de palavras-chave separadas por vírgulas pode ser usada pelo aplicativo para aprimorar a experiência do usuário. Leia as propriedades do conteúdo. |
| `isLive` | true ou false, indicando se é um fluxo Live ou VOD. |
| `content` | Uma matriz de objetos JSON com formatos alternativos para o conteúdo junto com os URLs correspondentes. Por exemplo, pode haver urls para os formatos f4m e m3u8. Os atributos do objeto JSON são descritos mais adiante. |
| `thumbnails` | Uma matriz de objetos JSON com urls para tamanhos diferentes de miniaturas. Os atributos do objeto JSON são definidos abaixo. |
| `metadata` | Um objeto JSON que define metadados para o conteúdo, atualmente esses metadados estão limitados aos metadados relacionados ao anúncio. O objeto de metadados é definido abaixo. |

O seguinte bloco de código define os objetos JSON que formam a matriz de **objetos de conteúdo**:

```
"content":  [
    {
        "format": "M3U8",
        "url": "https://adobeprimetime-f.akamaihd.net/i/
<i>longstringofcharacters</i>/
                 Episode_,640x360_1000,640x360_700,_b.mp4.csmil/master.m3u8",
        "language": "en"
    }  
],
```

| Propriedade | Descrição |
|--- |--- |
| format | É necessário ter o formato m3u8 para Android. |
| url | O url para o fluxo de vídeo para o formato especificado. |

O seguinte bloco de código define os objetos JSON que formam a matriz de **objetos miniatura**:

```
"thumbnails": [
    {
        "format": "JPEG",
        "height":  "90",
        "width": "160",
        "url": "https://example.com/small.jpg"
    },
    {
        "format": "JPEG",
        "height": "450",
        "width": "800",
        "url": "https://example.com/large.jpg"
    }
],
```

| Propriedade | Descrição |
|---|---|
| format | Uma string que indica o formato do arquivo de miniatura, por exemplo, JPEG, PNG etc. |
| altura | A altura da miniatura. No aplicativo de referência, a miniatura com menor altura e largura é retornada como a miniatura pequena e aquela com maior largura e altura é retornada como a miniatura grande. |
| largura | A largura da miniatura. No aplicativo de referência, a miniatura com menor altura e largura é retornada como a miniatura pequena e aquela com maior largura e altura é retornada como a miniatura grande. |
| url | O url para o arquivo em miniatura. |

O seguinte bloco de código define o objeto **metadata**:

```
"metadata" : {
    "ad" : {
        "type" : "",
        "details" : {
        }
    }
    "entitlement" : {
        "id" : ""
    }
}
```

| Propriedade | Descrição |
|--- |--- |
| anúncio | Metadados relacionados ao anúncio. |
| type | O valor pode ser Anúncios Primetime, Quebras de anúncios diretos ou Marcadores de anúncios personalizados. <br/><br/>O PSDK fornece suporte integrado para os seguintes tipos de metadados: Metadados relacionados ao Auditude para o Primetime Ad Serving (Anúncios Primetime), pausas de anúncio diretas com urls de anúncio (Quebras de anúncio direto) e marcadores de anúncio personalizados que fornecem o TimeRange para cada marcador de anúncio (Marcadores de anúncio personalizados). Cada tipo tem um AdProvider integrado no PSDK que processa os metadados.  <br/><br/>O formato JSON para cada um deles foi definido abaixo. |
| detalhes | Inclui os atributos de metadados do anúncio. Ambos os tipos de metadados de anúncio têm seu próprio conjunto de atributos definidos abaixo. Para os tipos incorporados, os atributos incluídos definem os dados esperados pelo PSDK para esse tipo. |
| direito | Metadados relacionados ao direito |
| id | ID do recurso de mídia usada para solicitações de autorização do serviço de passagem de TV paga da Adobe Primetime. A ID pode ser uma string de texto ou uma string mRSS codificada em HTML. Qualquer conteúdo de mídia que exija autorização deve conter uma ID de recurso válida. |

