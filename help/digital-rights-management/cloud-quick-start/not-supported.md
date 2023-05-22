---
title: O que NÃO é compatível com o Primetime Cloud DRM
description: O que NÃO é compatível com o Primetime Cloud DRM
copied-description: true
exl-id: 11dac4e3-6f08-43d0-a0db-3d3849baa8a9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# O que NÃO é compatível com o Primetime Cloud DRM{#what-is-not-supported-by-primetime-cloud-drm}

O Primetime Cloud DRM é compatível com quase todos os recursos atualmente disponíveis com o Primetime DRM. No entanto, devido a alguns dos recursos do DRM que exigem comunicação com o subsistema de regras de negócios de back-end de um cliente, alguns recursos não estão disponíveis com o DRM do Primetime Cloud.

Os recursos atualmente não compatíveis com o Primetime Cloud DRM são:

* Conteúdo empacotado com um CEK externo (em que o servidor de licenças solicita o CEK do conteúdo de um sistema de gerenciamento de chaves externas)
* Domínios de dispositivo
* Encadeamento de licenças avançado
* Devolução/Revogação de Licença
* PHLS/PHDS. São esquemas de proteção que não usam um License Server
* Autenticação de usuário/senha
