---
description: Você pode fornecer metadados personalizados sobre conteúdo, anúncios e chamadas de rastreamento de capítulo usando funções de retorno de chamada.
seo-description: Você pode fornecer metadados personalizados sobre conteúdo, anúncios e chamadas de rastreamento de capítulo usando funções de retorno de chamada.
seo-title: Implementação do suporte a metadados personalizados
title: Implementação do suporte a metadados personalizados
uuid: 068ef0b9-79a2-4e44-8a0a-01e9deb8e4a6
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Implementação do suporte a metadados personalizados {#implement-custom-metadata-support}

Você pode fornecer metadados personalizados sobre conteúdo, anúncios e chamadas de rastreamento de capítulo usando funções de retorno de chamada.

As funções de retorno de chamada são chamadas logo antes da chamada de rastreamento ser feita, de modo que seu aplicativo possa anexar os metadados específicos a um anúncio ou capítulo.

Chame funções de retorno de chamada para conteúdo, anúncios e capítulos.

```java
// Video Metadata Block 
vaMetadata.setVideoMetadataBlock(new VideoAnalyticsMetadata.VideoMetadataBlock() { 
    @Override 
    public HashMap<String, String> call() { 
        HashMap<String, String> result = new HashMap<String, String>(); 
        result.put("myvideoid", "1234"); 
        result.put("mysdkversion", Version.getVersion()); 
  
        return result; 
    } 
}); 
  
// Ad Metadata Block invoked on every ad start 
vaMetadata.setAdMetadataBlock(new VideoAnalyticsMetadata.AdMetadataBlock() { 
    @Override 
    public HashMap<String, String> call(Ad ad) { 
        HashMap<String, String> result = new HashMap<String, String>(); 
        result.put("myadid", "ad-1234"); 
        result.put("myad-sdkversion", Version.getVersion()); 
  
        return result; 
    } 
}); 
  
// Chapter Metadata Block invoked on every chapter start 
vaMetadata.setChapterMetadataBlock(new VideoAnalyticsMetadata.ChapterMetadataBlock() { 
    @Override 
    public HashMap<String, String> call(VideoAnalyticsChapterData chapter) { 
        HashMap<String, String> result = new HashMap<String, String>(); 
        result.put("mychapterid", "chapter-1234"); 
        result.put("mychapter-sdkversion", Version.getVersion()); 
  
        return result; 
    } 
});
```

