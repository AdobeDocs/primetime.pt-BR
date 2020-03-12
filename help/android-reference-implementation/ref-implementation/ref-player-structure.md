---
description: Os gerentes de recursos servem como invólucros ao redor da biblioteca TVSDK.
seo-description: Os gerentes de recursos servem como invólucros ao redor da biblioteca TVSDK.
seo-title: Estrutura de execução de referência
title: Estrutura de execução de referência
uuid: ae347a97-1500-476a-9fc8-c99e6b2ab8de
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Estrutura de execução de referência {#reference-implementation-structure}

Os gerentes de recursos servem como invólucros ao redor da biblioteca TVSDK.

Em Java, as classes são estruturadas em uma hierarquia. Por exemplo, todos os códigos relacionados à interface do usuário em `com.adobe.primetime.reference.ui` e todos os gerentes de recursos estão em `com.adobe.primetime.reference.manager`.

A implementação de referência Primetime contém os seguintes pacotes:

| Embalagem | Descrição |
|--- |--- |
| [com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | Esta classe estende android.app.Application. |
| [com.adobe.primetime.reference.publicitário](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | Contém código para anúncios personalizados. |
| [com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | Contém o código de interface necessário para configurar os gerenciadores de recursos. |
| [com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | Contém classes auxiliares para DRM. |
| [com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | Os adaptadores e adaptadores de item para obter informações sobre interface, plataforma e referência. Também inclui o código FeedAdapterFactory, ContentRenditionInfo e XMLParserHelper. |
| [com.adobe.primetime.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | Fornece classes para registro local e remotamente. |
| [com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | É aqui que você pode encontrar os gerenciadores de recursos e o ManagerFactory. Para recursos opcionais que podem ser ativados ou desativados, há dois gerenciadores de recursos: <ul><li>Um gerenciador de recursos que é o nome do recurso, por exemplo, CCManager. Este gerenciador de recursos está desativado e fornece o comportamento padrão de desativação.</li><li>Um gerenciador de recursos que tem Ativado anexado ao nome do gerenciador de recursos, por exemplo, CCManagerOn. Este gerenciador de recursos fornece exemplos de código para o recurso ativado.</li></ul> |
| [com.adobe.primetime.reference.ui.catalog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | Contém o código da interface do usuário para o catálogo. |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | Contém o código de interface do usuário para o log. |
| [com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | Contém código de interface do usuário para o player. |
| [com.adobe.primetime.reference.ui.seções](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | Contém código de interface para configurações. |
| [com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | Contém classes de utilidade geral. |
| [com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | Contém classes `HTTP-specific` de utilitários. |
