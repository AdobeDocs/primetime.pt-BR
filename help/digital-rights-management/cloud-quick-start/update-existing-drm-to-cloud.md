---
title: Atualizar conteúdo DRM existente para usar o DRM na nuvem (opcional)
description: Atualizar conteúdo DRM existente para usar o DRM na nuvem (opcional)
copied-description: true
exl-id: 89b1e99a-cb28-4524-9c47-f71f92d3753d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Atualizar conteúdo DRM existente para usar o DRM na nuvem (opcional) {#update-existing-drm-content-to-use-cloud-drm-optional}

Se você tiver uma biblioteca de conteúdo existente protegida pelo DRM do Primetime, é possível &quot;recarregar&quot; o conteúdo existente para usar o serviço DRM do Primetime Cloud, em vez de precisar empacotar/criptografar novamente os arquivos de origem originais. Redirecionar o conteúdo simplesmente atualiza os metadados DRM do conteúdo no manifesto HLS. Ele não executa qualquer cancelamento de criptografia/nova criptografia do ativo original. Essa pode ser uma opção útil se o conteúdo original não estiver disponível ou se houver preocupação sobre a quantidade de recursos necessários para empacotar uma grande biblioteca.

É possível usar o SDK do Java DRM do Primetime para atualizar os metadados de forma programática. Além disso, a [!DNL OfflinePackager.jar] ferramenta de linha de comando incluída neste kit de proteção também pode realizar esta tarefa usando o `-drm_refresh` opção.

## Detalhes do cabeçalho novamente {#section_3F3980D8E775450588C64E02A8448189}

O novo cabeçalho deve atualizar os seguintes campos para usar o CloudDRM:

* URL do Servidor de Licença (Para [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* Certificado de servidor de licença (para o certificado de servidor de licença CloudDRM)
* Certificado de transporte (para o certificado de transporte CloudDRM)
* Credencial do empacotador (para a credencial do empacotador que você ativou para uso com o CloudDRM)

## Localização dos metadados de DRM {#section_28721CB7966F40708AEC8637F2E9BB72}

O conteúdo que usa a tecnologia HTTP (como HDS ou HLS) utiliza um manifesto que faz referência aos metadados de DRM de acesso ao Adobe. Na HDS, os metadados são referenciados pela variável `<drmmeta>` e, no HLS, é referenciado pela variável `#EXT-X-FAXS-CM` tag. Em ambos os cenários, os metadados podem estar contidos em linha no manifesto como um blob codificado na base 64 ou referenciados externamente como um arquivo binário. Se os metadados estiverem incorporados/em linha no manifesto, talvez seja necessário primeiro decodificar os metadados em dados binários na base64 antes de usar esses dados para instanciar os metadados de DRM.

## Usar o OfflinePack.jar incluído {#section_37C2091856E44AA380D742C72B4DD1A7}

Forneça o `-drm_refresh option` para a linha de comando. Um novo arquivo de manifesto será criado com os metadados DRM atualizados, enquanto o conteúdo não será criptografado novamente.

## Utilização do SDK Java DRM do Primetime para redefinir o cabeçalho {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

A atualização de metadados de DRM existentes pode ser realizada usando o SDK Java DRM do Primetime (anteriormente conhecido como DRM de acesso ao Adobe) para uma abordagem programática. Para obter mais detalhes, consulte [!DNL RegenerateMetadata.java] amostra de código no [!DNL /Reference Implmentation/Command Line Tools/samples/] do SDK. O SDK do Java de acesso ao Adobe não faz parte desse Kit de proteção do Cloud DRM e deve ser adquirido diretamente do Adobe. Entre em contato com o contato comercial do Adobe para obter mais detalhes.
