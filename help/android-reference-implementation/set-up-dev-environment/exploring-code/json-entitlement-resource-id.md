---
seo-title: Objeto JSON para ID de recurso de direito
title: Objeto JSON para ID de recurso de direito
uuid: f5b659da-1732-404c-bf00-d32a0ae39aa1
description: O bloco de código a seguir fornece um exemplo de um objeto JSON quando a ID do recurso de direito é uma sequência de texto simples.
seo-description: O bloco de código a seguir fornece um exemplo de um objeto JSON quando a ID do recurso de direito é uma sequência de texto simples.
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Objeto JSON para ID de recurso de direito {#json-object-for-entitlement-resource-id}

O bloco de código a seguir fornece um exemplo de um objeto JSON quando a ID do recurso de direito é uma sequência de texto simples. Nesse caso, a ID do recurso é a string &quot;resource&quot;.

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

O bloco de código a seguir fornece um exemplo de um objeto JSON quando a ID do recurso de direito é uma string mRSS codificada em HTML.

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

A seguinte string mRSS é usada como a id do recurso.

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
