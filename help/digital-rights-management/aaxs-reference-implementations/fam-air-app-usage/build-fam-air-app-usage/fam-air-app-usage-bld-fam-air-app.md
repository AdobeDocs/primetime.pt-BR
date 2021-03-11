---
title: Criação do aplicativo AIR do Flash Access Manager
description: Criação do aplicativo AIR do Flash Access Manager
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Criação do Aplicativo AIR do Gerenciador de Flashes Access {#building-the-flash-access-manager-air-application}

Para criar o arquivo AIR do Flash Access Manager a partir do código-fonte, você precisa do SDK do Flex e do AIR instalado em sua máquina. Antes de poder empacotar e executar o aplicativo, você deve compilar o código MXML em um arquivo SWF usando o compilador [!DNL amxmlc]. O compilador [!DNL amxmlc] pode ser encontrado no diretório [!DNL bin] do Flex 4 ou SDK posterior. Se desejar, você pode definir sua variável de ambiente de caminho para incluir o diretório bin do SDK do Flex para facilitar a execução dos utilitários na linha de comando.

Use o procedimento a seguir para criar o arquivo AIR do Gerenciador de Flashes Access:

1. Abra um shell de comando ou um terminal e navegue até a pasta do projeto do aplicativo AIR do Flash Access Manager ( [!DNL UI Tools\Flash Access Manager] no diretório Implementação de referência).
1. Digite o seguinte comando:

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   Executar [!DNL amxmlc] produz [!DNL FlashAccessManager.swf], que contém o código compilado do aplicativo.

O Adobe AIR SDK inclui o utilitário AIR Developer Tool (ADT) para empacotar aplicativos do AIR e gerar certificados. As aplicações AIR devem ser assinadas digitalmente; os usuários receberão um aviso ao instalar aplicativos que não estão assinados corretamente ou que não estão assinados de forma alguma. Para gerar um certificado usando a linha de comando, abra uma janela do console na mesma pasta do aplicativo AIR e digite o seguinte:

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

Substitua *some_password* por uma senha de sua escolha. Após alguns segundos, o ADT deve concluir o processo de geração de certificados e você deve ter um novo arquivo [!DNL testCert.pfx] no diretório do aplicativo.

Em seguida, use ADT para empacotar o aplicativo em um arquivo [!DNL .air], usando o comando:

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

Este comando informa ao ADT para empacotar seu aplicativo, usando o arquivo de chave em [!DNL testCert.pfx]. Na linha acima, você configura o ADT para empacotar todo o aplicativo em um arquivo chamado [!DNL FlashAccessManager.air], e para incluir os arquivos [!DNL FlashAccessManager-app.xml] e [!DNL FlashAccessManager.swf] e as imagens do diretório de ativos.

Como parte desse processo, você será solicitado a fornecer a senha definida para o novo arquivo de certificado. Insira-o, aguarde um momento e um arquivo [!DNL FlashAccessManager.air] deve aparecer no mesmo diretório que os arquivos do projeto.
