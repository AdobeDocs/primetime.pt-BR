---
description: O Adobe fornece um serviço de DRM em nuvem para clientes de DRM da Adobe Primetime que não desejam desenvolver e manter seu próprio servidor de licença de DRM Primetime. Ao utilizar esse serviço, os clientes podem reduzir a complexidade operacional e de desenvolvimento da emissão de licenças de DRM. O DRM da Primetime Cloud pode emitir licenças de DRM para todos os dispositivos capazes de executar um aplicativo de vídeo habilitado para Primetime Browser TVSDK, como iOS, Android, Desktops e Xbox360. Esse serviço de DRM é hospedado e mantido pelo Adobe, com tempo de atividade 24 horas por dia, 7 dias por semana.
title: Histórico
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Plano de fundo {#background}

O Adobe fornece um serviço de DRM em nuvem para clientes de DRM da Adobe Primetime que não desejam desenvolver e manter seu próprio servidor de licença de DRM Primetime. Ao utilizar esse serviço, os clientes podem reduzir a complexidade operacional e de desenvolvimento da emissão de licenças de DRM. O DRM da Primetime Cloud pode emitir licenças de DRM para todos os dispositivos capazes de executar um aplicativo de vídeo habilitado para Primetime Browser TVSDK, como iOS, Android, Desktops e Xbox360. Esse serviço de DRM é hospedado e mantido pelo Adobe, com tempo de atividade 24 horas por dia, 7 dias por semana.

>[!NOTE]
>
>O DRM da Adobe Primetime era anteriormente chamado de Adobe Access e, antes disso, Flash Access.

## O que está incluído no Primetime Cloud DRM {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* Módulo de Autenticação/Direito personalizado e instruções sobre como engajar a autenticação personalizada para o seu conteúdo. Para obter mais documentação, consulte o diretório [!DNL Custom Authentication Entitlement] .
* Certificado do Servidor de Licenças específico para DRM na nuvem ( [!DNL .pem/.cer/.der])

* Certificado de transporte do servidor de licença específico para DRM na nuvem ( [!DNL .pem/.cer/.der])

* Pacote Offline do Primetime Java
* Exemplos de políticas de DRM para empacotamento

   * **policy_24hr**  - Cache de licenças no disco por 24 horas. Após 24 horas, uma nova licença deve ser adquirida para visualizar o conteúdo. Todas as outras políticas neste kit também possuem cache de licenças de 24 horas.
   * **policy_ios_remotekeyserver**  - Em dispositivos iOS, a licença de DRM será adquirida do Cloud DRM. Além disso, o cliente adquirirá todas as chaves de descriptografia do AES do DRM da nuvem. A reprodução não é permitida em dispositivos iOS com falha na prisão.

   * **policy_ios_localkeyserver**  - Nos dispositivos iOS, a licença de DRM será adquirida do Cloud DRM. Além disso, o cliente adquirirá todas as chaves de descriptografia do AES HLS de um servidor HTTP local, em vez do DRM da nuvem. A reprodução não é permitida em dispositivos iOS com falha na prisão.

   * **policy_adobePass**  - O cliente deve primeiro autenticar com (anteriormente chamado de Adobe Pass) ou uma licença será negada.

* Ferramenta Adobe Policy Manager para criar políticas de DRM adicionais
* Amostra do conteúdo do vídeo para uso na embalagem

