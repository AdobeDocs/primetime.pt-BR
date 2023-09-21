---
title: Introdução
description: Introdução
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# Introdução {#getting-started}

Este documento fornece as etapas para uma configuração e implantação rápidas de um ecossistema de DRM do Adobe Primetime que usa o Download progressivo para distribuir conteúdo, e do Servidor DRM do Primetime para transmissão protegida para distribuição de licença. Detalhes adicionais sobre cada etapa são fornecidos nos seguintes guias:

* *Uso do servidor DRM Primetime para proteção de conteúdo*
* *Uso do servidor DRM Primetime para transmissão protegida*

O servidor DRM do Primetime para transmissão protegida é um servidor com funcionalidade mínima que não inclui código-fonte. Para um servidor modificável com código-fonte Java completo, consulte *Uso das implementações de referência de DRM do Primetime* guia. Se você configurar um servidor de Licença de referência, isso substituirá o *Configurar e implantar o servidor DRM Primetime para transmissão protegida (Servidor de licenças)* etapa.

## Pré-requisitos {#prerequisites}

Antes de começar, conclua as seguintes tarefas:

* Obtenha dois computadores Windows ou Linux:

   * Um computador será o License Server.
   * Um computador será o Servidor de conteúdo.

* Instale os seguintes aplicativos em ambos os computadores:

   * Tomcat 6.0.18
   * Java 1.6

## Obter certificados {#obtain-certificates}

Depois que o software SDK for entregue, o Administrador de Certificados da Empresa designado receberá um convite para concluir o processo de registro do Registro de Certificados DRM da Adobe Primetime. Para obter mais informações, consulte *Guia de inscrição de certificado DRM do Primetime*.

1. O Administrador nomeia pelo menos uma pessoa para atuar como Solicitante de certificado.
1. O Solicitante do certificado gera uma chave privada e uma CSR.
1. O Solicitante envia uma solicitação de certificado.
1. O Administrador da empresa aprova a solicitação.
1. O Administrador do Certificado de Adobe confirma o envio.
1. O Solicitante recebe o certificado, vincula o certificado à chave privada e implanta o certificado. conforme descrito em .

   Para obter mais informações sobre a implantação do certificado, consulte a *Implantação do servidor DRM do Adobe Primetime para transmissão protegida* guia.
1. As etapas 3 a 6 devem ser concluídas para cada tipo de certificado.

   Para a versão de Produção DRM do Primetime, o Solicitante deve fazer solicitações separadas para os certificados Servidor de licenças, Empacotamento e Transporte, que são válidos por dois anos.

   Os clientes que usam a Avaliação DRM do Primetime ou as versões de avaliação precisam apenas de um certificado válido por 1 ano/90 dias, respectivamente.
