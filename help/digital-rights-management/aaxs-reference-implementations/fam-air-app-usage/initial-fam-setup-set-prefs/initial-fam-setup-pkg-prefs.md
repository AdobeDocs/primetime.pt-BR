---
title: Preferências do pacote
description: Preferências do pacote
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Preferências do pacote {#packager-preferences}

Esta guia contém as configurações necessárias para o conteúdo do empacotamento. A tabela a seguir descreve essas preferências:

| Preferência | Descrição |
|--- |--- |
| Certificado de Transporte do Servidor de Licenças | O certificado de transporte do servidor, emitido pelo Adobe. Esse certificado é usado para proteger as comunicações entre o cliente e o servidor de licenças. O arquivo deve estar localizado no Diretório de Recursos. |
| Ativar HSM | Especifica se certificados e credenciais são armazenados em um HSM. Nesse caso, as preferências relacionadas aos certificados e credenciais serão desativadas e as propriedades na guia HSM deverão ser especificadas. |
| Opções de criptografia de chave | Especifica como a chave de criptografia de conteúdo é criptografada no momento do empacotamento |
| Certificado do Servidor de Licenças | O Certificado do Servidor de Licenças, emitido pelo Adobe. O arquivo deve estar localizado no Diretório de Recursos. O CEK é criptografado com a chave pública do servidor de licenças. Apenas os titulares da chave privada do servidor de licenças podem desencriptar o CEK. |
| Credencial do Packager | A credencial do empacotador, emitida pelo Adobe. Esse arquivo é usado para assinar os metadados durante o empacotamento. |
| Nome do arquivo | O arquivo `PKCS#12` ( .pfx) contendo certificado e chave privada. O arquivo deve estar localizado no Diretório de Recursos. |
| Senha do arquivo | Senha do arquivo .pfx |
| Propriedades da pasta assistida global | Especifica configurações comuns a todas as Pastas vigiadas configuradas neste servidor. |
| Verificar Intervalo em Milissegundos | Especifica a frequência com que as Pastas vigiadas devem verificar o novo conteúdo no pacote. O servidor repete todas as Pastas vigiadas configuradas e, em seguida, dorme por esse tempo. |
| Sufixo do nome do arquivo de saída | Especifica uma extensão de arquivo para adicionar a arquivos de saída. Por exemplo, se .out for especificado e o arquivo de entrada for video.flv, o arquivo de saída será video.out.flv. |
| Arquivos de entrada de backup | Especifica se uma cópia do conteúdo original deve ser salva. Se esta opção não estiver selecionada, o arquivo original será excluído após a conclusão bem-sucedida do empacotamento. |
| Nome da Subpasta de Backup de Entrada | Se a opção Arquivos de Entrada de Backup estiver selecionada, especifica uma pasta onde os arquivos de entrada serão salvos. Essa opção especifica um nome de pasta relativo ao diretório de entrada Pasta assistida. Se a pasta não existir, ela será criada durante o empacotamento. |
| Substituir arquivos de saída existentes | Especifica se o arquivo de saída pode ser substituído se um arquivo já existir com o mesmo nome. Se essa opção não estiver selecionada e o arquivo de saída já existir, o processamento do arquivo de entrada será ignorado. |
