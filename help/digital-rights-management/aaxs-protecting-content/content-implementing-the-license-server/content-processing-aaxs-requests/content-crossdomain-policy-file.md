---
seo-title: Arquivo de política entre domínios
title: Arquivo de política entre domínios
uuid: fc05aa5e-6fbd-445f-a22a-f795d5a0b3ad
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Arquivo de política entre domínios {#crossdomain-policy-file}

Se o servidor de licença estiver hospedado em um domínio diferente do SWF de reprodução de vídeo, um arquivo de política entre domínios (crossdomain.xml) será necessário para permitir que o SWF solicite licenças do servidor de licença. Um arquivo de política entre domínios é um arquivo XML que fornece uma maneira para o servidor indicar que seus dados e documentos estão disponíveis para arquivos SWF fornecidos de outros domínios. Qualquer arquivo SWF servido de um domínio especificado no arquivo de política entre domínios do servidor de licenças tem permissão para acessar dados ou ativos desse servidor de licenças.

A Adobe recomenda que os desenvolvedores sigam as práticas recomendadas ao implantar o arquivo de política entre domínios, permitindo apenas que domínios confiáveis acessem o servidor de licenças e limitando o acesso ao subdiretório de licenças no servidor da Web.

Para obter mais informações sobre arquivos de política entre domínios, consulte os seguintes locais:

* Controles de site (arquivos de política)
* Especificação do arquivo de política entre domínios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

