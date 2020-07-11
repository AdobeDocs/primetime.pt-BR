---
seo-title: Criar políticas DRM personalizadas (Opcional)
title: Criar políticas DRM personalizadas (Opcional)
uuid: 701b51d9-6dde-4c21-bc5b-09e612582968
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Criar políticas DRM personalizadas (Opcional){#create-custom-drm-policies-optional}

O kit de proteção DRM da Primetime Cloud vem com algumas políticas pré-configuradas que podem ser usadas durante o empacotamento. Se outras configurações de política forem desejadas, por exemplo, um direito de listagem de permissão SWF específico, o Gerenciador de políticas DRM do Primetime pode ser usado para gerar políticas personalizadas.

>[!NOTE]
>
>Todas as políticas devem usar a autenticação ANONYMOUS (não Senha do nome de usuário ou Personalizado) - independentemente de o fluxo de trabalho de Autenticação/Direito personalizado ser usado ou não.

O Gerenciador de políticas está incluído no arquivo de [!DNL flashaccesstools.properties] configuração, que foi modificado para expor apenas as opções de política configuráveis suportadas pelo Serviço DRM da Primetime Cloud. Definir opções de política que não são suportadas pelo serviço DRM da Primetime Cloud resultará em erros de aquisição de licença. Para obter informações sobre como usar o Primetime DRM Policy Manager, consulte: [Implementações de referência do DRM Primetime: Gerenciador](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager)de políticas.

Para criar uma nova política, atualize o [!DNL flashaccesstools.properties] arquivo conforme desejado e use o comando:

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## Criar políticas dinamicamente para autenticação/autorização personalizada{#create-policies-dynamically-for-custom-auth-entitlement}

Se você estiver usando a Autenticação/autorização personalizada DRM da Primetime Cloud e quiser criar dinamicamente uma nova política DRM para cada solicitação de licença (em vez de extrair políticas de um pool pré-gerado), a Adobe recomenda que você use o SDK Java DRM Primetime diretamente. Usar o Java SDK diretamente é mais rápido do que a [!DNL AdobePolicyManager.jar] ferramenta, que exporta automaticamente o arquivo de política para o disco, incorrendo em sobrecarga de E/S de disco.

O código de amostra que usa o Java SDK pode ser encontrado no [!DNL /Primetime DRM PolicyManager/sampleCode/] diretório, nomeado [!DNL CreatePolicy.java] e [!DNL CreatePolicyWithOutputProtection.java]. Javadocs e documentação para o Java SDK podem ser encontrados em [Uma visão geral do SDK do Adobe Primetime DRM](../../../digital-rights-management/drm-sdk-overview/overview.md)

Para criar e executar as amostras, copie os arquivos .java na pasta ../libs/ e execute:

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
