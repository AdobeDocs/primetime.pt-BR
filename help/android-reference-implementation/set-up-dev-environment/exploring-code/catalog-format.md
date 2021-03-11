---
description: A implementação de referência do Primetime usa um formato de feed baseado em JSON para respostas. Este formato é analisado usando uma implementação da interface IFeedItemAdapter.
title: Formato do catálogo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---


# Formato do catálogo {#catalog-format}

A implementação de referência do Primetime usa um formato de feed baseado em JSON para respostas. Este formato é analisado usando uma implementação da interface IFeedItemAdapter.

>[!NOTE]
>
>Esse formato de feed é o formato de amostra que a implementação de referência usa e serve como exemplo de como o formato pode ser analisado e mapeado para a interface de feed. Você pode usar seu próprio formato de feed de entrada com suas próprias implementações da interface de feed.

Em um nível alto, o formato consiste em uma matriz de entradas de conteúdo. Cada entrada representa um conteúdo de vídeo publicado em tempo real ou VOD:

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
| `categories` | Uma lista de categorias marcadas para o conteúdo que pode ser usado pelo aplicativo para aprimorar a experiência do usuário. Leia as propriedades do conteúdo. |
| `keywords` | Uma lista de palavras-chave separadas por vírgulas pode ser usada pelo aplicativo para aprimorar a experiência do usuário. Leia as propriedades do conteúdo. |
| `isLive` | verdadeiro ou falso, indicando se é um fluxo Live ou VOD. |
| `content` | Uma matriz de objetos JSON com formatos alternativos para o conteúdo junto com os URLs correspondentes. Por exemplo, pode haver urls para os formatos f4m e m3u8. Os atributos do objeto JSON são descritos mais abaixo. |
| `thumbnails` | Uma matriz de objetos JSON com urls para tamanhos diferentes de miniaturas. Os atributos do objeto JSON são definidos abaixo. |
| `metadata` | Um objeto JSON que define metadados para o conteúdo, atualmente esses metadados estão limitados a metadados relacionados a anúncios. O objeto de metadados é definido abaixo. |

O bloco de código a seguir define os objetos JSON que formam a matriz de **objetos de conteúdo**:

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
| format | Precisa estar no formato m3u8 para Android. |
| url | O url para o fluxo de vídeo do formato especificado. |

O bloco de código a seguir define os objetos JSON que formam a matriz de **objetos miniatura**:

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
| altura | A altura da miniatura. No aplicativo de referência, a miniatura com menor altura e largura é retornada como a miniatura e a com maior largura e altura é retornada como a miniatura grande. |
| largura | A largura da miniatura. No aplicativo de referência, a miniatura com menor altura e largura é retornada como a miniatura e a com maior largura e altura é retornada como a miniatura grande. |
| url | O url para o arquivo de miniatura. |

O bloco de código a seguir define o **objeto de metadados**:

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
| ad | Metadados relacionados a anúncios. |
| type | O valor pode ser Anúncios do Primetime, Quebras de anúncios diretas ou Marcadores de anúncios personalizados. <br/><br/>O PSDK fornece suporte integrado para os seguintes tipos de metadados: Metadados relacionados ao Auditude para o Primetime Ad Serving (anúncios Primetime), ad breaks diretos com urls de anúncios (Direct Ad Breaks) e marcadores de anúncios personalizados que fornecem o Intervalo de tempo para cada marcador de anúncio (Marcadores de anúncios personalizados). Cada tipo tem um AdProvider integrado no PSDK que processa os metadados.  <br/><br/>O formato JSON para cada um deles foi definido abaixo. |
| detalhes | Inclui os atributos de metadados do anúncio. Ambos os tipos de metadados de anúncios têm seu próprio conjunto de atributos definidos abaixo. Para os tipos incorporados, os atributos incluídos definem os dados esperados pelo PSDK para esse tipo. |
| direito | Metadados relacionados a direitos |
| id | ID do recurso de mídia usada para solicitações de autorização contra o serviço de passagem da TV paga do Adobe Primetime. A ID pode ser uma string de texto ou uma string mRSS codificada em HTML. Qualquer conteúdo de mídia que exija autorização deve conter uma ID de recurso válida. |

