---
title: Sobre certificados
description: Sobre certificados
copied-description: true
exl-id: 24ca19bb-a71e-461a-9c3c-558d650e2d99
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Sobre certificados {#about-certificates}

O SDK do Adobe Primetime DRM está disponível nas seguintes configurações:

* SDK de produção DRM do Primetime
* SDK de avaliação DRM do Primetime
* SDK de avaliação do Primetime DRM

Para usar o SDK do DRM do Primetime para criar um servidor de licenciamento, você deve obter certificados digitais do Adobe. Os certificados digitais (também chamados simplesmente de certificados) vinculam uma entidade, como um indivíduo, organização ou sistema, a um par específico de chaves públicas e privadas. Certificados digitais podem ser considerados credenciais eletrônicas que verificam a identidade de um indivíduo, sistema ou organização.

Para permitir o máximo de flexibilidade e segurança aprimorada em suas opções de implantação, o SDK DRM do Primetime requer quatro certificados:

* Certificado do License Server

   O SDK usa esse certificado para assinar licenças de conteúdo emitidas para clientes.
* Certificado do empacotador

   O SDK usa esse certificado para gerar metadados DRM ao empacotar (criptografar) o conteúdo.
* Certificado de transporte

   O SDK usa esse certificado para proteger a comunicação entre os clientes e o servidor de licenças.
* Certificado CA do domínio

   Os clientes que desejam implementar um servidor de domínio precisam do certificado de autoridade de certificação de domínio. Ao contrário dos outros certificados, o certificado de autoridade de certificação de domínio não é emitido pelo Adobe.

>[!NOTE]
>
>Para o SDK de avaliação e o SDK de avaliação, os certificados do License Server, Packager e Transport são combinados em um único certificado.
