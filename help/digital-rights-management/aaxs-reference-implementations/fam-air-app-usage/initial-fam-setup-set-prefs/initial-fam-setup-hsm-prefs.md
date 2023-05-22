---
title: Preferências de HSM
description: Preferências de HSM
copied-description: true
exl-id: 323f839b-fbd8-492c-a210-7651e92c7513
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Preferências de HSM {#hsm-preferences}

As preferências nesta guia só precisarão ser especificadas se a variável **[!UICONTROL Enable HSM]** estiver marcada na guia Packager. A tabela a seguir descreve essas preferências:

| Preferência | Descrição |
|---|---|
| Nome do arquivo de configuração do Sun PKCS#11 | O caminho completo para o arquivo de configuração do provedor Sun PKCS#11. Consulte o Guia de referência Java PKCS#11 no site da Sun para obter detalhes sobre o conteúdo desse arquivo de configuração. |
| Senha da Partição | A senha para a partição HSM especificada no arquivo de configuração PKCS#11. |
| Alias do Certificado do Servidor de Licença | Alias do certificado de servidor de licenças emitido por Adobe armazenado no HSM. Este certificado é usado para criptografar o CEK durante a embalagem. Especifique isto em vez de *Certificado do servidor de licenças* na guia Packager. |
| Alias do Certificado de Transporte do Servidor de Licenças | Alias do certificado de transporte do servidor emitido por Adobe armazenado no HSM. Este certificado é usado para proteger as comunicações entre o cliente e o servidor de licenças. Especifique isto em vez de *Certificado de Transporte do Servidor de Licenças* na guia Packager. |
| Alias da credencial do empacotador | Alias da credencial do empacotador emitida por Adobe (certificado e chave privada) armazenada no HSM. Isso é usado para assinar os metadados durante o empacotamento. Especifique isto em vez de *Credencial do empacotador* na guia Packager. |
| Alias da credencial do servidor de licenças | Alias da credencial do servidor de licença emitida por Adobe (certificado e chave privada) armazenada no HSM. Esta credencial é usada para assinar Listas de Atualização de Política. Especifique isto em vez de *Credencial do Servidor de Licença* na guia Lista de atualização de política. (Este alias provavelmente será o mesmo que *Alias do Certificado do Servidor de Licença*.) |
