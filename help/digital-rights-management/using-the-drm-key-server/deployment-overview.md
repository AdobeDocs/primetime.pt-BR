---
seo-title: Implantação da visão geral do servidor de chaves DRM Primetime
title: Implantação da visão geral do servidor de chaves DRM Primetime
uuid: 86630675-c15d-4f32-8212-d7343f4f92e0
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---


# Implantar o servidor de chaves DRM Primetime {#deploy-the-primetime-drm-key-server}

Antes de implantar o Primetime DRM Key Server, verifique se você instalou as versões necessárias de Java e Tomcat. Consulte [Requisitos do servidor de chaves DRM](../../digital-rights-management/using-the-drm-key-server/requirements.md).

O download do Primetime DRM Key Server inclui [!DNL faxsks.war]. Para implantar esse arquivo WAR, copie o arquivo para o diretório [!DNL webapps] do Tomcat. Se você já implantou o arquivo WAR anteriormente, talvez seja necessário excluir manualmente o diretório WAR descompactado, [!DNL faxsks] no diretório [!DNL webapps] do Tomcat). Para impedir que o Tomcat descompacte arquivos WAR, edite o arquivo [!DNL server.xml] no diretório [!DNL conf] do Tomcat e defina o atributo `unpackWARs` como `false`.

Como opção, o Primetime DRM Key Server usa uma biblioteca específica da plataforma (`jsafe.dll` no Windows ou `libjsafe.so` no Linux) para melhorar o desempenho. Copie a biblioteca apropriada para sua plataforma de `thirdparty/cryptoj/platform` para um local especificado pela variável de ambiente `PATH` (ou `LD_LIBRARY_PATH` no Linux).

>[!NOTE]
>
>A versão de 64 bits da biblioteca [!DNL jsafe] só deve ser usada se o sistema operacional e o JDK oferecerem suporte a 64 bits, caso contrário use a versão de 32 bits.

## Configuração SSL {#ssl-configuration}

O SSL é necessário para o delivery de chave HTTPS Remoto. As conexões SSL podem ser manipuladas pelo servidor de aplicativos (ou seja, pela configuração do SSL no Tomcat) ou em outro servidor (ou seja, um balanceador de carga, acelerador SSL ou Apache). O delivery de chave HTTPS remoto requer uma conexão SSL. O servidor precisa de um certificado SSL emitido por uma CA confiável.

Há várias opções para configurar o SSL. Veja a seguir exemplos para configurar o SSL com autenticação de cliente no Apache e no Tomcat.

O exemplo a seguir mostra a configuração do Apache SSL:

```
SSLEngineon 
SSLCertificateFile "certs/server_cert.pem" 
SSLCertificateKeyFile "certs/server_key.pem" 
SSLOptions +StdEnvVars +FakeBasicAuth -ExportCertData +StrictRequire 
SSLRequireSSL 
ProxyRequests Off 
ProxyPass /https://keyserver-name:port/ 
ProxyPassReverse /https://keyserver-name:port/
```

O exemplo a seguir mostra a configuração SSL do Tomcat. Para gerar certificados e arquivos de chave:

```
Generate key:  
 openssl genrsa -des3 -out server.key 1024 
Generate CSR: 
 openssl req -new -key server.key -out server.csr 
Generate Certificate: 
 openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.cer
```

Quando solicitado pelo nome comum, use o FQDN (Fully Qualified Domain Name, Nome de domínio totalmente qualificado) do servidor.

Copie [!DNL server.cer] e [!DNL server.key] para o diretório Tomcat. Especifique o seguinte Conector em [!DNL conf/server.xml]:

```
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true" 
 maxThreads="150" scheme="https" secure="true" 
 sslProtocol="TLS" 
 SSLCertificateFile="${catalina.base}/server.cer" 
 SSLCertificateKeyFile="${catalina.base}/server.key" 
 SSLPassword="password-for-key-file" 
 SSLVerifyClient="require"/>
```

## Propriedades do sistema Java {#java-system-properties}

Você tem a opção de definir as duas propriedades do sistema Java a seguir para modificar a localização dos arquivos de configuração e registro do Primetime DRM Key Server:

