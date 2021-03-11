---
title: Introdução
description: Introdução
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Introdução {#getting-started}

Este documento fornece as etapas para uma configuração e implantação rápidas de um ecossistema Adobe Primetime DRM que usa o Download Progressivo para distribuir conteúdo, e o Servidor DRM Primetime para transmissão protegida para distribuição de licenças. Detalhes adicionais sobre cada etapa são fornecidos nos guias a seguir:

* *Uso do servidor DRM Primetime para proteção de conteúdo*
* *Uso do servidor DRM do Primetime para transmissão protegida*

O Primetime DRM Server for Protected Streaming é um servidor de funcionalidade mínima que não inclui código fonte. Para um servidor modificável com fonte Java completa, consulte o guia *Using the Primetime DRM Reference Implementations*. Se você configurar um servidor de Licença de Referência, que substituirá a etapa *Configurar e implantar o Primetime DRM Server for Protected Streaming (License Server)*.

## Pré-requisitos {#prerequisites}

Antes de começar, conclua as seguintes tarefas:

* Obtenha dois computadores Windows ou Linux:

   * Um computador será o License Server.
   * Um computador será o Servidor de conteúdo.

* Instale os seguintes aplicativos em ambos os computadores:

   * Tomcat 6.0.18
   * Java 1.6

## Obter certificados {#obtain-certificates}

Depois que o software SDK for entregue, o Administrador de certificado da empresa designado receberá um convite para concluir o processo de registro de certificado DRM da Adobe Primetime. Para obter mais informações, consulte o *Guia de Registro de Certificado DRM Primetime*.

1. O Administrador nomeia pelo menos um indivíduo para agir como o Requerente do Certificado.
1. O Solicitante de Certificado gera uma chave privada e um CSR.
1. O Requerente envia uma solicitação de certificado.
1. O Administrador da Empresa aprova a solicitação.
1. O Administrador de Certificados do Adobe confirma o envio.
1. O Requester recebe o certificado, vincula o certificado à chave privada e implanta o certificado. conforme descrito em .

   Para obter mais informações sobre a implantação do certificado, consulte o guia *Implantação do servidor DRM Adobe Primetime para transmissão protegida* .
1. As etapas 3 a 6 devem ser concluídas para cada tipo de certificado.

   Para a versão Primetime DRM Production (Produção de DRM Primetime), o Solicitante deve fazer solicitações separadas para os certificados License Server, Packaging e Transport, que são válidos por dois anos.

   Os clientes que usam as versões de Avaliação ou Avaliação de DRM do Primetime precisam apenas de um certificado válido por 1 ano/90 dias, respectivamente.