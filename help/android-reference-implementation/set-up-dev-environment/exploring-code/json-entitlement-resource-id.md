---
title: Objeto JSON para ID de recurso de direito
description: O bloco de código a seguir fornece um exemplo de um objeto JSON quando a ID do recurso de direito é uma string de texto simples.
exl-id: 396c43e7-404a-40f5-8113-a720e2c834e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Objeto JSON para ID de recurso de direito {#json-object-for-entitlement-resource-id}

O bloco de código a seguir fornece um exemplo de um objeto JSON quando a ID do recurso de direito é uma string de texto simples. Nesse caso, a ID do recurso é a cadeia de caracteres &quot;resource&quot;.

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

O bloco de código a seguir fornece um exemplo de um objeto JSON quando a ID de recurso de direito é uma string mRSS codificada em HTML.

```
<rss version="2.0" xmlns:media="https://search.yahoo.com/mrss/"> 
<channel> 
<title>REF_ADOBE</title> 
<item> 
<title>Adobe Primetime Reference</title> 
<guid>1234</guid> 
<media:rating scheme="urn:v-chip">TV-PG</media:rating> 
</item> 
</channel> 
</rss>
```

A cadeia de caracteres mRSS a seguir é usada como a ID do recurso.

```
"metadata" : { 
    "entitlement" : { 
        "id" : "<rss version=&quot;2.0&quot; 
        xmlns:media=&quot; 
        https://search.yahoo.com/mrss/&quot; 
        ><channel><title>REF_ADOBE</title><item> 
        <title>Adobe Primetime Reference</title><guid> 
        1234</guid><media:rating scheme=&quot;urn:v-chip&quot;> 
        TV-PG</media:rating></item></channel></rss>" 
        } 
} 
```
