---
title: Atualize o conteúdo de DRM existente para usar o DRM da nuvem (opcional)
description: Atualize o conteúdo de DRM existente para usar o DRM da nuvem (opcional)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# Atualize o conteúdo de DRM existente para usar o DRM da nuvem (opcional) {#update-existing-drm-content-to-use-cloud-drm-optional}

Se você tiver uma biblioteca de conteúdo existente protegida pelo DRM do Primetime, é possível &quot;redirecionar&quot; o conteúdo existente para usar o serviço DRM da Primetime Cloud, em vez de ter que reempacotar/criptografar os arquivos de origem originais. A renomeação do conteúdo simplesmente atualiza os metadados de DRM do conteúdo no manifesto HLS. Ele não executa nenhuma descriptografia/recriptografia do ativo original. Essa pode ser uma opção útil se o conteúdo de origem original não estiver disponível ou se houver preocupação sobre a quantidade de recursos necessários para reempacotar uma biblioteca grande.

É possível usar o SDK Java de DRM do Primetime para atualizar os metadados de forma programática. Além disso, a ferramenta de linha de comando [!DNL OfflinePackager.jar] incluída neste Kit de Proteção também pode realizar essa tarefa usando a opção `-drm_refresh`.

## Detalhes do recabeçalho {#section_3F3980D8E775450588C64E02A8448189}

A renomeação deve atualizar os seguintes campos para usar o CloudDRM:

* URL do Servidor de Licenças (Para [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* Certificado do servidor de licença (para o certificado do servidor de licenças CloudDRM)
* Certificado de transporte (para o certificado de transporte CloudDRM)
* Credencial do Empacotador (Para a credencial do empacotador que você ativou para uso com o CloudDRM)

## Localização dos metadados de DRM {#section_28721CB7966F40708AEC8637F2E9BB72}

O conteúdo que usa a tecnologia HTTP (como HDS ou HLS) usa um manifesto que faz referência aos metadados de DRM de acesso do Adobe. No HDS, os metadados são referenciados pela tag `<drmmeta>` e, no HLS, são referenciados pela tag `#EXT-X-FAXS-CM` . Em qualquer um dos cenários, os metadados podem ser contidos em linha no manifesto como um blob codificado na base 64 ou referenciados externamente como um arquivo binário. Se os metadados forem incorporados/incorporados no manifesto, talvez seja necessário primeiro decodificar a base64 dos metadados em dados binários antes de usá-los para instanciar os metadados de DRM.

## Usar o OfflinePacakger.jar incluído {#section_37C2091856E44AA380D742C72B4DD1A7}

Forneça o `-drm_refresh option` para a linha de comando. Um novo arquivo de manifesto será criado com metadados DRM atualizados, enquanto o conteúdo não será criptografado novamente.

## Uso do SDK Java de DRM do Primetime para recabeçalho {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

A atualização de metadados de DRM existentes pode ser realizada usando o SDK Java de DRM Primetime (anteriormente conhecido como DRM de acesso ao Adobe) para uma abordagem programática. Para obter mais detalhes, consulte a amostra de código [!DNL RegenerateMetadata.java] no pacote [!DNL /Reference Implmentation/Command Line Tools/samples/] do SDK. O SDK Java do Adobe Access não faz parte desse Kit de proteção do CloudDRM e deve ser adquirido diretamente do Adobe. Entre em contato com seu contato comercial do Adobe para obter mais detalhes.