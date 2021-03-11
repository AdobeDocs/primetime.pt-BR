---
description: Os gerentes de recursos atuam como wrappers ao redor da biblioteca TVSDK.
title: Estrutura de execução de referência
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# Estrutura de implementação de referência {#reference-implementation-structure}

Os gerentes de recursos atuam como wrappers ao redor da biblioteca TVSDK.

Em Java, as classes são estruturadas em uma hierarquia. Por exemplo, todo o código relacionado à interface do usuário em `com.adobe.primetime.reference.ui` e todos os gerentes de recurso estão em `com.adobe.primetime.reference.manager`.

A implementação de referência do Primetime contém os seguintes pacotes:

| Embalagem | Descrição |
|--- |--- |
| [com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | Essa classe estende android.app.Application. |
| [com.adobe.primetime.reference.advertising](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | Contém código para anúncios personalizados. |
| [com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | Contém o código de interface necessário para configurar os gerentes de recursos. |
| [com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | Contém classes auxiliares para DRM. |
| [com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | Adaptadores e adaptadores de item para informações de interface, plataforma e referência. Também inclui o código FeedAdapterFactory, ContentRenditionInfo e XMLParserHelper. |
| [com.adobe.primetime.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | Fornece classes para registro local e remoto. |
| [com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | É aqui que você pode encontrar os gerentes de recursos, bem como o ManagerFactory. Para recursos opcionais que podem ser ativados ou desativados, há dois gerentes de recursos: <ul><li>Um gerenciador de recursos que é o nome do recurso, por exemplo, CCManager. Este gerenciador de recursos está desativado e fornece o comportamento padrão de desativação.</li><li>Um gerenciador de recursos que tem On anexado ao nome do gerenciador de recursos, por exemplo, CCManagerOn. Este gerenciador de recursos fornece código de amostra para o recurso ativado.</li></ul> |
| [com.adobe.primetime.reference.ui.catalog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | Contém o código da interface do usuário para o catálogo. |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | Contém o código da interface do usuário para o log. |
| [com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | Contém o código da interface do usuário para o reprodutor. |
| [com.adobe.primetime.reference.ui.settings](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | Contém o código da interface do usuário para configurações. |
| [com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | Contém classes de utilitário geral. |
| [com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | Contém `HTTP-specific` classes de utilitário. |
