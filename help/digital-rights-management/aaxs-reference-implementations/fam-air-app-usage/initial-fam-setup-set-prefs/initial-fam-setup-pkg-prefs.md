---
title: Preferências do empacotador
description: Preferências do empacotador
copied-description: true
exl-id: 43e49372-a875-413a-ba27-25e3ce5c64c4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Preferências do empacotador {#packager-preferences}

Esta guia contém as configurações necessárias para o conteúdo do pacote. A tabela a seguir descreve essas preferências:

| Preferência | Descrição |
|--- |--- |
| Certificado de Transporte do Servidor de Licenças | O certificado de transporte do servidor, emitido pelo Adobe. Este certificado é usado para proteger as comunicações entre o cliente e o servidor de licenças. O arquivo deve estar localizado no Diretório de recursos. |
| Habilitar HSM | Especifica se certificados e credenciais são armazenados em um HSM. Nesse caso, as preferências relacionadas aos certificados e credenciais serão desativadas e as propriedades na guia HSM deverão ser especificadas. |
| Opções de Criptografia de Chave | Especifica como a Chave de Criptografia de Conteúdo é criptografada no momento do empacotamento |
| Certificado do servidor de licenças | O Certificado de Servidor de Licença, emitido pelo Adobe. O arquivo deve estar localizado no Diretório de recursos. O CEK é criptografado com a chave pública do servidor de licenças. Somente os titulares da chave privada do servidor de licenças podem descriptografar o CEK. |
| Credencial do empacotador | A credencial do empacotador, emitida pelo Adobe. Esse arquivo é usado para assinar os metadados durante o empacotamento. |
| Nome do arquivo | A variável `PKCS#12` ( .pfx) arquivo contendo certificado e chave privada. O arquivo deve estar localizado no Diretório de recursos. |
| Senha do arquivo | Senha para o arquivo .pfx |
| Propriedades globais da pasta monitorada | Especifica as configurações comuns a todas as Pastas monitoradas configuradas neste servidor. |
| Intervalo de verificação em milissegundos | Especifica a frequência com que as Pastas monitoradas devem verificar se há novo conteúdo para o pacote. O servidor repete todas as Pastas monitoradas configuradas e, em seguida, fica suspenso por esse tempo. |
| Sufixo do nome do arquivo de saída | Especifica uma extensão de arquivo para adicionar aos arquivos de saída. Por exemplo, se .out for especificado e o arquivo de entrada for video.flv, o arquivo de saída será video.out.flv. |
| Arquivos de entrada de backup | Especifica se uma cópia do conteúdo original deve ser salva. Se esta opção não estiver selecionada, o arquivo original será excluído depois que o empacotamento for concluído com sucesso. |
| Nome da Subpasta do Backup de Entrada | Se a opção Fazer backup dos arquivos de entrada estiver selecionada, especifica a pasta onde os arquivos de entrada serão salvos. Esta opção especifica um nome de pasta relativo ao diretório de entrada Pasta monitorada. Se a pasta não existir, ela será criada durante a compactação. |
| Substituir arquivos de saída existentes | Especifica se o arquivo de saída poderá ser substituído se já existir um arquivo com o mesmo nome. Se esta opção não estiver selecionada e o arquivo de saída já existir, o processamento do arquivo de entrada será ignorado. |
