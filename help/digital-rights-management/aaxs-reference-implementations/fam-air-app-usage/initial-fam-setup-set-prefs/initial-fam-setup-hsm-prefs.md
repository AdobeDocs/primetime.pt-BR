---
title: Preferências do HSM
description: Preferências do HSM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Preferências do HSM {#hsm-preferences}

As preferências nesta guia só precisam ser especificadas se a caixa de seleção **[!UICONTROL Enable HSM]** estiver selecionada na guia Empacotador. A tabela a seguir descreve essas preferências:

| Preferência | Descrição |
|---|---|
| Nome do arquivo de configuração PKCS#11 da Sun | O caminho completo para o arquivo de configuração do provedor Sun PKCS#11. Consulte o Guia de Referência do Java PKCS#11 no site da Sun para obter detalhes sobre o conteúdo desse arquivo de configuração. |
| Senha de Partição | A senha da partição HSM especificada no arquivo de configuração PKCS#11. |
| Alias do Certificado do Servidor de Licenças | Alias para certificado de servidor de licença emitido pelo Adobe armazenado no HSM. Este certificado é usado para criptografar o CEK durante a embalagem. Especifique isso em vez de *License Server Certificate* na guia Packager. |
| Alias do Certificado de Transporte do Servidor de Licenças | Alias do certificado de transporte de servidor emitido por Adobe armazenado no HSM. Esse certificado é usado para proteger as comunicações entre o cliente e o servidor de licenças. Especifique isso em vez de *License Server Transport Certificate* na guia Packager. |
| Alias de Credencial do Packager | Alias para credencial de empacotador emitida por Adobe (certificado e chave privada) armazenada no HSM. Isso é usado para assinar os metadados durante o empacotamento. Especifique isso em vez de *Credencial do Empacotador* na guia Empacotador. |
| Alias de Credencial do Servidor de Licenças | Alias da credencial do servidor de licença emitida pelo Adobe (certificado e chave privada) armazenada no HSM. Esta credencial é usada para assinar Listas de Atualização de Política. Especifique isso em vez de *Credencial do License Server* na guia Lista de Atualização de Política. (Esse alias provavelmente será o mesmo que *License Server Certificate Alias*.) |

