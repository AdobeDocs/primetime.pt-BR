---
description: O arquivo de configuração flashaccess-tenant.xml inclui configurações que se aplicam a um locatário específico do servidor de licenças.
title: Arquivo de configuração do inquilino
exl-id: 35ec521f-ba17-4a2d-8adb-82b2c6cbe33a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# Arquivo de configuração do inquilino{#tenant-configuration-file}

O arquivo de configuração flashaccess-tenant.xml inclui configurações que se aplicam a um locatário específico do servidor de licenças.

Cada locatário oferece suporte à própria instância desse arquivo de configuração localizado em `<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`. Consulte a `configs/flashaccessserver/tenants/sampletenant` diretório para um exemplo de arquivo de configuração de locatário.

Você pode especificar todos os caminhos de arquivo no arquivo de configuração do locatário como caminhos absolutos ou como caminhos relativos ao diretório de configuração do locatário (`<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`).

O arquivo de configuração do locatário inclui:

* *Credencial de transporte* — Especifica uma ou mais credenciais de transporte (certificado e chave privada) emitidas pelo Adobe. Pode ser especificado como um caminho para um [!DNL .pfx] arquivo e uma senha ou um alias para uma credencial armazenada em um HSM. Várias dessas credenciais podem ser especificadas aqui, como caminhos de arquivo, aliases de chave ou ambos.

   Consulte *Lidar com atualizações de certificado* in *Utilização do SDK do Adobe Primetime DRM para proteção de conteúdo* para obter mais informações sobre quando credenciais adicionais são necessárias.

* *Credencial do Servidor de Licença* — Especifica uma ou mais credenciais de servidor de licença (certificado e chave privada) emitidas pelo Adobe. Você pode especificar as credenciais do servidor de licenças como um caminho para um [!DNL .pfx] arquivo e uma senha ou um alias para uma credencial armazenada em um HSM. Várias dessas credenciais podem ser especificadas aqui, como caminhos de arquivo, aliases de chave ou ambos.

   Consulte *Lidar com atualizações de certificado* in *Utilização do SDK do Adobe Primetime DRM para proteção de conteúdo* para obter mais informações sobre quando credenciais adicionais são necessárias.

* *Certificados-chave do servidor* — Especifica opcionalmente o certificado de Servidor de chaves do License Server emitido pelo Adobe. Você pode especificar o certificado do Servidor de chaves como um caminho para um [!DNL .cer] arquivo ou um alias para um certificado armazenado em um HSM. Essa opção deve ser especificada para emitir licenças para conteúdo que é empacotado com uma política DRM que requer a entrega remota de chaves para dispositivos iOS.

* *Autorizadores personalizados* — Especifica opcionalmente as classes de autorizador personalizadas a serem chamadas para cada solicitação de licença. Se vários autorizadores forem especificados, eles serão chamados na ordem listada.
* *Lista de acondicionadores autorizados* — Especifica opcionalmente certificados que identificam entidades autorizadas a empacotar conteúdo para este servidor de licenças. Se nenhum certificado de empacotador for especificado, o servidor emitirá licenças para o conteúdo empacotado por qualquer empacotador. Se o servidor receber uma solicitação de licença de um empacotador não autorizado, a solicitação será negada.
* *Versão mínima do cliente com suporte* Consulte Uso do SDK DRM do Adobe Primetime para proteção de conteúdo.

* *Regras de uso*

   * *Licença de cache* — Especifica opcionalmente por quanto tempo você pode armazenar a licença no cliente. Por padrão, o armazenamento em cache de licenças está desativado. Para habilitar o cache de licenças por um período limitado, é necessário definir a data final ou o número de segundos para o qual a licença deve ser armazenada (começando com a emissão). Definir o número de segundos como 0 desativa o cache de licenças.

      >[!NOTE]
      >
      >Todas as licenças emitidas pelo Server for Protected Streaming incluem um período de expiração de 24 horas (86.400 segundos). Esse valor se aplica implicitamente como um limite superior a qualquer data final ou duração definida para o armazenamento em cache de licença, com um valor máximo de 86.400 segundos, mesmo que o esquema imponha limites mais altos.

   * *Reproduzir à direita* — É necessário especificar no mínimo um direito. Se você especificar vários direitos, o cliente usará o primeiro direito que atender a todos os requisitos.

      * *Proteção de saída* — Controla se a saída para dispositivos de renderização externos deve ser protegida.
      * *Restrições a aplicativos AIR e SWF* — lista de permissões opcional de aplicativos SWF e AIR que possam reproduzir o conteúdo (por exemplo, somente os aplicativos especificados são permitidos). Os aplicativos SWF são identificados por um URL ou pelo resumo do SWF e pelo tempo máximo para permitir o download e a verificação do resumo.

         Consulte *Calculadora de hash SWF* para obter informações sobre como calcular o resumo de SWF.

         Uma ID de editor e uma ID de aplicativo opcional, a versão mínima e a versão máxima identificam os aplicativos AIR e iOS. Se você não especificar restrições de aplicativos, qualquer aplicativo SWF ou AIR poderá reproduzir o conteúdo.

      * *Restrições de DRM e Módulo de Tempo de Execução* — Especifica o nível de segurança mínimo necessário para o módulo DRM/Runtime. Opcionalmente, inclui uma lista de bloqueios de versões que não têm permissão para reproduzir o conteúdo. As versões de módulos são identificadas por atributos, como sistema operacional e/ou um número de versão.

         Restrições do Módulo DRM e Restrições do Módulo de Tempo de Execução agora oferecem suporte aos seguintes atributos adicionais:

         * `oemVendor`
         * `model`
         * `screenType`

         Os seguintes atributos agora são opcionais:

         * `osVersion`
         * `version`
      * *Requisitos de capacidade do dispositivo* — especifica opcionalmente os recursos de hardware necessários para acessar o conteúdo.
      * *Requisitos de detecção de jailbreak* — Especifica opcionalmente que a reprodução não é permitida em dispositivos nos quais o jailbreak é detectado.



Consulte os comentários no arquivo de configuração de locatário de exemplo para obter mais detalhes.
