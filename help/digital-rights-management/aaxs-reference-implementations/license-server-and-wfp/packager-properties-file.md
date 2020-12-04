---
seo-title: Arquivo de propriedades do Packager
title: Arquivo de propriedades do Packager
uuid: 156624ec-66f0-4718-8a66-ed04a47f234d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Arquivo de propriedades do Packager {#packager-properties-file}

Use o arquivo [!DNL flashaccess-refimpl-packager.properties] para configurar o componente de Packager da pasta monitorada da implementação de referência. No mínimo, certifique-se de definir o URL do servidor de licenças, o certificado do servidor de licenças, as credenciais do empacotador e as opções de proteção de chave. Esse arquivo também contém o local de cada pasta assistida (packager.watchfolder.source. `n`). Quaisquer alterações feitas nos valores neste arquivo de propriedade entrarão em vigor na próxima vez que o empacotador de pastas monitorado for executado (a reinicialização do servidor não é necessária). No entanto, se houver um erro de configuração no empacotador, o thread do empacotador de pastas monitorado será encerrado e o servidor precisará ser reiniciado para reiniciar o encadeamento do empacotador.
