---
seo-title: Preferências de HSM
title: Preferências de HSM
uuid: 1b97d582-d4b6-48cd-9c24-2d13493571e9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Preferências de HSM {#hsm-preferences}

As preferências nesta guia só precisam ser especificadas se a **[!UICONTROL Enable HSM]** caixa de seleção estiver selecionada na guia Packager. A tabela a seguir descreve essas preferências:

| Preferência | Descrição |
|---|---|
| Nome do arquivo de configuração Sun PKCS#11 | O caminho completo para o arquivo de configuração do provedor Sun PKCS#11. Consulte o Guia de referência do Java PKCS#11 no site da Sun para obter detalhes sobre o conteúdo desse arquivo de configuração. |
| Senha da partição | A senha da partição HSM especificada no arquivo de configuração PKCS#11. |
| Alias do Certificado do Servidor de Licenças | Alias para certificado de servidor de licença emitido pela Adobe armazenado em HSM. Este certificado é usado para criptografar o CEK durante a embalagem. Especifique isso em vez do Certificado *do servidor de* licença na guia Packager. |
| Alias do Certificado de Transporte do Servidor de Licenças | Alias para o certificado de transporte de servidor emitido pela Adobe armazenado em HSM. Este certificado é usado para proteger as comunicações entre o cliente e o servidor de licenças. Especifique isso em vez do Certificado *de Transporte do* License Server na guia Packager. |
| Alias de Credencial do Packager | Alias para credenciais de empacotador emitidas pela Adobe (certificado e chave privada) armazenadas no HSM. Isso é usado para assinar os metadados durante o empacotamento. Especifique isso em vez da Credencial *do* Packager na guia Packager. |
| Alias de Credencial do Servidor de Licenças | Alias para credenciais de servidor de licença emitidas pela Adobe (certificado e chave privada) armazenadas no HSM. Esta credencial é usada para assinar Listas de Atualização de Política. Especifique isso em vez da Credencial ** do License Server na guia Lista de atualizações de política. (Esse alias será provavelmente o mesmo que o Alias *do Certificado do Servidor de* Licenças.) |

