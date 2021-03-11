---
description: Para configurar o Adobe® Access™ para uso, copie arquivos do DVD. Esses arquivos incluem arquivos JAR contendo código, certificados e classes de terceiros. Além disso, solicite um certificado da Adobe Systems Incorporated. Você receberá várias credenciais usadas para proteger a integridade de conteúdo empacotado, licenças e comunicação entre o cliente e o servidor.
title: Configuração do ambiente de desenvolvimento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Configurar o SDK {#setting-up-the-sdk}

Para configurar o Adobe® Access™ para uso, copie arquivos do DVD. Esses arquivos incluem arquivos JAR contendo código, certificados e classes de terceiros. Além disso, solicite um certificado da Adobe Systems Incorporated. Você receberá várias credenciais usadas para proteger a integridade de conteúdo empacotado, licenças e comunicação entre o cliente e o servidor.

O SDK de Acesso ao Adobe está disponível em dois tipos:
* Adobe Access Core SDK
* Adobe Access Professional SDK

A tabela a seguir mostra uma comparação básica dos SDKs do Adobe Access:

| Recurso | Adobe Access Core SDK | Adobe Access Professional SDK |
|---|---|---|
| Recursos do Flash Access 2.0 | Disponível | Disponível |
| Rotação de chaves | - | Disponível |
| Suporte de domínio | Disponível | Disponível |
| Encadeamento de licença aprimorado | Disponível | Disponível |
| Mensagens de sincronização | Disponível | Disponível |
| Pré-geração de Licença | Disponível | Disponível |
| Licenças incorporadas | Disponível | Disponível |

## Configuração do ambiente de desenvolvimento {#setting-up-the-development-environment}

No DVD, copie os seguintes arquivos SDK para uso no ambiente de desenvolvimento e no classpath do Java:

* adobe-flashaccess-certs.jar (contém certificados Adobe root)
* adobe-flashaccess-sdk.jar (contém classes SDK do Adobe Access Core)
* adobe-flashaccess-sdk-pro.jar (contém classes SDK do Adobe Access Professional, necessárias apenas para recursos Professional)

Você precisa dos seguintes arquivos JAR de terceiros também localizados no DVD na pasta &quot;de terceiros&quot; do SDK:

* bcmail-jdk15-141.jar
* bcprov-jdk15-141.jar
* commons-discovery-0.4.jar
* commons-logging-1.1.1.jar
* cryptoj.jar
* jaxb-api.jar
* jaxb-impl.jar
* jaxb-libs.jar
* relaxngDatatype.jar
* rm-pdrl.jar
* xsdlib.jar

Para melhorar o desempenho, opcionalmente, é possível ativar o suporte nativo para operações criptográficas, implantando as bibliotecas específicas da plataforma localizadas na pasta &quot;thirdparty/cryptoj&quot; do SDK. Para ativar o suporte nativo, adicione a biblioteca para sua plataforma (jsafe.dll para Windows ou libjsafe.so para Linux) ao caminho. As versões de 32 bits e 64 bits dessas bibliotecas são fornecidas. (Observe que a versão de 64 bits só deve ser usada se você tiver um sistema operacional de 64 bits e estiver executando a versão de 64 bits do Java).

Além disso, uma parte opcional do SDK é adobe-flashaccess-lcrm.jar. Esse arquivo é necessário somente para a funcionalidade relacionada à compatibilidade do Adobe Flash Media Rights Management Server (FMRMS) 1.x. Se você implantou o FMRMS 1.x anteriormente e não quiser reempacotar seu conteúdo protegido por FMRMS, é necessário adicionar suporte ao servidor de licenças para que ele possa lidar com conteúdo e clientes antigos.
