---
title: Renovar certificados
description: Renovar certificados
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Renovar certificados{#renew-certificates}

Você deve estar ciente das seguintes restrições de renovação de certificado, que são baseadas na configuração do SDK do Adobe Primetime DRM:

* SDK de produção DRM do Primetime

  O Adobe fornece o conjunto inicial de certificados gratuitos para o SDK de produção do Primetime DRM quando você compra um contrato de suporte. Se você não tiver um contrato de suporte, poderá adquirir um conjunto de certificados de renovação válidos por dois anos.
* SDK de avaliação DRM do Primetime

  O certificado definido para este SDK é válido por um ano e não pode ser renovado.
* SDK de avaliação do Primetime DRM

  O SDK de avaliação do Primetime DRM é válido por três meses, e o Adobe fornece um conjunto de certificados de renovação gratuitos.

## Implementar novos certificados e usar certificados antigos para conteúdo existente {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

No Primetime DRM, você pode permitir que um servidor de licenças emita uma licença para conteúdo que é empacotado com certificados de empacotador anteriores (ou até mesmo expirados). Para configurar o servidor para aceitar solicitações de licença de conteúdo empacotado anteriormente, forneça o certificado antigo ao servidor e atualize o arquivo de configuração dele para que o servidor saiba onde encontrar os certificados antigos. Para obter mais informações, consulte *Manipulação de atualizações de certificado quando os certificados emitidos pelo Adobe expiram* in *Utilização do SDK do Adobe Primetime DRM para proteção de conteúdo*.

Se o aplicativo do servidor for baseado na Implementação de referência de DRM do Primetime, não será necessário atualizar o programa do lado do servidor. No `flashaccess-refimpl.properties` , há campos nos quais você pode especificar certificados adicionais de Transporte e de Servidor de Licenças. Se você tiver apenas um certificado, não será necessário preencher essas propriedades. Se você tiver certificados expirados e quiser usá-los ao emitir respostas de licença, forneça esses certificados ao arquivo de configuração e reinicie o servidor.

Para especificar certificados antigos, use as seguintes propriedades:

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`
