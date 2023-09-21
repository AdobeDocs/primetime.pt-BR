---
description: O Adobe fornece um serviço de DRM da nuvem para clientes do Adobe Primetime DRM que não desejam desenvolver e manter seu próprio servidor de licenças de DRM do Primetime. Com a utilização desse serviço, os clientes podem reduzir a complexidade operacional e de desenvolvimento relacionada à emissão de licenças de DRM. O Primetime Cloud DRM pode emitir licenças DRM para todos os dispositivos capazes de executar um aplicativo de vídeo habilitado para TVSDK do navegador Primetime, como iOS, Android, Desktops e Xbox 360. Esse serviço de DRM é hospedado e mantido pelo Adobe, com tempo de atividade de 24 horas por dia, 7 dias por semana.
title: Histórico
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Histórico {#background}

O Adobe fornece um serviço de DRM da nuvem para clientes do Adobe Primetime DRM que não desejam desenvolver e manter seu próprio servidor de licenças de DRM do Primetime. Com a utilização desse serviço, os clientes podem reduzir a complexidade operacional e de desenvolvimento relacionada à emissão de licenças de DRM. O Primetime Cloud DRM pode emitir licenças DRM para todos os dispositivos capazes de executar um aplicativo de vídeo habilitado para TVSDK do navegador Primetime, como iOS, Android, Desktops e Xbox 360. Esse serviço de DRM é hospedado e mantido pelo Adobe, com tempo de atividade de 24 horas por dia, 7 dias por semana.

>[!NOTE]
>
>O Adobe Primetime DRM era anteriormente chamado de Adobe Access e, antes disso, Flash Access.

## O que está incluído no Primetime Cloud DRM {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* Módulo de autenticação/direito personalizado e instruções sobre como realizar a autenticação personalizada para o seu conteúdo. Para obter mais documentação, consulte o [!DNL Custom Authentication Entitlement] diretório.
* Certificado de servidor de licenças específico do DRM de nuvem ( [!DNL .pem/.cer/.der])

* Certificado de Transporte de Servidor de Licenças específico para DRM de nuvem ( [!DNL .pem/.cer/.der])

* Empacotador offline Java do Primetime
* Exemplo de políticas de DRM para empacotamento

   * **policy_24hr** - Licenças de cache em disco por 24 horas. Após 24 horas, uma nova licença deve ser adquirida para visualizar o conteúdo. Todas as outras políticas neste kit também têm cache de licença de 24 horas.
   * **policy_ios_remotekeyserver** - Em dispositivos iOS, a licença do DRM será adquirida do Cloud DRM. Além disso, o cliente adquirirá todas as chaves de descriptografia AES do DRM da nuvem. A reprodução não é permitida em dispositivos iOS com jailbreak.

   * **policy_ios_localkeyserver** - Em dispositivos iOS, a licença do DRM será adquirida do Cloud DRM. Além disso, o cliente adquirirá todas as chaves de descriptografia HLS AES de um servidor HTTP local, em vez do DRM da nuvem. A reprodução não é permitida em dispositivos iOS com jailbreak.

   * **policy_adobePass** - Primeiro, o cliente deve se autenticar no (anteriormente chamado de Adobe Pass), caso contrário, uma licença será negada.

* Ferramenta Adobe Policy Manager para criar políticas DRM adicionais
* Exemplo de conteúdo de vídeo a ser usado para empacotamento
