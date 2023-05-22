---
description: Para configurar o Adobe® Access™ para uso, copie arquivos do DVD. Esses arquivos incluem arquivos JAR contendo código, certificados e classes de terceiros. Além disso, solicite um certificado da Adobe Systems Incorporated. Você receberá várias credenciais usadas para proteger a integridade do conteúdo empacotado, das licenças e da comunicação entre o cliente e o servidor.
title: Configuração do ambiente de desenvolvimento
exl-id: 66310fc8-7513-4aab-81d6-1370ce216cbf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Configuração do SDK {#setting-up-the-sdk}

Para configurar o Adobe® Access™ para uso, copie arquivos do DVD. Esses arquivos incluem arquivos JAR contendo código, certificados e classes de terceiros. Além disso, solicite um certificado da Adobe Systems Incorporated. Você receberá várias credenciais usadas para proteger a integridade do conteúdo empacotado, das licenças e da comunicação entre o cliente e o servidor.

O SDK de acesso ao Adobe está disponível em dois tipos:
* ADOBE ACCESS CORE SDK
* ADOBE ACCESS PROFESSIONAL SDK

A tabela a seguir mostra uma comparação básica entre SDKs de acesso ao Adobe:

| Recurso | ADOBE ACCESS CORE SDK | ADOBE ACCESS PROFESSIONAL SDK |
|---|---|---|
| Recursos do Flash Access 2.0 | Disponível | Disponível |
| Rotação de chaves | - | Disponível |
| Suporte de domínio | Disponível | Disponível |
| Encadeamento de licenças aprimorado | Disponível | Disponível |
| Mensagens de Sincronização | Disponível | Disponível |
| Licença de pré-geração | Disponível | Disponível |
| Licenças incorporadas | Disponível | Disponível |

## Configuração do ambiente de desenvolvimento {#setting-up-the-development-environment}

A partir do DVD, copie os seguintes arquivos SDK para uso no ambiente de desenvolvimento e no classpath do Java:

* adobe-flashaccess-certs.jar (contém certificados raiz de Adobe)
* adobe-flashaccess-sdk.jar (contém classes do SDK do Adobe Access Core)
* adobe-flashaccess-sdk-pro.jar (contém classes do SDK do Adobe Access Professional, necessárias apenas para recursos profissionais)

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

Para melhorar o desempenho, você pode ativar o suporte nativo para operações de criptografia implantando as bibliotecas específicas da plataforma localizadas na pasta &quot;thirdparty/cryptoj&quot; do SDK. Para ativar o suporte nativo, adicione a biblioteca da sua plataforma (jsafe.dll para Windows ou libjsafe.so para Linux) ao caminho. As versões de 32 bits e 64 bits dessas bibliotecas são fornecidas. (Observe que a versão de 64 bits só deve ser usada se você tiver um SO de 64 bits e estiver executando a versão de 64 bits do Java).

Além disso, uma parte opcional do SDK é adobe-flashaccess-lcrm.jar. Esse arquivo é necessário apenas para a funcionalidade relacionada à compatibilidade do Adobe Flash Media Rights Management Server (FMRMS) 1.x. Se você implantou anteriormente o FMRMS 1.x e não deseja reempacotar o conteúdo protegido por FMRMS, é necessário adicionar suporte ao servidor de licenças para que ele possa lidar com o conteúdo e os clientes antigos.
