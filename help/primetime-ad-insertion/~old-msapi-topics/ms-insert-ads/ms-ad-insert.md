---
description: Todas as solicitações para inserção de anúncios usam a mesma estrutura de URL e os mesmos parâmetros básicos de consulta. Parâmetros de consulta adicionais permitem que o servidor de manifesto funcione com uma variedade de clientes e situações.
title: Solicitações para inserção de anúncio
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Solicitações para inserção de anúncio {#requests-for-ad-insertion}

Todas as solicitações para inserção de anúncios usam a mesma estrutura de URL e os mesmos parâmetros básicos de consulta. Parâmetros de consulta adicionais permitem que o servidor de manifesto funcione com uma variedade de clientes e situações.

| Parâmetro | Descrição |
|--- |--- |
| u | A ID do ativo é um hash MD5 do ad_request_id dos metadados de decisão de anúncios do Adobe Primetime. Fornecido pelo Gerente técnico de conta do Adobe. |
| z | A ID da zona do ativo que precisa ser fornecido ao Auditude. Fornecido pelo Gerente técnico de conta do Adobe. |
| `__sid__` | Uma ID exclusiva que o servidor de manifesto usará para gerar a ID da sessão. |

>[!NOTE]
>
>A variável `__sid__` é delimitado por caracteres com sublinhado duplo.

O servidor de manifesto mantém sessões para clientes individuais ou grupos de clientes para garantir que as sequências de interações da API para clientes diferentes permaneçam separadas. A variável `__sid__` que o cliente envia no URL de inicialização para o servidor manifest deve ser exclusivo em seu ambiente. O servidor de manifesto o usa esse ID para criar uma ID globalmente exclusiva, que retorna ao cliente.

Os parâmetros de consulta restantes pertencem a clientes e situações diferentes.