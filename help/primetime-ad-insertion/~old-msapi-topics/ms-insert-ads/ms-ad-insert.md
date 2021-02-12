---
description: Todas as solicitações de inserção de publicidade usam a mesma estrutura de URL e os mesmos parâmetros básicos de query. Parâmetros de query adicionais permitem que o servidor manifest funcione com uma variedade de clientes e situações.
seo-description: Todas as solicitações de inserção de publicidade usam a mesma estrutura de URL e os mesmos parâmetros básicos de query. Parâmetros de query adicionais permitem que o servidor manifest funcione com uma variedade de clientes e situações.
seo-title: Solicitações de inserção de anúncio
title: Solicitações de inserção de anúncio
uuid: e42b3228-bff7-4202-86ed-7f631f3016ae
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Solicitações de inserção de anúncio {#requests-for-ad-insertion}

Todas as solicitações de inserção de publicidade usam a mesma estrutura de URL e os mesmos parâmetros básicos de query. Parâmetros de query adicionais permitem que o servidor manifest funcione com uma variedade de clientes e situações.

| Parâmetro | Descrição |
|--- |--- |
| u | A ID do ativo é um hash MD5 do ad_request_id dos metadados de decisão do anúncio da Adobe Primetime. Fornecido pelo Gerente técnico de contas do Adobe. |
| z | A ID de zona do ativo que precisa ser fornecido ao Auditude. Fornecido pelo Gerente técnico de contas do Adobe. |
| `__sid__` | Uma ID exclusiva que o servidor manifest usará para gerar a ID da sessão. |

>[!NOTE]
>
>O parâmetro `__sid__` é rodeado por caracteres sublinhados de duplo.

O servidor manifest mantém sessões para clientes individuais ou grupos de clientes para garantir que as sequências de interações de API para clientes diferentes permaneçam separadas. O `__sid__` que o cliente envia no URL de inicialização para o servidor de manifesto deve ser exclusivo dentro de seu ambiente. O servidor manifest o usa para construir uma ID exclusiva globalmente, que retorna ao cliente.

Os parâmetros de query restantes pertencem a diferentes clientes e situações.