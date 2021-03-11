---
title: Gestores de recursos
description: Os gerentes de recursos fornecem uma maneira de controlar os recursos individuais sem percorrer todo o TVSDK em busca de código para um recurso que pode ser distribuído em vários locais.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 2%

---


# Gestores de recursos {#feature-managers}

Os gerentes de recursos fornecem uma maneira de controlar os recursos individuais sem percorrer todo o TVSDK em busca de código para um recurso que pode ser distribuído em vários locais. Os gerentes de recursos condensam o código em uma classe por recurso. Os gerentes de recurso esperam por acionadores de eventos TVSDK e informam a classe que usa o gerenciador de recursos para lidar com o resultado. O gerenciador de recursos fornece as informações necessárias para a classe.

Os gerentes de recursos executam as seguintes tarefas:

* **Aciona recursos do TVSDK.**
Essas são chamadas de função para acionar um recurso TVSDK. Por exemplo, 
`PlaybackManager.play()` é chamado quando o aplicativo reprodutor precisa iniciar a reprodução do vídeo.

* **Escuta eventos TVSDK.**
O gerenciador de recursos precisa ouvir eventos TVSDK para adquirir informações do TVSDK. Por exemplo, 
`AdsManager` escuta eventos de anúncios TVSDK a serem notificados quando o ad breaks começarem.

* **Despacha eventos para o manipulador.**
Depois que os gerentes de recursos receberem e processarem os eventos do TVSDK, eles notificarão o lado do cliente para lidar com o evento. Por exemplo, depois de 
`AdsManager` recebe um evento ad break start, informa ao fragmento do reprodutor para refletir essa alteração na interface do usuário (desative a barra de depuração, mostre a sobreposição do anúncio etc.).

A implementação de referência do Primetime inclui os seguintes gerentes de recursos:

| Gerenciador de recursos | Arquivo padrão | Recurso |  |
|---|---|---|---|
| Reprodução de vídeo | PlaybackManager | Reprodução e controle de HLS, reprodução e controle de DVR, controle de buffer e tratamento de taxa de vários bits. | Obrigatório |
| Proteção de conteúdo DRM | DrmManager | Proteção de conteúdo. | Obrigatório |
| Inserção de anúncio | AdsManager | Inserção de anúncios, incluindo o Adobe Primetime ad Decisioning direct ad break e ad break personalizado. | Opcional |
| Legendas ocultas | CCManager | Legendas ocultas e legendas VTT. | Opcional |
| Áudio de ligação tardia | AAManager | Áudio de ligação tardia. | Opcional |
| QoS | QosManager | Estatísticas de QoS. | Opcional |
| Direito | EntitlementManager | Integração de direito de autenticação do Primetime. | Opcional |

A implementação de referência contém classes padrão básicas, listadas acima, e classes correspondentes com o sufixo Ativado. As classes padrão fornecem os comportamentos padrão do TVSDK, enquanto as classes com o sufixo On incluem todo o código necessário para acionar o recurso TVSDK e ouvir eventos TVSDK para esse recurso.

* Para recursos opcionais, o código padrão funciona como se o recurso estivesse desativado.
* As classes com o sufixo Ativado operam como se o recurso estivesse ativado.