---
seo-title: Gerenciadores de recursos
title: Gerenciadores de recursos
uuid: 3d78544e-4819-4122-bfd3-01522a067aa9
description: Os gerentes de recursos fornecem uma maneira de controlar os recursos individuais sem percorrer todo o TVSDK em busca do código de um recurso que pode ser espalhado em vários locais.
seo-description: Os gerentes de recursos fornecem uma maneira de controlar os recursos individuais sem percorrer todo o TVSDK em busca do código de um recurso que pode ser espalhado em vários locais.
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 2%

---


# Gerenciadores de recursos {#feature-managers}

Os gerentes de recursos fornecem uma maneira de controlar os recursos individuais sem percorrer todo o TVSDK em busca do código de um recurso que pode ser espalhado em vários locais. Os gerentes de recurso condensam o código em uma classe por recurso. Os gerentes de recursos esperam por acionadores de eventos TVSDK e informam a classe que usa o gerenciador de recursos para lidar com o resultado. O gerenciador de recursos fornece as informações necessárias para a classe.

Os gerentes de recursos executam as seguintes tarefas:

* **Aciona os recursos do TVSDK.**
São chamadas de função para acionar um recurso TVSDK. Por exemplo, 
`PlaybackManager.play()` é chamado quando o aplicativo do player precisa start a reprodução do vídeo.

* **Escuta eventos TVSDK.**
O gerenciador de recursos precisa ouvir eventos TVSDK para adquirir informações do TVSDK. Por exemplo, 
`AdsManager` escuta os eventos de anúncios TVSDK a serem notificados quando o anúncio interromper o start.

* **Despacha eventos para o manipulador.**
Depois que os gerentes de recursos receberem e processarem os eventos do TVSDK, eles notificarão o lado do cliente para lidar com o evento. Por exemplo, após 
`AdsManager` recebe um evento de start de quebra de anúncio, informa ao fragmento do player que deve refletir essa alteração na interface do usuário (desative a barra de depuração, mostre a sobreposição do anúncio etc.).

A implementação de referência Primetime inclui os seguintes gerenciadores de recursos:

| Gerenciador de recursos | Arquivo padrão | Recurso |  |
|---|---|---|---|
| Reprodução de vídeo | PlaybackManager | Reprodução e controle de HLS, reprodução e controle de DVR, controle de buffer e gerenciamento de taxa de vários bits. | Obrigatório |
| Proteção de conteúdo DRM | DrmManager | Proteção de conteúdo. | Obrigatório |
| Inserção de anúncio | AdsManager | Inserção de anúncios, incluindo o intervalo direto de anúncios de decisão do Adobe Primetime e o intervalo de anúncios personalizado. | Opcional |
| Legendas ocultas | CCManager | Legendas ocultas e legendas VTT. | Opcional |
| Áudio de ligação tardia | AAManager | Áudio de ligação tardia. | Opcional |
| QoS | QosManager | Estatísticas de QoS. | Opcional |
| Direito | EntitlementManager | Integração de direito de autenticação Primetime. | Opcional |

A implementação de referência contém classes padrão básicas, listadas acima, e classes correspondentes com o sufixo de Ativado. As classes padrão fornecem os comportamentos padrão de TVSDK, enquanto as classes com o sufixo On incluem todo o código necessário para acionar o recurso TVSDK e ouvir eventos TVSDK para esse recurso.

* Para recursos opcionais, o código padrão funciona como se o recurso estivesse desativado.
* As classes com o sufixo On funcionam como se o recurso estivesse ativado.