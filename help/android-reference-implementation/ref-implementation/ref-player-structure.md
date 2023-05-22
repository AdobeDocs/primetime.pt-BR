---
description: Os gerenciadores de recursos atuam como invólucros da biblioteca TVSDK.
title: Estrutura de implementação de referência
exl-id: cf102ccc-2e31-4197-a321-e485f77ba754
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Estrutura de implementação de referência {#reference-implementation-structure}

Os gerenciadores de recursos atuam como invólucros da biblioteca TVSDK.

Em Java, as classes são estruturadas em uma hierarquia. Por exemplo, todo o código relacionado à interface em `com.adobe.primetime.reference.ui` e todos os gerenciadores de recursos estão em `com.adobe.primetime.reference.manager`.

A implementação de referência do Primetime contém os seguintes pacotes:

| Pacote | Descrição |
|--- |--- |
| [com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | Essa classe estende android.app.Application. |
| [com.adobe.primetime.reference.advertising](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | Contém o código para anúncios personalizados. |
| [com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | Contém o código de interface necessário para configurar os gerenciadores de recursos. |
| [com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | Contém classes auxiliares para DRM. |
| [com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | Adaptadores e adaptadores de item para informações de interface, plataforma e referência. Também inclui o código FeedAdapterFactory, ContentRenditionInfo e XMLParserHelper. |
| [com.adobe.primetime.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | Fornece classes para registro local e remoto. |
| [com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | É aqui que você pode encontrar os gerenciadores de recursos, bem como o ManagerFactory. Para recursos opcionais que você pode ativar ou desativar, há dois gerenciadores de recursos: <ul><li>Um gerenciador de recursos que é o nome do recurso, por exemplo, CCManager. Este gerenciador de recursos está desativado e fornece o comportamento desativado padrão.</li><li>Um gerenciador de recursos que tem On anexado ao nome do gerenciador de recursos, por exemplo, CCManagerOn. Este gerenciador de recursos fornece exemplos de código para o recurso ativado.</li></ul> |
| [com.adobe.primetime.reference.ui.catalog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | Contém o código da interface do usuário para o catálogo. |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | Contém o código da interface do usuário para o log. |
| [com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | Contém o código de interface do usuário do reprodutor. |
| [com.adobe.primetime.reference.ui.sesettings](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | Contém o código de interface do usuário para configurações. |
| [com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | Contém classes de utilitários gerais. |
| [com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | Contém `HTTP-specific` classes de utilitário. |
