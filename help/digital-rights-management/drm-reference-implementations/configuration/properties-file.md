---
title: Arquivo de propriedades do servidor de licenças
description: Arquivo de propriedades do servidor de licenças
copied-description: true
exl-id: 07cd9866-c29b-476e-a63f-9c5272ccd678
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Arquivo de propriedades do servidor de licenças{#license-server-properties-file}

As propriedades de referências do servidor de licenças definidas no [!DNL flashaccess-refimpl.properties] arquivo. Você pode consultar esse arquivo diretamente para obter detalhes sobre valores específicos e para obter informações de uso sobre cada propriedade. Uma amostra totalmente funcional é fornecida no [!DNL resources] diretório da implementação de referência ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`).

**Credenciais** - O arquivo de propriedades inclui configurações para o local das credenciais que o Adobe emite para você. Você pode especificar essas credenciais em um [!DNL .pfx] arquivo com uma senha ou forneça um alias e senha para uma credencial que esteja armazenada em um HSM. É necessário pelo menos configurar as propriedades relacionadas à Credencial de Transporte e à Credencial do Servidor de Licença. Especifique os locais dos arquivos de credencial relativos ao diretório especificado no `config.resourcesDirectory` propriedade.

**Flash Media Rights Management Server** - A `flashaccess-refimpl.properties` O arquivo também inclui várias propriedades relacionadas ao conteúdo do empacotamento. Essas propriedades são usadas somente para a conversão de metadados do Flash Media Rights Management Server 1.x. Depois de modificar os valores neste arquivo de propriedades, para que as alterações entrem em vigor, reinicie o servidor de licenças.
