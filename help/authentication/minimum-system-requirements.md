---
title: Requisitos mínimos do sistema
description: Requisitos mínimos do sistema
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Requisitos mínimos do sistema {#minimum-system-requirements}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.


## Visão geral {#overview}

Este documento apresenta os requisitos atuais de software e hardware para implementar integrações de Autenticação Adobe Primetime em plataformas compatíveis. Todos os navegadores Web/móveis e sistemas operacionais compatíveis listados abaixo se beneficiarão do suporte completo da equipe de Autenticação da Adobe Primetime, vinculada aos SLAs acordados.

Enquanto equipe de Autenticação da Adobe Primetime, incentivamos o uso das versões estáveis mais recentes dos navegadores e sistemas operacionais; reconhecemos também a existência de plataformas e navegadores incompatíveis/antigos que estão em uso no momento. Esses dispositivos desatualizados ainda podem funcionar sem problemas, no entanto, estarão mais propensos a erros.

A abordagem inicial para atenuar qualquer problema que apareça nessas plataformas desatualizadas deve ser a atualização para as versões mais recentes; pode ser a versão do SO, do navegador ou a versão do aplicativo instalado.

Qualquer problema que apareça nessas plataformas será resolvido da melhor maneira pela equipe de autenticação da Adobe Primetime. 

A Adobe Primetime incentiva nossos parceiros a considerar a atualização para as versões mais recentes para se beneficiarem do suporte completo da Adobe, além de possíveis problemas de desempenho, eficiência e melhorias de segurança. 


## Requisitos do navegador e sistema operacional {#browser-OS-system-requirements}


| Navegador Web/móvel (†) | Versões suportadas |
|---|---|
| Google Chrome | **70º** ou posterior |
| Mozilla Firefox | **57º** ou posterior |
| Apple Safari | **14.** ou posterior |
| Microsoft Edge | **100** ou posterior |

(†) O Adobe recomenda não usar o modo privado ou incógnito.

| Sistema operacional | Versões suportadas |
|---|---|
| *Android* | **7,0** (Nougat) ou posterior |
| *iOS* | **14.** ou posterior |
| *iPadOS* | **14.** ou posterior |
| *tvOS* | **14.** ou posterior |
| *Fire OS* | **5 (Android 5.1)** ou posterior |
| *Mac OS* | **10,13** ou posterior |
| *Microsoft Windows* | **10º** ou posterior |




>[!NOTE]
>
>Cookies de terceiros - Os fluxos de direito da Autenticação do Adobe Primetime podem falhar quando cookies de terceiros estão desativados.  Esse problema só é exibido quando as configurações do navegador são modificadas. Para todos os navegadores compatíveis, a Autenticação do Primetime deve ser funcional com as configurações padrão.\
 

## Requisitos do dispositivo para implementações sem cliente (REST) {#general_clientless_reqs}

 
Qualquer dispositivo que consumirá serviços de autenticação da Adobe Primetime por meio de implementações sem cliente **deve ser capaz de**:

* Forneça uma ID de dispositivo com hash exclusiva. Se o dispositivo não fornecer uma ID de dispositivo com hash exclusiva, ele deverá ser capaz de manter uma ID exclusiva fornecida pela Autenticação Adobe Primetime. O dispositivo deve ser capaz de manter a ID exclusiva permanentemente em seu armazenamento local e fornecer a ID exclusiva como a ID do dispositivo ao fazer chamadas para as APIs de autenticação da Adobe Primetime.
* Gerar assinaturas digitais usando o algoritmo HMAC-SHA1
* Definir cabeçalhos HTTP arbitrários
* Consumir serviços Web RESTful
* Analisar formatos de dados XML e JSON
* Enviar tráfego usando HTTPS
* Gerenciar códigos de erro HTTP
