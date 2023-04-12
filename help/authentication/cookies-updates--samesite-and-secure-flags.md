---
title: Atualizações de cookies - Sinalizadores SameSite e Secure
description: Atualizações de cookies - Sinalizadores SameSite e Secure
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---



# Atualizações de cookies - Sinalizadores SameSite e Secure {#cookies-updates---samesite-and-secure-flags}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>


## Atualizações {#Updates}

Esta seção destaca as alterações introduzidas pelo navegador Chrome e pela Autenticação Adobe Primetime para lidar com cookies de terceiros.

 

### Atualizações do Chrome 80 {#Chrome}

A partir do Chrome versão 80 (exceto a versão 82), os cookies que não especificam um *SameSite* será tratado como se fosse *SameSite=Lax*. Portanto, os cookies que precisam ser entregues em um contexto entre sites devem especificar explicitamente a variável *SameSite=None* e também devem ser marcadas com a variável *Seguro* atributo e entrega *HTTPS*. Mais detalhes sobre essas atualizações podem ser lidos na página oficial do chromium: <https://www.chromium.org/updates/same-site> e também de <https://web.dev/samesite-cookies-explained/>.


### Atualizações de autenticação do Adobe Primetime {#Pass-Updates}

No momento, o serviço de Autenticação da Adobe Primetime depende de alguns cookies considerados de terceiros do ponto de vista do navegador, incluindo o Chrome, para funcionar em combinação com algumas plataformas e versões dos SDKs de Autenticação da Adobe Primetime. Portanto, para estar em conformidade com as alterações futuras e continuar a fornecer esses cookies em um contexto entre sites desses SDKs mais antigos, o serviço de Autenticação da Adobe Primetime implementa as alterações necessárias no *adobe-pass-2.55.1* versão.

Essas alterações do *adobe-pass-2.55.1* a versão envolve adicionar a *Seguro* e *SameSite=None* atributos para todos os seus cookies passados para todos os SDKs de autenticação da Adobe Primetime ao usar navegadores Chrome começando com a versão 80 e superior (exceto a versão 82).

A próxima seção apresenta alguns possíveis problemas para uma lista de plataformas e versões dos SDKs de autenticação da Adobe Primetime caso um usuário esteja usando o navegador Chrome 80 e superior (exceto a versão 82).

## Solução de problemas {#Troubleshooting}

Ao navegar por esta seção, lembre-se de que todos os cookies do serviço de autenticação da Adobe Primetime devem ter *Seguro* conjunto de atributos em *adobe-pass-2.55.1* para todos os navegadores, enquanto a *SameSite=None* deve ser definido somente para navegadores Chrome versão 80 e superior (exceto a versão 82).


### Solução de problemas gerais {#General}

1. Importante observar que alguns agentes do usuário são incompatíveis com o *SameSite=None* atributo.

   - Versões do Chrome do Chrome 51 para o Chrome 66 (inclusive em ambas as extremidades). Essas versões do Chrome rejeitarão um cookie com *SameSite=None*. Isso também afeta versões mais antigas de navegadores derivados do Chromium, assim como Android WebView. Esse comportamento estava correto de acordo com a versão da especificação do cookie no momento, mas com a adição do novo valor &quot;Nenhum&quot; à especificação, esse comportamento foi atualizado no Chrome 67 e mais recente. (Antes do Chrome 51, o atributo SameSite era totalmente ignorado e todos os cookies eram tratados como se fossem *SameSite=None*.)
   - Versões do navegador UC no Android anteriores à versão 12.13.2. As versões anteriores rejeitarão um cookie com *SameSite=None*. Esse comportamento estava correto de acordo com a versão da especificação do cookie no momento, mas com a adição do novo valor &quot;Nenhum&quot; à especificação, esse comportamento foi atualizado em versões mais recentes do Navegador de UC.
   - Versões do Safari e navegadores incorporados no MacOS 10.14 e todos os navegadores no iOS 12. Essas versões tratarão erroneamente os cookies marcados com *SameSite=None* como se fossem marcadas *SameSite=Strict*. Esse erro foi corrigido em versões mais recentes do iOS e do MacOS.


1. É importante observar que os cookies que têm a variável *Seguro* deve ser enviado *HTTPS*, caso contrário, o cookie não alcançará o serviço de Autenticação da Adobe Primetime.

   - SDK do JavaScript do AccessEnabler:
      - Obrigatória de que a comunicação com *sp.auth.adobe.com* uses *HTTPS* para versões *2,35* e *3.5.0*, antes de introduzir o Registro dinâmico de clientes.
   - SDK do AccessEnabler iOS/tvOS:
      - Obrigatória de que a comunicação com *sp.auth.adobe.com* uses *HTTPS* para versões anteriores a *3.0.0*, antes de introduzir o Registro dinâmico de clientes.
   - SDK do Android do AccessEnabler:
      - Obrigatória de que a comunicação com *sp.auth.adobe.com* uses *HTTPS* para versões anteriores a *3.0.0*, antes de introduzir o Registro dinâmico de clientes.
   - SDK do AccessEnabler FireOS:
      - Obrigatória de que a comunicação com *sp.auth.adobe.com* uses *HTTPS* para versão *2.0.4*.

</br>

### Solução de problemas do AccessEnabler JavaScript SDK versão 2.35 {#235-Troubleshooting}

O fluxo de autenticação do usuário pode ser afetado no Chrome 80 e superior (exceto a versão 82). Para garantir que o usuário não tenha problemas para autenticar devido às atualizações acima, é possível:

- Verifique se a variável *JSESSIONID* O cookie é definido no navegador e tem a variável *SameSite=None* e *Seguro* conjunto de atributos. 
- Verifique se a variável *JSESSIONID* do *https://sp.auth.adobe.com/authenticate/saml* a solicitação de rede corresponde ao *JSESSIONID* do *https://sp.auth.adobe.com/session* solicitação de rede.


### Solução de problemas do AccessEnabler JavaScript SDK versão 3.5.0 {#350-Troubleshooting}

O fluxo de autenticação do usuário pode ser afetado no Chrome 80 e superior (exceto a versão 82). Para garantir que o usuário não tenha problemas para autenticar devido às atualizações acima, é possível:

- Verifique se a variável *JSESSIONID* O cookie é definido no navegador e tem a variável *SameSite=None* e *Seguro* conjunto de atributos. 
- Verifique se a variável *JSESSIONID* do *https://sp.auth.adobe.com/authenticate/saml* a solicitação de rede corresponde ao *JSESSIONID* do *https://sp.auth.adobe.com/session* solicitação de rede.
- Verifique se a variável *pass\_sfp* O cookie é definido no navegador e tem a variável *SameSite=None* e *Seguro* conjunto de atributos.
- Verifique se a variável *pass\_sfp* cookie definido em *https://sp.auth.adobe.com/session* solicitação de rede.


O fluxo de autorização do usuário pode ser afetado no Chrome 80 e superior (exceto na versão 82). Para garantir que o usuário não tenha problemas para assistir a um recurso protegido, depois de ter sido autenticado com êxito, devido às atualizações acima, é possível:

- Verifique se a variável *pass\_sfp* O cookie é definido no navegador e tem a variável *SameSite=None* e *Seguro* conjunto de atributos.
- Verifique se a variável *pass\_sfp* cookie definido em *https://sp.auth.adobe.com/adobe-services/authorize* solicitação de rede.
- Verifique se a variável *pass\_sfp* cookie definido em *https://sp.auth.adobe.com/adobe-services/shortAuthorize* solicitação de rede.
