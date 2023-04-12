---
title: Recurso de comprovação, como ativar, solucionar problemas ou determinar o problema
description: Recurso de comprovação, como ativar, solucionar problemas ou determinar o problema
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---


# Recurso de comprovação: Como ativar, solucionar problemas ou determinar o problema {#preflight-feature}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

Houve uma alteração na maneira como a autenticação da Adobe Primetime calcula preAuthorizeResources. A API de pré-autorização tem uma nova implementação. Essa implementação substitui a solução antiga, que consiste em fazer várias chamadas de autorização somente.
A interface externa da API de Pré-autorização permanece inalterada, nenhuma atualização é necessária no aplicativo do Programador.

Há três maneiras de calcular os recursos de Comprovação:

* **Bifurcar e unir método ao MVPD**: isso envolve Adobe fazendo várias chamadas de autorização para o MVPD (o cliente ainda terá que fazer uma chamada de pré-voo).
* **Linha de canal**: o MVPD expõe a linha de canal para o usuário conectado na resposta de autenticação SAML e o Adobe retorna os recursos autorizados com base nisso. A resposta authN SAML no marcador SAML deve expor essa lista.
* **Autorização de vários canais**: a autenticação cliente e Adobe faz uma única chamada para o MVPD para um conjunto de recursos.

Independentemente do MVPD, o aplicativo Client fará uma única chamada para o endpoint Preflight (API checkPreauthorizedResources), transmitindo um conjunto de resourceIDs. Com base em uma das maneiras acima suportadas pelo MVPD, o Adobe retornará os resourceIDs pré-autorizados.

Se a Comprovação for baseada no método de bifurcação e associação, o back-end da Autenticação do Adobe Primetime verificará um valor definido para as &quot;chamadas de pré-autorização máximas&quot; em sua configuração. Isso é configurado pelo Adobe.

O valor padrão para a configuração &#39;max preauthorization calls&#39; é &#39;5&#39;, o que significa que no máximo apenas 5 recursos podem ser enviados em Preflight para a bifurcação e unir MVPDs. Passar mais de 5 recursos resultará em uma exceção e uma lista nula será retornada. Esse é o comportamento esperado. Podemos configurá-lo para qualquer valor se o MVPD não oferecer suporte à linhagem de canais ou à autorização de vários canais, mas somente após consultá-los como várias chamadas de bifurcação e autorização de associação aumentará seu tempo de carregamento.

Consequentemente, essas são coisas que devem ser procuradas ao ativar/solucionar problemas de Comprovação para um MVPD:

* O método que o MVPD suporta (bifurcação e associação, line-up de canal ou multicanal).
* Se houver suporte para apenas bifurcação e associação, será necessário perguntar ao Programador quantas IDs de recurso ele estará enviando na chamada de Comprovação.
* O MVPD precisa ser consultado e precisa saber o impacto de fazer um número &quot;n&quot; de bifurcações e chamadas de autorização de associação. Depois, o valor deve ser configurado na configuração se for maior que 5.

**Limitação**

Observe que não obtemos nenhum resourceID da chamada de Comprovação para alguns MVPDs como AT&amp;T e TWC se qualquer um dos resourceIDs for uma ID falsa ou uma ID não reconhecida na lista de resourceIDs que eles enviam na chamada de comprovação, mesmo que tenhamos recursos válidos e autorizados também nessa lista.

