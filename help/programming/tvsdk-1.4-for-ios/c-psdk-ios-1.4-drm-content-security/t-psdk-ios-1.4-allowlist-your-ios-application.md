---
description: Você pode lista de permissões seus aplicativos iOS usando a ferramenta Adobe machotools.
title: Lista de permissões seu aplicativo iOS
exl-id: ff647647-6c5f-4a10-9040-8600f6103b99
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Lista de permissões seu aplicativo iOS {#allowlist-your-ios-application}

Você pode lista de permissões seus aplicativos iOS usando a ferramenta Adobe machotools.

Geralmente, ao concluir um aplicativo TVSDK, você pode usar as ferramentas de linha de comando do Adobe Primetime DRM para lista de permissões seu aplicativo.

>[!TIP]
>
>Você também pode usar essas ferramentas para criar políticas de DRM e criptografar conteúdo.

Permitir a listagem do seu aplicativo garante que o conteúdo protegido só possa ser reproduzido no player de vídeo. No entanto, para permitir a listagem de um aplicativo do iOS, é necessário concluir um procedimento especial que funcione com as políticas de envio de aplicativos do Apple.

Antes de enviar um aplicativo do iOS, é necessário assiná-lo e publicá-lo no Apple.

>[!NOTE]
>
>A Apple desmonta a assinatura do desenvolvedor e assina novamente o aplicativo com seu próprio certificado.

Devido à nova assinatura, as informações de lista de permissões geradas antes de você enviar para o Apple App Store não podem ser usadas.

Para trabalhar com essa política de envio, o Adobe criou um `machotools` ferramenta que fará a impressão digital do aplicativo iOS para criar um valor de resumo, assinar esse valor e inserir esse valor no aplicativo do iOS. Depois de criar a impressão digital do aplicativo iOS, envie o aplicativo para o Apple App Store. Quando um usuário executa seu aplicativo da App Store, o Primetime DRM faz um cálculo de tempo de execução da impressão digital do aplicativo e a confirma com o valor de resumo inserido anteriormente no aplicativo. Se a impressão digital for correspondente, o aplicativo será confirmado como incluído na lista de permissões e o conteúdo protegido terá permissão para ser reproduzido.

O ADOBE `machotools` ferramenta está incluída no SDK TVSDK do iOS, no [!DNL [..]pasta /tools/DRM].

Para usar `machotools`:

1. Gere um par de chaves.

   Para usar um utilitário como OpenSSL, abra uma janela de comando e digite o seguinte:

   ```shell
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. Quando solicitado, insira uma senha para proteger a chave privada.

   As senhas devem conter pelo menos 12 caracteres e os caracteres devem incluir uma mistura de caracteres ASCII maiúsculos e minúsculos e números.
1. Para usar o OpenSSL para gerar uma senha forte para você, abra uma janela de comando e digite o seguinte:

   ```shell
   openssl rand -base64 8
   ```

1. Gerar uma solicitação de assinatura de certificado (CSR).

   Para usar o OpenSSL para gerar uma CSR, abra uma Janela de Comando e insira o seguinte:

   ```shell
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. Assine o certificado automaticamente e insira qualquer duração.

   O exemplo a seguir fornece uma expiração de 20 anos:

   ```shell
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. Converta o certificado autoassinado em um arquivo PKCS#12:

   ```shell
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   Você pode usar o certificado autoassinado para assinar seu aplicativo iOS.

1. Atualize o local do arquivo PFX e a senha.
1. Antes de criar seu aplicativo no Xcode, acesse  **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** e adicione o seguinte comando ao script de execução:

   ```shell
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. Executar [!DNL machotools] para gerar o valor de hash da ID do editor do aplicativo.

   ```shell
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. Crie uma nova Política DRM ou atualize a política existente para incluir o valor de hash da ID do editor retornada.
1. Usar o [!DNL AdobePolicyManager.jar], crie uma nova Política DRM (atualize sua política existente) para incluir o valor de hash da ID do editor retornada, uma ID do aplicativo opcional e os atributos de versão mín. e máx. na [!DNL flashaccess-tools.properties] arquivo.

   ```shell
   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. Crie o pacote do conteúdo usando a nova política DRM e confirme a reprodução do conteúdo listado com permissão no aplicativo iOS.
