---
description: A Adobe fornece um serviço de DRM em nuvem para clientes de DRM do Adobe Primetime que não desejam desenvolver e manter seu próprio Servidor de Licenças de DRM do Primetime. Ao utilizar esse serviço, os clientes podem reduzir a complexidade operacional e de desenvolvimento da emissão de licenças de DRM. O Primetime Cloud DRM pode emitir licenças de DRM para todos os dispositivos capazes de executar um aplicativo de vídeo ativado por TVSDK do navegador Primetime, como iOS, Android, Desktops e Xbox360. Esse serviço DRM é hospedado e mantido pela Adobe, com tempo de atividade 24 horas por dia, 7 dias por semana.
seo-description: A Adobe fornece um serviço de DRM em nuvem para clientes de DRM do Adobe Primetime que não desejam desenvolver e manter seu próprio Servidor de Licenças de DRM do Primetime. Ao utilizar esse serviço, os clientes podem reduzir a complexidade operacional e de desenvolvimento da emissão de licenças de DRM. O Primetime Cloud DRM pode emitir licenças de DRM para todos os dispositivos capazes de executar um aplicativo de vídeo ativado por TVSDK do navegador Primetime, como iOS, Android, Desktops e Xbox360. Esse serviço DRM é hospedado e mantido pela Adobe, com tempo de atividade 24 horas por dia, 7 dias por semana.
seo-title: Contexto
title: Contexto
uuid: 11a5b9ea-ebd2-47e0-b078-af2a3e1f7bf6
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Contexto {#background}

A Adobe fornece um serviço de DRM em nuvem para clientes de DRM do Adobe Primetime que não desejam desenvolver e manter seu próprio Servidor de Licenças de DRM do Primetime. Ao utilizar esse serviço, os clientes podem reduzir a complexidade operacional e de desenvolvimento da emissão de licenças de DRM. O Primetime Cloud DRM pode emitir licenças de DRM para todos os dispositivos capazes de executar um aplicativo de vídeo ativado por TVSDK do navegador Primetime, como iOS, Android, Desktops e Xbox360. Esse serviço DRM é hospedado e mantido pela Adobe, com tempo de atividade 24 horas por dia, 7 dias por semana.

>[!NOTE]
>
>O Adobe Primetime DRM era anteriormente chamado de Adobe Access, e antes disso, Flash Access.

## O que está incluído no Primetime Cloud DRM {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* Módulo Autenticação/Direito personalizado e instruções sobre como realizar a autenticação personalizada para seu conteúdo. Para obter mais documentação, consulte o [!DNL Custom Authentication Entitlement] diretório.
* Certificado do Servidor de Licenças Específico DRM da Cloud ( [!DNL .pem/.cer/.der])

* Certificado de Transporte do Servidor de Licença ( [!DNL .pem/.cer/.der]) específico para DRM da nuvem

* Primetime Java Offline Packager
* Exemplo de políticas de DRM para empacotamento

   * **policy_24hr** - Cache de licenças no disco por 24 horas. Após 24 horas, uma nova licença deve ser adquirida para exibir o conteúdo. Todas as outras políticas neste kit também possuem cache de 24 horas de licença.
   * **policy_ios_remotekeyserver** - Em dispositivos iOS, a licença DRM será adquirida do DRM da Cloud. Além disso, o cliente adquirirá todas as chaves de descriptografia AES do DRM da Cloud. A reprodução não é permitida em dispositivos iOS com falha na prisão.

   * **policy_ios_localkeyserver** - Em dispositivos iOS, a licença DRM será adquirida do DRM da Cloud. Além disso, o cliente adquirirá todas as chaves de decodificação AES HLS de um servidor HTTP local, em vez do DRM da nuvem. A reprodução não é permitida em dispositivos iOS com falha na prisão.

   * **policy_adobePass** - O cliente deve primeiro se autenticar com (anteriormente chamado de Adobe Pass) ou uma licença será negada.

* Ferramenta Adobe Policy Manager para criar políticas DRM adicionais
* Amostra de conteúdo de vídeo a ser usado para empacotamento

