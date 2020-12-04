---
seo-title: Preferências do Packager
title: Preferências do Packager
uuid: 3e9c971d-3a5f-4f3e-97e7-baab63b1f67f
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Preferências do Packager {#packager-preferences}

Esta guia contém as configurações necessárias para o conteúdo do empacotamento. A tabela a seguir descreve essas preferências:

| Preferência | Descrição |
|--- |--- |
| Certificado de Transporte do Servidor de Licenças | O certificado de transporte do servidor, emitido pela Adobe. Este certificado é usado para proteger as comunicações entre o cliente e o servidor de licenças. O arquivo deve estar localizado no Diretório de Recursos. |
| Habilitar HSM | Especifica se os certificados e as credenciais são armazenados em um HSM. Em caso afirmativo, as preferências relacionadas aos certificados e credenciais serão desativadas e as propriedades na guia HSM deverão ser especificadas. |
| Opções de criptografia de chave | Especifica como a Chave de criptografia de conteúdo é criptografada no momento do empacotamento |
| Certificado do servidor de licença | O Certificado de Servidor de Licença, emitido pela Adobe. O arquivo deve estar localizado no Diretório de Recursos. O CEK é criptografado com a chave pública do servidor de licenças. Só os titulares da chave privada do servidor de licenças podem desencriptar o CEK. |
| Credencial do Packager | A credencial do empacotador, emitida pela Adobe. Esse arquivo é usado para assinar os metadados durante o empacotamento. |
| Nome do arquivo | O arquivo `PKCS#12` ( .pfx) contendo certificado e chave privada. O arquivo deve estar localizado no Diretório de Recursos. |
| Senha do arquivo | Senha para o arquivo .pfx |
| Propriedades da pasta assistida global | Especifica configurações comuns a todas as Pastas monitoradas configuradas neste servidor. |
| Verificar intervalo em milissegundos | Especifica com que frequência as Pastas monitoradas devem verificar se há novo conteúdo no pacote. O servidor repete todas as Pastas monitoradas configuradas e dorme por esse tempo. |
| Sufixo do nome do arquivo de saída | Especifica uma extensão de arquivo para adicionar aos arquivos de saída. Por exemplo, se .out for especificado e o arquivo de entrada for video.flv, o arquivo de saída será video.out.flv. |
| Arquivos de Entrada de Backup | Especifica se uma cópia do conteúdo original deve ser salva. Se essa opção não estiver selecionada, o arquivo original será excluído depois que o empacotamento for concluído com êxito. |
| Nome da subpasta de backup de entrada | Se a opção Backup Input Files estiver selecionada, especifica uma pasta na qual os arquivos de entrada serão salvos. Essa opção especifica um nome de pasta relativo ao diretório de entrada Pasta assistida. Se a pasta não existir, ela será criada durante o empacotamento. |
| Substituir arquivos de saída existentes | Especifica se o arquivo de saída pode ser substituído se já existir um arquivo com o mesmo nome. Se essa opção não for selecionada e o arquivo de saída já existir, o processamento do arquivo de entrada será ignorado. |
