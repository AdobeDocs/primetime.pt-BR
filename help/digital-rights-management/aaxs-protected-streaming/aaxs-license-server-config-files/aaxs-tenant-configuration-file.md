---
title: Arquivo de configuração do locatário
description: Arquivo de configuração do locatário
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---


# Arquivo de configuração de locatário {#tenant-configuration-file}

O arquivo de configuração flashaccess-tenant.xml contém configurações que se aplicam a um locatário específico do servidor de licenças. Cada locatário tem sua própria instância desse arquivo de configuração localizado em *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*. Consulte o diretório [!DNL configs/flashaccessserver/tenants/sampletenant] para obter um exemplo de arquivo de configuração de locatário.

Você pode especificar todos os caminhos de arquivo no arquivo de configuração do locatário como caminhos absolutos ou caminhos relativos para o diretório de configuração do locatário (*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*).

O arquivo de configuração do locatário inclui:

* **Credencial de Transporte**  — Especifica uma ou mais credenciais de transporte (certificado e chave privada) emitidas pelo Adobe. Pode ser especificado como um caminho para um arquivo .pfx e uma senha, ou um alias para uma credencial armazenada em um HSM. Várias dessas credenciais podem ser especificadas aqui, como caminhos de arquivo, aliases de chave ou ambos. Consulte &quot;[Manipular atualizações de certificado](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-cert-updates.md)&quot; em *Usar o SDK de acesso do Adobe para proteger conteúdo* para obter mais informações sobre quando credenciais adicionais são necessárias.
* **Credencial do License Server**  — Especifica uma ou mais credenciais do servidor de licenças (certificado e chave privada) emitidas pelo Adobe. Pode ser especificado como um caminho para um arquivo .pfx e uma senha, ou um alias para uma credencial armazenada em um HSM. Várias dessas credenciais podem ser especificadas aqui, como caminhos de arquivo, aliases de chave ou ambos. Consulte Manuseio de atualizações de certificado em *Uso do SDK de acesso do Adobe para proteção de conteúdo *para obter mais informações sobre quando credenciais adicionais são necessárias.
* **Certificados**  do Servidor de Chave— Opcional. Especifica o certificado do Servidor de Licenças do Servidor de Chave emitido pelo Adobe. Pode ser especificado como um caminho para um arquivo .cer ou alias para um certificado armazenado em um HSM. Essa opção deve ser especificada para emitir licenças para conteúdo empacotado com uma política que requer a entrega remota de chaves para dispositivos iOS.
* **Autorizadores personalizados** — Opcional. Especifica classes de autorizador personalizadas a serem chamadas para cada solicitação de licença. Se vários autorizadores forem especificados, eles serão chamados na ordem listada. Para obter mais informações, consulte &quot;[Extensões de autorização personalizadas](../../aaxs-protected-streaming/custom-authorization-extensions.md)&quot;.
* **Lista de pacotes autorizados** — opcional. Especifica certificados que identificam entidades autorizadas a empacotar conteúdo para este servidor de licenças. Se nenhum certificado do empacotador for especificado, o servidor emitirá licenças para o conteúdo empacotado por qualquer empacotador.
* **Versão mínima compatível do cliente**  (Consulte  *Uso do SDK de acesso do Adobe para proteção de conteúdo*).
* **Regras de uso**

   * **Cache de Licenças** — Opcional. Especifica por quanto tempo a licença pode ser armazenada no cliente. Por padrão, o armazenamento em cache de licenças está desativado. Para permitir o armazenamento em cache de licenças por um período limitado, fixar a data de término ou o número de segundos durante os quais a licença deve ser armazenada (a partir do momento em que a licença é emitida). Definir o número de segundos como 0 desativa o armazenamento em cache de licenças.

      Observe que todas as licenças emitidas pelo Servidor para transmissão protegida têm um período de expiração de 24 horas (86400 segundos). Portanto, esse valor se aplica implicitamente como um limite superior para qualquer data final ou duração definida para o armazenamento em cache de licenças, também com um valor máximo de 86400 segundos, mesmo que o schema imponha limites mais altos.

   * **Play Right** — Deve ser especificado pelo menos um direito. Se vários direitos forem especificados, o cliente usará o primeiro direito para o qual atenderá a todos os requisitos.

      * **Proteção de saída**  — Controla se a saída para dispositivos de renderização externos deve ser protegida.
      * **Restrições**  de Aplicação AIR e SWF — lista de permissões opcional de aplicações SWF e AIR que possam reproduzir o conteúdo (ou seja, apenas são permitidas as aplicações especificadas). As aplicações SWF são identificadas por um URL ou pelo resumo do SWF e o tempo máximo para permitir o download e a verificação do resumo. Para obter informações sobre o cálculo do resumo SWF, consulte a seção &quot;Calculadora de Hash SWF&quot;. Os aplicativos AIR e iOS são identificados por uma ID do editor e uma ID de aplicativo opcional, versão mínima e versão máxima. Se nenhuma restrição de aplicativo for especificada, qualquer aplicativo SWF ou AIR poderá reproduzir o conteúdo.
      * **DRM e restrições do módulo de tempo de execução**  — Especifica o nível mínimo de segurança necessário para o módulo DRM/Tempo de execução. Opcionalmente inclui uma lista de bloqueios de versões que não têm permissão para reproduzir o conteúdo. As versões do módulo são identificadas por atributos como sistema operacional e/ou um número de versão. Restrições do módulo DRM e restrições do módulo de tempo de execução agora oferecem suporte aos seguintes atributos adicionais:

         * `oemVendor`
         * `model`
         * `screenType`

         Os seguintes atributos agora são opcionais:

         * `osVersion`
         * `version`
      * **Requisitos de capacidade do dispositivo**  — especifica opcionalmente os recursos de hardware necessários para acessar o conteúdo.
      * **Requisitos**  de detecção de quebra de maré — especifica opcionalmente que a reprodução não é permitida para dispositivos em que a quebra de maré é detectada.



Consulte os comentários no arquivo de configuração do locatário de exemplo para obter mais detalhes.
