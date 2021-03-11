---
description: Todas as solicitações de inserção de anúncio usam a mesma estrutura de URL e os mesmos parâmetros de consulta básicos. Parâmetros de consulta adicionais permitem que o servidor manifest funcione com uma variedade de clientes e situações.
title: Solicitações de inserção de anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Solicitações de inserção de anúncio {#requests-for-ad-insertion}

Todas as solicitações de inserção de anúncio usam a mesma estrutura de URL e os mesmos parâmetros de consulta básicos. Parâmetros de consulta adicionais permitem que o servidor manifest funcione com uma variedade de clientes e situações.

| Parâmetro | Descrição |
|--- |--- |
| u | A ID do ativo é um hash MD5 do ad_request_id dos metadados de decisão do anúncio do Adobe Primetime. Fornecido pelo seu Gerente de conta técnico do Adobe. |
| z | O ID de zona do ativo que precisa ser fornecido ao Auditude. Fornecido pelo seu Gerente de conta técnico do Adobe. |
| `__sid__` | Uma id exclusiva que o servidor de manifesto usará para gerar a id da sessão. |

>[!NOTE]
>
>O parâmetro `__sid__` é rodeado por caracteres sublinhados duplos.

O servidor manifest mantém sessões para clientes individuais ou grupos de clientes para garantir que as sequências de interações da API para clientes diferentes permaneçam separadas. O `__sid__` que o cliente envia no URL de inicialização para o servidor de manifesto deve ser exclusivo em seu ambiente. O servidor de manifesto o usa para criar uma ID exclusiva globalmente, que retorna ao cliente.

Os parâmetros de consulta restantes pertencem a clientes e situações diferentes.