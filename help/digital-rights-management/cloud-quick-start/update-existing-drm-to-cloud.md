---
seo-title: Atualizar o conteúdo DRM existente para usar o DRM em nuvem (opcional)
title: Atualizar o conteúdo DRM existente para usar o DRM em nuvem (opcional)
uuid: cfabeb06-210f-45af-b8a6-8e0b03a76103
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# Atualize o conteúdo DRM existente para usar a Cloud DRM (Opcional) {#update-existing-drm-content-to-use-cloud-drm-optional}

Se você tiver uma biblioteca de conteúdo protegida pelo Primetime DRM, será possível &quot;recabeçalho&quot; do conteúdo existente para usar o serviço Primetime Cloud DRM, em vez de precisar reempacotar/criptografar os arquivos de origem originais. A regravação de cabeçalhos do conteúdo simplesmente atualiza os Metadados DRM do conteúdo no manifesto HLS. Ele não executa nenhuma descriptografia/recriptografia do ativo original. Essa pode ser uma opção útil se o conteúdo de origem original não estiver disponível ou se houver preocupação sobre a quantidade de recursos necessários para reempacotar uma biblioteca grande.

É possível usar o Primetime DRM Java SDK para atualizar os metadados de forma programática. Além disso, a ferramenta de linha de comando [!DNL OfflinePackager.jar] incluída com este Kit de Proteção também pode realizar essa tarefa usando a opção `-drm_refresh`.

## Detalhes do novo cabeçalho {#section_3F3980D8E775450588C64E02A8448189}

A substituição de cabeçalhos deve atualizar os seguintes campos para usar a CloudDRM:

* URL do License Server (Para [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* Certificado do servidor de licença (para o certificado do servidor de licença CloudDRM)
* Certificado de transporte (para o certificado de transporte CloudDRM)
* Credencial do Packager (para a credencial do Packager que você ativou para uso com a CloudDRM)

## Localizando os metadados do DRM {#section_28721CB7966F40708AEC8637F2E9BB72}

O conteúdo que usa a tecnologia HTTP (como HDS ou HLS) utiliza um manifesto que faz referência aos metadados de DRM de acesso ao Adobe. Em HDS, os metadados são referenciados pela tag `<drmmeta>` e, em HLS, são referenciados pela tag `#EXT-X-FAXS-CM`. Em qualquer um dos cenários, os metadados podem ser contidos em linha no manifesto como um blob codificado em base 64 ou referenciados externamente como um arquivo binário. Se os metadados forem incorporados/incorporados no manifesto, talvez seja necessário decodificar os metadados em dados binários antes de usar esses dados para instanciar os metadados DRM.

## Usar o OfflinePacakger.jar {#section_37C2091856E44AA380D742C72B4DD1A7} incluído

Forneça `-drm_refresh option` para a linha de comando. Um novo arquivo manifest será criado com os Metadados DRM atualizados, enquanto o conteúdo não será criptografado novamente.

## Uso do SDK Java DRM Primetime para recabeçalho {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

A atualização de metadados DRM existentes pode ser realizada usando o SDK Java DRM Primetime (anteriormente conhecido como DRM de acesso ao Adobe) para uma abordagem programática. Para obter mais detalhes, consulte a amostra de código [!DNL RegenerateMetadata.java] no pacote [!DNL /Reference Implmentation/Command Line Tools/samples/] do SDK. O SDK do Java de acesso ao Adobe não faz parte deste Kit de proteção do CloudDRM e deve ser adquirido diretamente do Adobe. Entre em contato com seu contato comercial com a Adobe para obter mais detalhes.