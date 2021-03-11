---
title: Criar políticas de DRM personalizadas (Opcional)
description: Criar políticas de DRM personalizadas (Opcional)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Criar políticas de DRM personalizadas (Opcional){#create-custom-drm-policies-optional}

O Kit de proteção DRM da Primetime Cloud vem com algumas políticas pré-configuradas que podem ser usadas durante o empacotamento. Se outras configurações de política forem desejadas, por exemplo, um direito de listagem de permissões de SWF específico, o Gerenciador de políticas de DRM do Primetime incluído poderá ser usado para gerar políticas personalizadas.

>[!NOTE]
>
>Todas as políticas devem usar a autenticação ANONYMOUS (não a Senha do nome de usuário ou Personalizada) - independentemente de o fluxo de trabalho Autenticação/Direito personalizado ser ou não usado.

Incluído com o Gerenciador de políticas é o arquivo de configuração [!DNL flashaccesstools.properties], que foi modificado para expor apenas as opções de política configuráveis suportadas pelo Serviço DRM da Primetime Cloud. Definir as opções de política que não são suportadas pelo Serviço DRM da Primetime Cloud resultará em erros de aquisição de licença. Para obter informações sobre como usar o Gerenciador de políticas de DRM do Primetime, consulte: [Implementações de referência de DRM do Primetime: Gerenciador de políticas](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

Para criar uma nova política, atualize o arquivo [!DNL flashaccesstools.properties] conforme desejado e use o comando:

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## Criar políticas dinamicamente para Autenticação/Direito Personalizado{#create-policies-dynamically-for-custom-auth-entitlement}

Se estiver usando a Autenticação/Direito personalizado de DRM da Primetime Cloud e quiser criar dinamicamente uma nova política de DRM para cada solicitação de licença (em vez de extrair políticas de um pool pré-gerado), o Adobe recomenda usar o SDK Java de DRM do Primetime diretamente. O uso direto do SDK do Java é mais rápido que a ferramenta [!DNL AdobePolicyManager.jar], que gera automaticamente o arquivo de política para o disco, incorrendo na sobrecarga de E/S do disco.

É possível encontrar o código de amostra usando o SDK do Java no diretório [!DNL /Primetime DRM PolicyManager/sampleCode/], chamado [!DNL CreatePolicy.java] e [!DNL CreatePolicyWithOutputProtection.java]. Javadocs e documentação do SDK do Java podem ser encontrados em [An Overview of Adobe Primetime DRM SDK](../../../digital-rights-management/drm-sdk-overview/overview.md)

Para criar e executar as amostras, copie os arquivos .java na pasta ../libs/ e execute:

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
