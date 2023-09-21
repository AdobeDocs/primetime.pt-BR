---
title: Notas de versão do DRM 5.3.1
description: As Notas de versão do DRM 5.3.1 descrevem os novos recursos e os problemas conhecidos no DRM 5.3.1.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Notas de versão do DRM 5.3.1 {#drm-release-notes}

As Notas de versão do DRM 5.3.1 descrevem os novos recursos e os problemas conhecidos no DRM 5.3.1.

## Novos recursos na versão 5.3 {#new-features}

* **Interrupção segura -** Você pode especificar se a reprodução pára ou continua no final de uma janela de reprodução.
* **Proteção de saída com base em resolução (RBOP) -** Você pode especificar as restrições de saída com base nas resoluções de pixel.
* **Classificação do CDM -** Para oferecer suporte ao HTML5, o Adobe atualizou o servidor de licença da Implementação de referência incluído no SDK Java do Adobe Primetime DRM (antigo Adobe Access DRM) para poder consumir todas as mensagens do protocolo DRM em um único endpoint de URL. Essa consolidação de métodos de URL HTTP é necessária para estar em conformidade com a especificação HTML5 EME (Encrypted Media Extension) que, por sua vez, deve ser implementada pelos fornecedores de DRM (Content Decryption Module, Módulo de Descriptografia de Conteúdo) do CDM. Anteriormente, esses eram os únicos endpoints de URL expostos pelo servidor de licenças da Implementação de referência:

   * /flashaccess/i15n/v3 (Individualização)
   * /flashaccess/license/v5 (Solicitação de licença)
   * /flashaccess/licenseRet/v5 (Retorno de licença)
   * /flashaccess/getServerVersion/v5 (Obter Versão do Servidor)

Agora, todas as solicitações (originadas de um CDM HTML5) podem ser direcionadas a um único endpoint: /req

Essa alteração é compatível com versões anteriores de plataformas que não são CDM, como Flash Player, Android, iOS.

* **Redução de RBOP -** Específico do espaço HTML5, o RBOP contém o recurso de rebaixamento automático, em que, se uma taxa de bits que exceder a taxa de bits permitida especificada na política DRM, o conteúdo será rebaixado para a resolução máxima permitida. Por exemplo, se um fluxo de 1080p for transmitido para um cliente que está exibindo o conteúdo em um monitor não compatível com HDCP, a política DRM pode indicar que a resolução máxima deve ser de 720p. O Primetime DRM decodificará o fluxo de 1080p e o diminuirá para 720p antes de renderizá-lo na tela. Se o navegador que está reproduzindo o vídeo for arrastado para um monitor compatível com HDCP, o Primetime DRM parará de reduzir o conteúdo e permitirá que ele seja reproduzido a 1080.

## Problemas conhecidos na versão 5.3 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` gera mensagens de log para `flashaccess-global.log.`Você deve garantir que a variável `flashaccess-global.log` O arquivo está no mesmo diretório que Hasher.bat.

* A saída de alguns dos `toJSON()`chamadas retornam `Strings` que não são totalmente compatíveis com JSON ou totalmente compatíveis de maneira independente (ou seja, sem a composição de estruturas JSON).

* O servidor de chaves do Xbox aceita solicitações de chaves com valor de versão diferente de 1.

O servidor de chaves do Xbox só deve aceitar solicitações de chaves cuja versão seja igual a 1, mas, no momento, o servidor aceita solicitações de chaves cuja versão não seja 1.

* O servidor de chaves Xbox não valida uma política corretamente.

O servidor de chaves do Xbox não deve aceitar políticas que estejam fora da data de validade, mas que, atualmente, o servidor as aceita independentemente.

* O servidor de chaves do Xbox deve rejeitar uma solicitação de chave que contenha metadados criados com um certificado de empacotador incorreto.
* O valor retornado de algumas estruturas JSON não está formatado corretamente para as classes relacionadas à Proteção de Saída baseada em Resolução.

Várias classes implementam um método toJSON() que deve retornar uma representação compatível com JSON desse objeto como uma String, mas atualmente o valor retornado não é totalmente compatível com JSON.

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
