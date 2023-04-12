---
title: Suporte para logon único
description: Suporte para logon único
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---


# Suporte para logon único

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#overview-sso-support}

Este documento descreve os tipos de Logon único suportados e fornecidos pela autenticação da Adobe Primetime em plataformas diferentes. O escopo deste documento é esclarecer o que é suportado e o que não é, qual é a cobertura do MVPD para cada método SSO e o que é exigido aos programadores para poderem se beneficiar do SSO em cada plataforma.

Depois que um usuário faz logon com suas credenciais do MVPD, a autenticação da Adobe Primetime gera um token seguro que representa a sessão de Autenticação do MVPD e vincula esse token ao dispositivo do usuário usando uma ID do dispositivo. A autenticação da Adobe Primetime armazena o token/ID do dispositivo em um servidor ou no dispositivo. Isso permite que os usuários insiram suas credenciais com menos frequência, mantendo as transações seguras.

>[!NOTE]
>
>Os workflows SSO são parte do pacote Premium Workflow . Entre em contato com seu representante de vendas do Primetime, caso esteja interessado em usar essa funcionalidade.

## Status atual para SSO em várias plataformas {#current-sso-status-platforms}

| Plataforma/dispositivo | Suporte SSO | Tipo de SSO | Cobertura de MVPD | Notas |
|:-------------------:|:-----------:|:---------------------------------------:|-----------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| Web (JavaScript) | Sim | Token de autenticação compartilhado (Adobe SSO) | Todos | Nenhum SSO entre navegadores Siga as instruções do Guia de Integração do Programador para JavaScript. Após seguir as instruções, o SSO é ativado por padrão.  Habilitar a autenticação por solicitante interrompe o SSO |
| iOS | Sim | Platform SSO - troca de token | Dependendo do suporte do Apple - a lista está aqui | A partir do iOS 10, a Apple &amp; Adobe introduziu a funcionalidade SSO para programadores participantes e MVPDs. Ao usar o SDK mais recente do Adobe ou a API REST sem cliente Adobe e implementar a funcionalidade Apple SSO, você pode se beneficiar do SSO em dispositivos iOS. Mais detalhes sobre a implementação do SDK aqui e mais detalhes sobre a implementação sem cliente aqui. Notas adicionais: - Se você não quiser usar o Apple SSO, ainda poderá ter um SSO limitado entre aplicativos do mesmo fornecedor (mesma ID de pacote) que podem compartilhar armazenamento e uma ID (IDFV); portanto, o SSO é limitado apenas aos aplicativos do mesmo fornecedor. |
| Android | Sim | Token de autenticação compartilhado (Adobe SSO) | Todos | Se o usuário não aceitar a solicitação de permissão WRITE_EXTERNAL_STORAGE, a biblioteca usará um armazenamento em sandbox local. A implicação nesse caso é que não haverá SSO entre aplicativos diferentes ao usar o armazenamento local. |
| tvOS - nova TV Apple | Sim | Platform SSO - troca de token | Dependendo do suporte do Apple - a lista está aqui | A partir do tvOS 10, a Apple &amp; Adobe introduziu a funcionalidade SSO para programadores e MVPDs participantes. Ao usar o SDK do Adobe tvOS ou a API REST sem cliente e implementar a funcionalidade Apple SSO, você pode se beneficiar do SSO em dispositivos tvOS. Mais detalhes sobre o tvOS SDK: aqui e aqui e mais detalhes sobre a implementação sem cliente aqui. |
| Roku | Sim | Token de autenticação compartilhado (Adobe SSO) | Lista completa de cobertura significativa a fornecer em breve. | O Roku SSO funciona imediatamente com a API sem cliente para todos os clientes que respeitam as diretrizes do Roku, sem necessidade de implementação especial. O SSO é baseado nas informações de identificação do dispositivo que o Roku está enviando com segurança para o Adobe. |
| Amazon FireTV | Sim | Token de autenticação compartilhado (Adobe SSO) | Lista completa de cobertura significativa a fornecer em breve. | O SDK do FireTV oferece suporte ao Logon único com base nos recursos do Android. O SSO nessa plataforma é possível somente entre aplicativos que estão usando o SDK do Adobe FireTV por enquanto. Mais informações sobre o novo SDK do FireTV aqui. Os aplicativos FireTV implementados sobre a API sem cliente poderão se beneficiar do SSO por EOY 2018. |
| Xbox 360 | Não |  |  | Não há ID de dispositivo que possamos utilizar. Há uma ID do aplicativo, portanto, os usuários não precisam autenticar sempre. |
| Xbox One | Não |  |  | Não há ID de dispositivo que possamos utilizar. Há uma ID do aplicativo, portanto, os usuários não precisam autenticar sempre. |
| Windows 8/10 | Não |  |  | Não há ID de dispositivo que possamos utilizar. Há uma ID do aplicativo, portanto, os usuários não precisam autenticar sempre. |
| TVs da Samsung | Não |  |  | Não há ID de dispositivo que possamos utilizar. Há uma ID do aplicativo, portanto, os usuários não precisam autenticar sempre. |

