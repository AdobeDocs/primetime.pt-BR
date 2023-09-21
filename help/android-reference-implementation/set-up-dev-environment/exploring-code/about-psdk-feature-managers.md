---
title: Gerenciadores de recursos
description: Os gerenciadores de recursos fornecem uma maneira de controlar recursos individuais sem atravessar todo o TVSDK em busca de código para um recurso que pode estar espalhado em vários locais.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Gerenciadores de recursos {#feature-managers}

Os gerenciadores de recursos fornecem uma maneira de controlar recursos individuais sem atravessar todo o TVSDK em busca de código para um recurso que pode estar espalhado em vários locais. Os gerenciadores de recursos condensam o código em uma classe por recurso. Os gerenciadores de recursos aguardam acionadores de eventos TVSDK e informam a classe que usa o gerenciador de recursos para lidar com o resultado. O gerenciador de recursos fornece as informações necessárias para a classe.

Os gerentes de recursos executam as seguintes tarefas:

* **Aciona recursos do TVSDK.**
Essas são chamadas de função para acionar um recurso TVSDK. Por exemplo, `PlaybackManager.play()` é chamado quando o aplicativo de reprodução precisa iniciar a reprodução de vídeo.

* **Escuta eventos TVSDK.**
O gerenciador de recursos precisa acompanhar eventos TVSDK para adquirir informações do TVSDK. Por exemplo, `AdsManager` escuta eventos de anúncios TVSDK para serem notificados quando ad breaks começam.

* **Despacha eventos para o manipulador.**
Depois que os gerentes de recursos recebem e processam os eventos do TVSDK, eles notificam o lado do cliente para lidar com o evento. Por exemplo, depois de `AdsManager` recebe um evento de início de ad break, ele informa ao fragmento do player para refletir essa alteração na interface do usuário (desative a barra de limpeza, mostre a sobreposição do anúncio etc.).

A implementação de referência do Primetime inclui os seguintes gerenciadores de recursos:

| Gerenciador de recursos | Arquivo padrão | Recurso |  |
|---|---|---|---|
| Reprodução de vídeo | PlaybackManager | Reprodução e controle HLS, reprodução e controle DVR, controle de buffer e manipulação de taxa de vários bits. | Obrigatório |
| Proteção de conteúdo DRM | DrmManager | Proteção de conteúdo. | Obrigatório |
| Inserção de anúncio | AdsManager | Inserção de anúncio, incluindo ad break direto do Adobe Primetime Ad Decisioning e ad break personalizado. | Opcional |
| Legendas ocultas | CCManager | Legendas ocultas e legendas em VTT. | Opcional |
| Áudio de associação tardia | AAManager | Áudio de associação tardia. | Opcional |
| QoS | QosManager | Estatísticas de QoS. | Opcional |
| Direito | EntitlementManager | Integração de direitos de autenticação do Primetime. | Opcional |

A implementação de referência contém classes padrão básicas, listadas acima, e classes correspondentes com o sufixo On. As classes padrão fornecem os comportamentos TVSDK padrão, enquanto as classes com o sufixo On incluem todo o código necessário para acionar o recurso TVSDK e ouvir eventos TVSDK para esse recurso.

* Para recursos opcionais, o código padrão funciona como se o recurso estivesse desativado.
* As classes com o sufixo On operam como se o recurso estivesse ativado.
