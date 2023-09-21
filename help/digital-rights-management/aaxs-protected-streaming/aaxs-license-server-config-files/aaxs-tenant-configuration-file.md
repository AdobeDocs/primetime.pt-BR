---
title: Arquivo de configuração do inquilino
description: Arquivo de configuração do inquilino
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---

# Arquivo de configuração do inquilino {#tenant-configuration-file}

O arquivo de configuração flashaccess-tenant.xml contém definições que se aplicam a um locatário específico do servidor de licenças. Cada locatário tem sua própria instância desse arquivo de configuração localizada em *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*. Consulte a [!DNL configs/flashaccessserver/tenants/sampletenant] diretório para um exemplo de arquivo de configuração de locatário.

Você pode especificar todos os caminhos de arquivo no arquivo de configuração do locatário como caminhos absolutos ou caminhos relativos ao diretório de configuração do locatário (*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*).

O arquivo de configuração do locatário inclui:

* **Credencial de transporte** — Especifica uma ou mais credenciais de transporte (certificado e chave privada) emitidas pelo Adobe. Pode ser especificado como um caminho para um arquivo .pfx e uma senha ou um alias para uma credencial armazenada em um HSM. Várias dessas credenciais podem ser especificadas aqui, como caminhos de arquivo, aliases de chave ou ambos. Consulte &quot;[Lidar com atualizações de certificado](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-cert-updates.md)&quot; em *Utilização do SDK do Adobe Access para proteção de conteúdo* para obter mais informações sobre quando credenciais adicionais são necessárias.
* **Credencial do Servidor de Licença** — Especifica uma ou mais credenciais de servidor de licença (certificado e chave privada) emitidas pelo Adobe. Pode ser especificado como um caminho para um arquivo .pfx e uma senha ou um alias para uma credencial armazenada em um HSM. Várias dessas credenciais podem ser especificadas aqui, como caminhos de arquivo, aliases de chave ou ambos. Consulte Manipular atualizações de certificado em *Usar o SDK de acesso do Adobe para proteção de conteúdo *para obter mais informações sobre quando credenciais adicionais são necessárias.
* **Certificados-chave do servidor** — Facultativo. Especifica o certificado de Servidor de Licenças do Servidor de Chaves emitido por Adobe. Pode ser especificado como um caminho para um arquivo .cer ou um alias para um certificado armazenado em um HSM. Essa opção deve ser especificada para emitir licenças para conteúdo empacotado com uma política que requer entrega remota de chaves para dispositivos iOS.
* **Autorizadores personalizados** — Facultativo. Especifica as classes de autorizador personalizadas a serem invocadas para cada solicitação de licença. Se vários autorizadores forem especificados, eles serão chamados na ordem listada. Para obter mais informações, consulte &quot;[Extensões de autorização personalizadas](../../aaxs-protected-streaming/custom-authorization-extensions.md)&quot;.
* **Lista de acondicionadores autorizados** — Facultativo. Especifica certificados que identificam entidades autorizadas a empacotar conteúdo para este servidor de licenças. Se nenhum certificado de empacotador for especificado, o servidor emitirá licenças para o conteúdo empacotado por qualquer empacotador.
* **Versão mínima do cliente com suporte** (Consulte *Utilização do SDK do Adobe Access para proteção de conteúdo*).
* **Regras de uso**

   * **Licença de cache** — Facultativo. Especifica por quanto tempo a licença pode ser armazenada no cliente. Por padrão, o armazenamento em cache de licenças está desativado. Para permitir o armazenamento em cache de licenças por um período limitado, defina a data final ou o número de segundos para os quais a licença deve ser armazenada (começando quando a licença é emitida). Definir o número de segundos como 0 desativa o cache de licenças.

     Observe que todas as licenças emitidas pelo servidor para transmissão protegida têm um período de expiração de 24 horas (86.400 segundos). Portanto, esse valor se aplica implicitamente como um limite superior a qualquer data final ou duração definida para o armazenamento em cache de licença, com um valor máximo de 86.400 segundos, mesmo que o esquema imponha limites mais altos.

   * **Reproduzir à direita** — Pelo menos um direito deve ser especificado. Se vários direitos forem especificados, o cliente usará o primeiro direito para o qual ele atender a todos os requisitos.

      * **Proteção de saída** — Controla se a saída para dispositivos de renderização externos deve ser protegida.
      * **Restrições a aplicativos AIR e SWF** — lista de permissões opcional de aplicativos SWF e AIR que possam reproduzir o conteúdo (ou seja, somente os aplicativos especificados são permitidos). Os aplicativos SWF são identificados por um URL ou pelo resumo do SWF e pelo tempo máximo para permitir o download e a verificação do resumo. Para obter informações sobre como calcular o resumo de SWF, consulte a seção &quot;Calculadora de hash de SWF&quot;. Os aplicativos do AIR e do iOS são identificados por uma ID do editor e uma ID do aplicativo opcional, a versão mínima e a versão máxima. Se nenhuma restrição de aplicativo for especificada, qualquer aplicativo SWF ou AIR poderá reproduzir o conteúdo.
      * **Restrições de DRM e Módulo de Tempo de Execução** — Especifica o nível de segurança mínimo necessário para o módulo DRM/Runtime. Opcionalmente, inclui uma lista de bloqueios de versões que não têm permissão para reproduzir o conteúdo. As versões de módulo são identificadas por atributos como sistema operacional e/ou um número de versão. Restrições do Módulo DRM e Restrições do Módulo de Tempo de Execução agora oferecem suporte aos seguintes atributos adicionais:

         * `oemVendor`
         * `model`
         * `screenType`

        Os seguintes atributos agora são opcionais:

         * `osVersion`
         * `version`

      * **Requisitos de capacidade do dispositivo** — especifica opcionalmente os recursos de hardware necessários para acessar o conteúdo.
      * **Requisitos de detecção de jailbreak** — Especifica opcionalmente que a reprodução não é permitida em dispositivos nos quais o jailbreak é detectado.

Consulte os comentários no arquivo de configuração de locatário de exemplo para obter mais detalhes.
