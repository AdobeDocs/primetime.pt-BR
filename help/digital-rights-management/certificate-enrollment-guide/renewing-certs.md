---
title: Renovar certificados
description: Renovar certificados
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# Renovar certificados{#renew-certificates}

Você deve estar ciente das seguintes restrições de renovação de certificado que são baseadas na configuração do SDK do Adobe Primetime DRM:

* SDK de produção de DRM do Primetime

   O Adobe fornece o conjunto inicial de certificados gratuitos para o SDK de produção de DRM do Primetime quando você compra um contrato de suporte. Se você não tiver um contrato de suporte, poderá comprar um conjunto de certificados de renovação válidos por dois anos.
* SDK de avaliação de DRM do Primetime

   O conjunto de certificados para este SDK é válido por um ano e não pode ser renovado.
* SDK de avaliação de DRM do Primetime

   O SDK de avaliação de DRM do Primetime é válido por três meses e o Adobe fornece um conjunto de certificados de renovação gratuitos.

## Implementar novos certificados e usar certificados antigos para conteúdo existente {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

No Primetime DRM, você pode permitir que um servidor de licenças emita uma licença para conteúdo empacotado com certificados anteriores (ou mesmo expirados) do empacotador. Para configurar o servidor para aceitar solicitações de licença de conteúdo empacotado anteriormente, forneça seu certificado antigo ao servidor e atualize o arquivo de configuração do servidor para que o servidor saiba onde encontrar os certificados antigos. Para obter mais informações, consulte *Manipular atualizações de certificado quando certificados emitidos por Adobe expirarem* em *Usar o Adobe Primetime DRM SDK para proteger conteúdo*.

Se o aplicativo de servidor for baseado na Implementação de referência de DRM do Primetime, não será necessário atualizar o programa do lado do servidor. No arquivo `flashaccess-refimpl.properties`, há campos nos quais você pode especificar certificados adicionais de Servidor de Transporte e Licença. Se você tiver apenas um certificado, não precisará preencher essas propriedades. Se você tiver expirado os certificados e quiser usá-los ao emitir respostas de licença, forneça esses certificados ao arquivo de configuração e reinicie o servidor.

Para especificar certificados antigos, use as seguintes propriedades:

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`

