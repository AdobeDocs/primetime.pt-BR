---
seo-title: Sobre certificados
title: Sobre certificados
uuid: 0b7818b4-bd6a-4f2e-94c2-565e0d735bf8
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

---


# Sobre certificados {#about-certificates}

O SDK do Adobe Primetime DRM está disponível nas seguintes configurações:

* SDK de produção do DRM Primetime
* SDK de avaliação do DRM Primetime
* SDK de avaliação do DRM Primetime

Para usar o SDK DRM Primetime para criar um servidor de licenças, você deve obter certificados digitais da Adobe. Certificados digitais (também chamados simplesmente de certificados) vinculam uma entidade, como um indivíduo, uma organização ou um sistema, a um par específico de chaves públicas e privadas. Certificados digitais podem ser considerados como credenciais eletrônicas que verificam a identidade de um indivíduo, sistema ou organização.

Para permitir máxima flexibilidade e segurança aprimorada nas opções de implantação, o SDK do Primetime DRM requer quatro certificados:

* Certificado do servidor de licença

   O SDK usa esse certificado para assinar licenças de conteúdo emitidas para clientes.
* Certificado da Packager

   O SDK usa esse certificado para gerar metadados DRM ao empacotar (criptografar) conteúdo.
* Certificado de transporte

   O SDK usa esse certificado para proteger a comunicação entre os clientes e o servidor de licenças.
* Certificado de autoridade de domínio

   Os clientes que desejam implementar um servidor de domínio precisam do certificado da CA de domínio. Ao contrário dos outros certificados, o certificado da CA de domínio não é emitido pela Adobe.

>[!NOTE]
>
>Para o SDK de avaliação e o SDK de avaliação, os certificados do License Server, Packager e Transport são combinados em um único certificado.

