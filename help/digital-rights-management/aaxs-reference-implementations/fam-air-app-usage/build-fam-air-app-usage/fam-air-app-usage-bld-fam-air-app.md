---
title: Criação do aplicativo AIR do Flash Access Manager
description: Criação do aplicativo AIR do Flash Access Manager
copied-description: true
exl-id: f15fe9d2-d5e8-43ef-a1d5-1211752d54da
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Criação do aplicativo AIR do Flash Access Manager {#building-the-flash-access-manager-air-application}

Para criar o arquivo AIR do Flash Access Manager a partir do código-fonte, é necessário ter o SDK do Flex e do AIR instalado no computador. Antes de empacotar e executar o aplicativo, é necessário compilar o código do MXML em um arquivo SWF usando o [!DNL amxmlc] compilador. A variável [!DNL amxmlc] o compilador pode ser encontrado no [!DNL bin] diretório do SDK do Flex 4 ou posterior. Se desejar, você pode definir a variável de ambiente path para incluir o diretório bin do SDK da Flex para facilitar a execução dos utilitários na linha de comando.

Use o procedimento a seguir para criar o arquivo AIR do Flash Access Manager:

1. Abra um shell de comando ou um terminal e navegue até a pasta do projeto do aplicativo AIR do Flash Access Manager ( [!DNL UI Tools\Flash Access Manager] no diretório Reference Implementation ).
1. Digite o seguinte comando:

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   Executando [!DNL amxmlc] produz [!DNL FlashAccessManager.swf], que contém o código compilado do aplicativo.

O SDK do Adobe AIR inclui o utilitário ADT (AIR Developer Tool) para empacotar aplicativos AIR e gerar certificados. Os aplicativos do AIR devem ser assinados digitalmente; os usuários receberão um aviso ao instalar aplicativos que não são assinados corretamente ou que não são assinados. Para gerar um certificado usando a linha de comando, abra uma janela de console na mesma pasta do aplicativo AIR e digite o seguinte:

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

Substituto *some_password* com uma senha de sua escolha. Após alguns segundos, o ADT deve concluir o processo de geração de certificados e você deve ter um novo [!DNL testCert.pfx] no diretório do aplicativo.

Em seguida, use o ADT para empacotar o aplicativo em um [!DNL .air] usando o comando:

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

Este comando informa ao ADT para empacotar seu aplicativo, usando o arquivo de chave em [!DNL testCert.pfx]. Na linha acima, configure o ADT para empacotar todo o aplicativo em um arquivo chamado [!DNL FlashAccessManager.air]e para incluir os arquivos [!DNL FlashAccessManager-app.xml] e [!DNL FlashAccessManager.swf] e as imagens do diretório de ativos.

Como parte desse processo, você será solicitado a fornecer a senha definida para o novo arquivo de certificado. Insira-o, aguarde um momento e [!DNL FlashAccessManager.air] O arquivo deve aparecer no mesmo diretório dos arquivos do projeto.
