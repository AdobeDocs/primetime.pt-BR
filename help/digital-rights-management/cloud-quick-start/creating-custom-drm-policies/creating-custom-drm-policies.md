---
title: Criar políticas DRM personalizadas (Opcional)
description: Criar políticas DRM personalizadas (Opcional)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Criar políticas DRM personalizadas (Opcional){#create-custom-drm-policies-optional}

O Kit de Proteção DRM do Primetime Cloud vem com algumas políticas pré-configuradas que podem ser usadas durante o empacotamento. Se desejar configurações de política adicionais, por exemplo, um direito de listagem de permissão de SWF específico, o Gerenciador de política DRM do Primetime incluído poderá ser usado para gerar políticas personalizadas.

>[!NOTE]
>
>Todas as políticas devem usar autenticação ANÔNIMA (não Nome de usuário Senha ou Personalizado), independentemente de o fluxo de trabalho Autenticação/Qualificação personalizada ser usado ou não.

Incluído com o Policy Manager está o [!DNL flashaccesstools.properties] arquivo de configuração, que foi modificado para expor apenas as opções de política configuráveis suportadas pelo Serviço DRM da Primetime Cloud. A configuração de opções de política que não têm suporte no Serviço DRM da Primetime Cloud resultará em erros de aquisição de licença. Para obter informações sobre como usar o Gerenciador de políticas do Primetime DRM, consulte: [Implementações de referência de DRM do Primetime: Policy Manager](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

Para criar uma nova política, atualize o [!DNL flashaccesstools.properties] e, em seguida, use o comando:

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## Crie políticas dinamicamente para Autenticação/Autorização personalizada{#create-policies-dynamically-for-custom-auth-entitlement}

Se você estiver usando Autenticação/qualificação personalizadas de DRM da Primetime Cloud e quiser criar dinamicamente uma nova política de DRM para cada solicitação de licença (em vez de extrair políticas de um pool pré-gerado), a Adobe recomenda usar o SDK Java DRM do Primetime diretamente. Usar o SDK do Java diretamente é mais rápido que o [!DNL AdobePolicyManager.jar] que gera automaticamente o arquivo de política para o disco, gerando sobrecarga de E/S de disco.

Um exemplo de código usando o SDK do Java pode ser encontrado no [!DNL /Primetime DRM PolicyManager/sampleCode/] diretório, nomeado [!DNL CreatePolicy.java] e [!DNL CreatePolicyWithOutputProtection.java]. Javadocs e a documentação do SDK do Java podem ser encontrados em [Uma visão geral do SDK do Adobe Primetime DRM](../../../digital-rights-management/drm-sdk-overview/overview.md)

Para criar e executar as amostras, copie os arquivos .java na pasta ../libs/ e execute:

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
