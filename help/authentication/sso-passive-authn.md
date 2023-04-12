---
title: SSO via autenticação passiva
description: SSO via autenticação passiva
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# SSO via autenticação passiva

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.


## Introdução

O escopo deste documento é descrever a implementação do fluxo de autenticação passiva e como isso funciona com nossa abordagem padrão de logon único.

## Usecases

A autenticação da Adobe Primetime habilita o Logon único (SSO) entre aplicativos/sites. Depois que um usuário faz logon com suas credenciais do MVPD, a autenticação da Adobe Primetime gera um token seguro que representa a sessão de autenticação do MVPD e vincula esse token ao dispositivo do usuário usando uma ID do dispositivo. A autenticação da Adobe Primetime armazena o token/ID do dispositivo em um servidor ou no dispositivo.

Desde que o token ainda seja válido, os usuários aparecerão diretamente como autenticados. Isso permite que os usuários insiram suas credenciais com menos frequência, mantendo as transações seguras.



O caso de uso comercial detalhado aqui é um requisito muito específico: que o usuário DEVE ser autenticado pelo menos uma vez para cada site visitado. Isso permite que o MVPD aplique regras de negócios associadas à sessão authN que podem variar de acordo com a rede. Ela está em conflito com a promessa de TVE atual de que um usuário precisa fazer logon apenas uma vez e será autenticado em todos os sites que fazem parte do ecossistema de autenticação da Adobe Primetime.



Para manter a regra de negócios, mas também manter uma boa experiência do usuário, o MVPD NÃO exige que o usuário forneça manualmente as informações de credenciais. Podemos nos beneficiar do cookie de sessão definido anteriormente e tentar fazer uma reautenticação automática usando o fluxo passivo; do ponto de vista do usuário, ele aparecerá como conectado automaticamente.



Para resolvê-las, implementamos 2 características distintas: autenticação por rede e suporte à autenticação passiva. Os MVPDs oferecerão suporte ao SAML passive authN, onde estão simplesmente reautenticando um usuário se uma sessão authN existir no IdP, independentemente do site em que a sessão foi criada.



## Autenticação por rede

Esse recurso garante que o MVPD receba uma solicitação de autenticação uma vez para cada site visitado. Essa funcionalidade significa que um token de autenticação da Adobe Primetime será vinculado à ID do solicitante, sendo válido apenas para a rede que o solicitou. Como resultado, uma vez que o usuário se autentica no site &quot;A&quot; e depois visita o site &quot;B&quot;, será necessário autenticar.



Observe que devido ao fato de que no IdP do MVPD o usuário já está autenticado, ele não precisará fornecer informações de logon, mas, em vez disso, o navegador será simplesmente redirecionado do site &quot;B&quot; para o MVPD IdP e, em seguida, de volta. O mesmo usuário ainda será autenticado no site &quot;A&quot; se ele retornar.



O fluxo a seguir descreve o recurso básico Autenticação por rede:





## Autenticação passiva

O objetivo é fazer com que o processo de reautenticação ocorra em segundo plano sem a necessidade de um redirecionamento completo do navegador e o seletor seja exibido. Como resultado, um usuário que muda do site A para o site B será autenticado automaticamente.



De uma perspectiva UX, não haverá diferença entre este fluxo e um fluxo executado com um MVPD normal. O que o usuário vê é que, depois de inserir as credenciais como resultado da visita ao site A, elas serão automaticamente autenticadas no site B.



Para tornar esse fluxo viável, o MVPD precisará suportar autenticação passiva para que o iframe oculto não fique &quot;preso&quot; na página de logon, caso o MVPD não tenha mais uma sessão. Isso é feito por meio do atributo padrão &quot;isPassive&quot;.



O diagrama a seguir descreve o fluxo melhorado e a autenticação passiva &quot;nos bastidores&quot;:





Exemplo de solicitação SAML Aqui está uma amostra de solicitação SAML para o fluxo authN passivo:


```xml
<saml2p:AuthnRequest xmlns:saml2p="urn:oasis:names:tc:SAML:2.0:protocol"
                     AssertionConsumerServiceURL="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"
                     Destination="https://mvpd_idp_url"
                     ForceAuthn="false"
                     ID="_15056686-399c-4528-b21a-4a9542cfc8ec"
                     IsPassive="true"
                     IssueInstant="2014-11-03T14:18:12.394Z"
                     ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
                     Version="2.0"
                     >
    <saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">https://saml.sp.auth.adobe.com </saml2:Issuer>
    <saml2p:Extensions>
        <thrpty:RespondTo xmlns:thrpty="urn:oasis:names:tc:SAML:protocol:ext:third-party">https://saml.sp.auth.adobe.com</thrpty:RespondTo>
    </saml2p:Extensions>
    <saml2p:NameIDPolicy AllowCreate="true"
                         Format="urn:oasis:names:tc:SAML:2.0:nameid-format:transient"
                         SPNameQualifier="https://saml.sp.auth.adobe.com"
                         />
</saml2p:AuthnRequest>
```

Os MVPDs de regras comerciais têm restrições específicas de domínio de escopo de SSO. Por exemplo, apenas alguns domínios poderiam ser permitidos por alguns MVPDs (SSO para a mesma empresa de mídia, mas não entre empresas).
Alguns MVPDs podem exigir a aplicação de regras de autenticação diferentes. Por exemplo, os MVPDs podem ter TTLs de autenticação diferentes por redes diferentes. Além disso, os MVPDs podem habilitar a autenticação por conta própria para algumas redes, mas não para outras (os casos de uso do controle dos pais são fortemente representados aqui).


Esses requisitos de negócios devem ter em mente que o principal caso de uso é que o usuário não deve ser obrigado a entrar novamente depois de fazer logon com o MVPD.

Isso pode ser feito usando a autenticação por rede com o sinalizador authN passivo.



Limitações conhecidas do iOS - devido à natureza do armazenamento local do iOS, os fluxos de SSO não funcionam no iOS para aplicativos desenvolvidos por diferentes fornecedores. Para obter mais informações sobre SSO no iOS 8 e superior, consulte esta Nota Técnica.


<!--
>[!RELATEDINFORMATION]
>* Single Sign-On on iOS
>* SSO on iOS when using the Primetime authentication Access Enabler
-->