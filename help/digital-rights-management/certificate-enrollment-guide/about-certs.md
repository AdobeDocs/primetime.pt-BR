---
title: Sobre certificados
description: Sobre certificados
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Sobre certificados {#about-certificates}

O SDK de DRM da Adobe Primetime está disponível nas seguintes configurações:

* SDK de produção de DRM do Primetime
* SDK de avaliação de DRM do Primetime
* SDK de avaliação de DRM do Primetime

Para usar o SDK de DRM do Primetime para criar um servidor de licenças, você deve obter certificados digitais do Adobe. Certificados digitais (também chamados simplesmente de certificados) vinculam uma entidade, como um indivíduo, organização ou sistema, a um par específico de chaves públicas e privadas. Certificados digitais podem ser considerados credenciais eletrônicas que verificam a identidade de um indivíduo, sistema ou organização.

Para permitir o máximo de flexibilidade e segurança aprimorada nas opções de implantação, o SDK de DRM do Primetime requer quatro certificados:

* Certificado do Servidor de Licenças

   O SDK usa esse certificado para assinar licenças de conteúdo emitidas para clientes.
* Certificado do empacotador

   O SDK usa esse certificado para gerar metadados DRM ao empacotar (criptografar) conteúdo.
* Certificado de transporte

   O SDK usa esse certificado para proteger a comunicação entre os clientes e o servidor de licenças.
* Certificado de autoridade de certificação de domínio

   Os clientes que desejam implementar um servidor de domínio precisam do certificado de autoridade de certificação de domínio. Ao contrário dos outros certificados, o certificado de autoridade de certificação de domínio não é emitido pelo Adobe.

>[!NOTE]
>
>Para o SDK de avaliação e o SDK de avaliação, os certificados do License Server, do Packager e do Transport são combinados em um único certificado.

