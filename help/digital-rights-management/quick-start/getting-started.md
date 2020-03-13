---
seo-title: Introdução
title: Introdução
uuid: 2002cf94-c8a7-4820-a560-6d9f7f33ee97
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Introdução {#getting-started}

Este documento fornece as etapas para uma configuração e implantação rápidas de um ecossistema DRM do Adobe Primetime que usa o Download Progressivo para distribuir conteúdo, e o Servidor DRM Primetime para streaming protegido para distribuição de licenças. Os seguintes guias fornecem detalhes adicionais sobre cada etapa:

* *Uso do servidor DRM Primetime para proteção de conteúdo*
* *Usando o servidor DRM Primetime para transmissão protegida*

O Primetime DRM Server for Protected Streaming é um servidor de funcionalidade mínima que não inclui o código fonte. Para um servidor modificável com fonte Java completa, consulte o guia *Usando as Implementações* de referência do DRM Primetime. Se você configurar um servidor de Licença de Referência, este substituirá a etapa *Configuração e implantará o Primetime DRM Server para Protected Streaming (License Server)* .

## Pré-requisitos {#prerequisites}

Antes de começar, conclua as seguintes tarefas:

* Adquira dois computadores Windows ou Linux:

   * Um computador será o License Server.
   * Um computador será o Servidor de conteúdo.

* Instale os seguintes aplicativos em ambos os computadores:

   * Tomcat 6.0.18
   * Java 1.6

## Obter certificados {#obtain-certificates}

Depois que o software SDK for entregue, o Administrador de certificados da empresa designado receberá um convite para concluir o processo de registro da inscrição de certificados DRM do Adobe Primetime. Para obter mais informações, consulte o Guia *de inscrição de certificados DRM Primetime*.

1. O administrador nomeia pelo menos um indivíduo para agir como o Solicitante de certificado.
1. O Solicitante de certificado gera uma chave privada e um CSR.
1. O Requerente envia uma solicitação de certificado.
1. O Administrador da empresa aprova a solicitação.
1. O Administrador de certificados da Adobe confirma o envio.
1. O Solicitante recebe o certificado, vincula o certificado à chave privada e implanta o certificado. conforme descrito em .

   Para obter mais informações sobre a implantação do certificado, consulte o guia *Implantação do Adobe Primetime DRM Server para Protected Streaming* .
1. As etapas de 3 a 6 devem ser concluídas para cada tipo de certificado.

   Para a versão Primetime DRM Production, o Solicitante deve fazer solicitações separadas para os certificados License Server, Packaging e Transport, que são válidos por dois anos.

   Os clientes que usam as versões de Avaliação ou Avaliação do Primetime DRM precisam apenas de um certificado válido por 1 ano/90 dias, respectivamente.