* `KeyServer.ConfigRoot` - Este diretório contém todos os arquivos de configuração do Primetime DRM Key Server. Para obter detalhes sobre o conteúdo desses arquivos, consulte [Arquivos de configuração do Key Server](#key-server-configuration-files). Se não estiver definido, o padrão será [!DNL CATALINA_BASE/keyserver].

* `KeyServer.LogRoot` - Este é um diretório de log que contém os logs de aplicativo do Servidor de chaves do iOS. Se não estiver definido, o padrão será igual a `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot` - Este é um diretório de log que contém os logs do aplicativo Xbox Key Server. Se não estiver definido, o padrão será igual a `KeyServer.ConfigRoot`.

Se você estiver usando [!DNL catalina.bat] ou [!DNL catalina.sh] para o start Tomcat, essas propriedades do sistema podem ser facilmente definidas usando a variável de ambiente `JAVA_OPTS`. Qualquer opção Java definida aqui será usada quando o Tomcat for iniciado. Por exemplo, defina:

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Credenciais do DRM Primetime {#primetime-drm-credentials}

Para processar solicitações de chave de clientes Primetime DRM iOS e Xbox 360, o Primetime DRM Key Server deve ser configurado com um conjunto de credenciais emitidas pelo Adobe. Essas credenciais podem ser armazenadas em arquivos PKCS#12 ( [!DNL .pfx]) ou em um HSM.

Os arquivos [!DNL .pfx] podem ser localizados em qualquer lugar, mas para facilitar a configuração, o Adobe recomenda colocar os arquivos [!DNL .pfx] no diretório de configuração do locatário. Para obter mais informações, consulte [Arquivos de configuração do Key Server](#key-server-configuration-files).

### Configuração do HSM {#section_13A19E3E32934C5FA00AEF621F369877}

Se você optar por usar um HSM para armazenar suas credenciais de servidor, deverá carregar as chaves privadas e os certificados no HSM e criar um arquivo de configuração *pkcs11.cfg*. Este arquivo deve estar localizado no diretório *KeyServer.ConfigRoot*. Consulte o diretório `<Primetime DRM Key Server>/configs` para obter um exemplo de arquivo de configuração PKCS 11. Para obter informações sobre o formato de [!DNL pkcs11.cfg], consulte a documentação do provedor Sun PKCS11.

Para verificar se seus arquivos de configuração HSM e Sun PKCS11 estão configurados corretamente, você pode usar o seguinte comando do diretório em que o arquivo [!DNL pkcs11.cfg] está localizado ( [!DNL keytool] está instalado com o Java JRE e o JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se as credenciais forem exibidas na lista, o HSM será configurado corretamente e o servidor de chaves poderá acessá-las.

## Arquivos de configuração do servidor de chaves {#key-server-configuration-files}

O Primetime DRM Key Server requer dois tipos de arquivos de configuração:

* Um arquivo de configuração global, [!DNL flashaccess-keyserver-global.xml]
* Um arquivo de configuração de locatário para cada locatário, [!DNL flashaccess-keyserver-tenant.xml]

Se forem feitas alterações nos arquivos de configuração, o servidor deverá ser reiniciado para que as alterações entrem em vigor.

Para evitar disponibilizar senhas em texto nítido nos arquivos de configuração, todas as senhas especificadas nos arquivos de configuração global e locatário devem ser criptografadas. Para obter mais informações sobre como criptografar senhas, consulte [*Scrambler de senha* em *Usando o servidor DRM Primetime para streaming protegido*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md).

## Estrutura do diretório de configuração {#configuration-directory-structure}

Os diretórios de configuração têm a seguinte estrutura:

```
KeyServer.ConfigRoot/  
--flashaccess-keyserver-global.xml 
--pkcs11.cfg (optional) 
--faxsks/ 
----tenants/ 
------tenantname/
---------flashaccess-keyserver-tenant.xml 
---------credential.pfx (optional) 
```

## Arquivo de configuração global {#global-configuration-file}

O arquivo de configuração [!DNL flashaccess-keyserver-global.xml] contém configurações que se aplicam a todos os locatários do Servidor de Chave. Esse arquivo deve estar localizado em `KeyServer.ConfigRoot`. Consulte o diretório [!DNL configs] para obter um exemplo de arquivo de configuração global. O arquivo de configuração global inclui o seguinte:

* Registro - Especifica o nível de registro e a frequência com que os arquivos de registro são rolados.
* Senha HSM - Obrigatório somente se um HSM for usado para armazenar credenciais de servidor.

Consulte os comentários no arquivo de configuração global de exemplo localizado em `<Primetime DRM Key Server>/configs` para obter mais detalhes.

## Arquivos de configuração de locatário {#tenant-configuration-files}

Os arquivos de configuração [!DNL flashaccess-ioskeyserver-tenant.xml] e [!DNL flashaccess-xboxkeyserver-tenant.xml] contêm configurações que se aplicam a um locatário específico do servidor de chaves DRM Primetime. Cada locatário tem sua própria instância desses arquivos de configuração localizados em [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. Consulte o diretório [!DNL configs/faxsks/tenants/sampletenant] para obter um exemplo de arquivo de configuração do locatário.

Você pode especificar todos os caminhos de arquivo no arquivo de configuração do locatário como caminhos absolutos ou caminhos relativos ao diretório de configuração do locatário ( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]).

Todos os arquivos de configuração do locatário incluem:

* Credenciais do Servidor de Chaves - Especifica uma ou mais credenciais do Servidor de Chaves (certificado e chave privada) emitidas pelo Adobe. Pode ser especificado como um caminho para um arquivo [!DNL .pfx] e uma senha, ou um alias para uma credencial armazenada em um HSM. Várias dessas credenciais podem ser especificadas aqui, como caminhos de arquivo, aliases de chave ou ambos.

O arquivo de configuração do locatário **iOS** inclui:

* Janela Delivery-chave - (Opcional) Especifica a janela de validade do carimbo de data e hora da solicitação do delivery-chave (em segundos). O valor padrão é de 500 segundos.

O arquivo de configuração do locatário **Xbox 360** inclui:

* Credencial XSTS - Especifica a credencial do desenvolvedor de aplicativos usada para descriptografar tokens XSTS
* Certificado de assinatura XSTS - Especifica o certificado usado para verificar a assinatura nos tokens XSTS.
* Lista de permissões do Packager - Certificados do Packager que são confiáveis pelo Servidor de chaves. Se não houver certificados do empacotador contidos na lista, todos os certificados do empacotador serão confiáveis.

## Arquivos de registro {#log-files}

Os arquivos de log gerados pelo aplicativo Primetime DRM Key Server ( [!DNL flashaccess-ioskeyserver_*.log] e [!DNL flashaccess-xboxkeyserver_*.log]) estarão localizados no diretório especificado por `KeyServer.LogRoot`.

Os arquivos de log são diferenciados por tipo de cliente. Há dois logs por tipo de cliente:

* Um *log de acesso* - monitora somente solicitações e respostas.
* A *context log* - Contém mensagens de erro detalhadas e rastreamentos de pilha.

## Iniciando o Servidor de Chave {#starting-the-key-server}

Para start do servidor de chaves, start Tomcat.