### Notas sobre o Xbox 360 e o Xbox One {#notes-xbox-360}

* **Xbox 360**- O Xbox 360 depende do Live Service para fornecer o token que incorpora o deviceID. As camadas do Serviço em tempo real no valor do appID para deviceID, tornando-o escopo somente para o aplicativo. Para o Xbox 360, a Microsoft forneceu o Adobe a biblioteca Java para ajudar na análise do token.

* **Xbox One**- Será emitido um token da Web JSON criptografado com o certificado/chave do editor e assinado pela Microsoft. O Adobe extrai a deviceID de um parâmetro chamado DPI (Device Pairexpressão do dispositivo), diferente do parâmetro Xbox 360 PDID (Partner Device ID). O PDID também existe no Xbox One, mas deve ser substituído por esse novo parâmetro &quot;Device Pairexpressão ID&quot; (DPI).


### Desabilitação do SSO {#disable-sso}

Em determinadas situações, alguns aplicativos ou sites desejam desativar o SSO para atender a casos de negócios avançados.

* **Para JS e SDKs nativos** - A equipe de suporte à autenticação do Primetime pode desativar o SSO para um par de ID do solicitante / MVPD. Nenhum trabalho é necessário em sites ou em aplicativos nativos.  Quando o SSO for desativado pela equipe de suporte de autenticação do Primetime, as autenticações executadas usando o par RequestorId / MVPD especificado não serão compartilhadas com sites ou aplicativos usando IDs de Solicitante diferentes. Além disso, as autenticações existentes com IDs de Solicitante diferentes não serão válidas para a combinação ID de Solicitante / MVPD na qual o SSO foi desativado. Tecnicamente, a desativação do SSO é realizada vinculando o token AuthN à combinação específica da ID do solicitante / MVPD.
* **Para API sem cliente** - Você pode desativar o SSO no fluxo de autenticação sem cliente especificando um parâmetro appId não vazio nas chamadas REST. Você pode usar qualquer string como o valor, desde que essa string seja exclusiva para a ID do solicitante. Observe que para a API sem cliente, o programador/implementador deve alterar o site ou o aplicativo para adicionar esse parâmetro específico do solicitante.

>[!IMPORTANT]
>
>OBSERVAÇÃO IMPORTANTE PARA SSO DE API SEM CLIENTES: Alguns MVPDs exigem que cada rede (ID do solicitante) execute seu próprio fluxo de autenticação. Para os fluxos com base no SDK (iOS etc.), isso é manipulado automaticamente pelo SDK. No entanto, para as APIs sem cliente, isso precisa ser tratado pelo programador. Aconselhamos os programadores a não ativar os fluxos de SSO para APIs sem cliente neste ponto e, em vez disso, usar uma combinação de ID de dispositivo + ID de aplicativo para a ID do dispositivo. O Adobe também trabalhará para melhorar os fluxos de API sem cliente para que o SSO adequado possa ser estabelecido.

### Logout {#logout-sso-support}

Os programadores precisam estar cientes de que a ação &quot;Logout&quot; no contexto de Logon único, quando executada em um aplicativo/em um site, excluirá todos os tokens no dispositivo e o usuário será desconectado dos aplicativos/sites.

Se as condições do SSO forem atendidas (se o SSO estiver ou não ativado ou desativado), o Logout será executado e ele excluirá todas as informações de autenticação e autorização.
