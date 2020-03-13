---
seo-title: Renovar certificados
title: Renovar certificados
uuid: 12a560b0-966b-424e-bfe5-22e9c10d8667
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

---


# Renovar certificados{#renew-certificates}

Você deve estar ciente das seguintes restrições de renovação de certificado que são baseadas na configuração do SDK do Adobe Primetime DRM:

* SDK de produção do DRM Primetime

   A Adobe fornece o conjunto inicial de certificados gratuitos para o SDK de produção Primetime DRM quando você compra um contrato de suporte. Se você não tiver um contrato de suporte, poderá comprar um conjunto de certificados de renovação válidos por dois anos.
* SDK de avaliação do DRM Primetime

   O certificado definido para este SDK é válido por um ano e não pode ser renovado.
* SDK de avaliação do DRM Primetime

   O SDK de avaliação do DRM Primetime é válido por três meses e a Adobe fornece um conjunto de certificados de renovação gratuitos.

## Implementação de novos certificados e uso de certificados antigos para conteúdo existente {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

No DRM Primetime, é possível permitir que um servidor de licenças emita uma licença para conteúdo empacotado com certificados empacotadores anteriores (ou mesmo expirados). Para configurar o servidor para aceitar solicitações de licença de conteúdo empacotado anteriormente, forneça seu certificado antigo ao servidor e atualize o arquivo de configuração do servidor para que o servidor saiba onde encontrar os certificados antigos. Para obter mais informações, consulte *Manuseio de atualizações de certificados quando certificados emitidos pela Adobe expiram* em *Uso do SDK do Adobe Primetime DRM para Proteção de Conteúdo*.

Se o aplicativo do servidor for baseado na Implementação de referência do DRM Primetime, você não precisará atualizar o programa do lado do servidor. No `flashaccess-refimpl.properties` arquivo, há campos nos quais você pode especificar certificados adicionais de Transporte e Servidor de Licenças. Se você tiver apenas um certificado, não será necessário preencher essas propriedades. Se tiver certificados expirados e quiser usá-los ao emitir respostas de licença, forneça-os ao arquivo de configuração e reinicie o servidor.

Para especificar certificados antigos, use as seguintes propriedades:

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`

