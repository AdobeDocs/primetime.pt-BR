---
title: Notas de versão do DRM 5.3.1
seo-title: Notas de versão do DRM 5.3.1
description: As notas de versão do DRM 5.3.1 descrevem os novos recursos e os problemas conhecidos no DRM 5.3.1.
seo-description: As notas de versão do DRM 5.3.1 descrevem os novos recursos e os problemas conhecidos no DRM 5.3.1.
uuid: bb61b79f-a5b3-42ed-8016-495b1ac99ea6
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Notas de versão do DRM 5.3.1 {#drm-release-notes}

As notas de versão do DRM 5.3.1 descrevem os novos recursos e os problemas conhecidos no DRM 5.3.1.

## Novos recursos na versão 5.3 {#new-features}

* **Parada segura -** Você pode especificar se a reprodução para ou continua no final de uma janela de reprodução.
* **Proteção de Saída Baseada em Resolução (RBOP) -** Você pode especificar as restrições de saída com base nas resoluções de pixel.
* **Gating do CDM - para oferecer suporte ao HTML5, a Adobe atualizou o servidor de licença de Implementação de referência incluído no SDK Java do Adobe Primetime DRM (antigo Adobe Access DRM) para poder consumir todas as mensagens de protocolo DRM em um único terminal de URL.** Essa consolidação dos métodos de URL HTTP é necessária para atender à especificação HTML5 EME (Encrypted Media Extension), que, por sua vez, é necessária para ser implementada pelos fornecedores de DRM (Content Decryption Module, módulo de decodificação de conteúdo) do CDM. Anteriormente, estes eram os únicos pontos finais de URL expostos pelo servidor de licença de Implementação de Referência:

   * /flashaccess/i15n/v3 (Individualização)
   * /flashaccess/license/v5 (Solicitação de licença)
   * /flashaccess/licenseRet/v5 (Devolução de licença)
   * /flashaccess/getServerVersion/v5 (Obter versão do servidor)

Agora, todas as solicitações (originárias de um HTML5 CDM) podem ser direcionadas para um único terminal: /req

Essa alteração é compatível com versões anteriores de plataformas não-CDM, como Flash Player, Android e iOS.

* **Redução de RBOP -** específica para o espaço HTML5, a RBOP contém o recurso automático de redução, no qual, se uma taxa de bits que excede a taxa de bits permitida especificada na política de DRM, o conteúdo será reduzido para a resolução máxima permitida. Por exemplo, se um fluxo de 1080p for transmitido para um cliente que esteja exibindo o conteúdo em um monitor não compatível com HDCP, a política de DRM pode indicar que a resolução máxima deve ser 720p. O Primetime DRM decodificará o fluxo de 1080p e o reduzirá para 720p antes de renderizá-lo na tela. Se o navegador reproduzindo o vídeo for arrastado para um monitor que não suporta HDCP, o Primetime DRM parará de baixar o conteúdo e permitirá que ele seja reproduzido no 1080.

## Problemas conhecidos na versão 5.3 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` gera mensagens de log para `flashaccess-global.log.`Você deve garantir que o `flashaccess-global.log` arquivo esteja no mesmo diretório com Hasher.bat.

* A saída de algumas das `toJSON()`chamadas retorna `Strings` que não estão totalmente em conformidade com o JSON ou estão totalmente em conformidade de forma independente (ou seja, sem a composição das estruturas JSON).

* O servidor de chave Xbox aceita solicitações de chave que têm o valor da versão igual a 1.

O servidor de chaves Xbox deve suportar apenas solicitações de chave com a versão igual a 1, mas, no momento, o servidor aceita solicitações de chave nas quais a versão não é 1.

* O servidor de chave Xbox não valida uma política corretamente.

O servidor de chaves Xbox não deve aceitar políticas que estejam fora da data de validade, mas que atualmente o servidor as aceita independentemente.

* O servidor de chaves Xbox deve rejeitar uma solicitação de chave que contenha metadados criados com um certificado do empacotador incorreto.
* O valor retornado de algumas estruturas JSON não está formatado corretamente para classes relacionadas à Proteção de Saída com base em Resolução.

Várias classes implementam um método toJSON() que deve retornar uma representação compatível com JSON desse objeto como uma String, mas no momento o valor retornado não é totalmente compatível com JSON.

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página Aprendizagem e suporte [do](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.
