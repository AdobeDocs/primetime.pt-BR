---
title: Integração do verificador de token de mídia
description: Integração do verificador de token de mídia
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---


# Integração do verificador de token de mídia

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Sobre o Verificador de token de mídia {#about-media-token-verifier}

Quando a autorização é bem-sucedida, a autenticação do Adobe Primetime cria um token de autorização de longa duração (AuthZ).  O token AuthZ é passado para o lado do cliente ou armazenado no lado do servidor, dependendo da plataforma do cliente.  (Consulte [Noções básicas sobre tokens](/help/authentication/programmer-overview.md#understanding-tokens) para saber como os tokens são armazenados em diferentes sistemas clientes, juntamente com outros detalhes.)


Um token AuthZ autoriza o usuário do site a exibir um determinado recurso.  Ele tem um TTL (time-to-live) típico de 6 a 24 horas, após o qual o token expira. **Para acesso de visualização real, a autenticação do Primetime usa o token AuthZ para gerar um token de mídia de curta duração que você obtém e transmite para o servidor de mídia**. Esses tokens de mídia de curta duração têm um TTL muito breve (normalmente, alguns minutos).


Nas integrações do AccessEnabler, você obtém o token de mídia de curta duração por meio do `setToken()` retorno de chamada. Para integrações de API sem cliente, obtenha o token de mídia de curta duração com a variável `<SP_FQDN>/api/v1/tokens/media` Chamada de API. O token é uma string enviada em texto claro, assinada pelo Adobe, usando a proteção de token com base em PKI (Public Key Infrastructure, Infraestrutura de chave pública). Com essa proteção baseada em PKI, o token é assinado usando uma chave assimétrica, emitida para o Adobe por uma autoridade de certificação.


Como não há validação no lado do cliente para o token, um usuário mal-intencionado pode usar ferramentas para injetar falsificações `setToken()` chamadas . Portanto, você **cannot** confiar simplesmente no fato de que `setToken()` foi acionado ao considerar se um usuário está autorizado ou não. Você deve validar se o próprio token de curta duração é legítimo. A ferramenta para executar a validação é a Biblioteca do Verificador de Token de Mídia.


>[!TIP]
>
>Você deve passar todo o comprimento da string de token retornada para o Verificador de token de mídia para validação.

## Validação de tokens de curta duração com o verificador de token de mídia {#validate-short-livedttokens}

Recomendamos que os Programadores enviem o token para um serviço da Web que use a Biblioteca do verificador de token de mídia, para validar o token antes de realmente iniciar o fluxo de vídeo. O TTL muito curto dos tokens de mídia de curta duração é definido para ser suficientemente longo para permitir problemas de sincronização de relógio entre o servidor que gera o token e o servidor que valida o token, mas não mais.



O [Biblioteca do verificador de token de mídia](https://adobeprimetime.zendesk.com/auth/v2/login/signin?return_to=https%3A%2F%2Ftve.zendesk.com%2Fhc%2Fen-us%2Farticles%2F204963159-Media-Token-Verifier-library&amp;theme=hc&amp;locale=en-us&amp;brand_id=343429&amp;auth_origin=343429%2Cfalse%2Ctrue){target=_blank} O está disponível para parceiros de autenticação do Primetime.



A biblioteca Media Token Verifier está contida no arquivo Java `mediatoken-verifier-VERSION.jar`. A biblioteca define:

* Uma API de verificação de token (`ITokenVerifier` interface), com a documentação do JavaDoc
* A chave pública Adobe usada para verificar se o token realmente vem do Adobe
* Uma implementação de referência (`com.adobe.entitlement.test.EntitlementVerifierTest.java`) que mostra como usar a API Verifier e como usar a chave pública do Adobe contida na biblioteca para verificar sua origem


O arquivo contém todas as dependências e armazenamentos de chaves de certificado. A senha padrão do armazenamento de chaves do certificado incluído é &quot;123456&quot;.

* A biblioteca de verificação requer o JDK versão 1.5 ou superior.
* Use seu provedor JCE preferido para o algoritmo de assinatura, &quot;SHA256WithRSA&quot;.


**A Biblioteca do verificador deve ser o único meio usado para analisar o conteúdo do token. Os programadores não devem analisar o token e extrair os dados, pois o formato do token não é garantido e está sujeito a alterações futuras.** Somente a API Verifier deve funcionar corretamente. A análise direta da string pode funcionar temporariamente, mas causar problemas no futuro, quando o formato for alterado. A API Verifier recupera informações do token, como:

* O token é válido (a variável `isValid()` método)?
* A ID de recurso vinculada ao token (a variável `getResourceID()` método); isso pode ser comparado a (e deve corresponder) ao outro parâmetro da função `setToken()` retorno de chamada de função. Se não corresponder, isso pode indicar comportamento fraudulento.
* A hora em que o token foi emitido (`getTimeIssued()` método ).
* O TTL (`getTimeToLive()` método ).
* Um GUID de autenticação anônimo recebido do MVPD (`getUserSessionGUID()` método ).
* A ID do distribuidor que autenticou o usuário e se for o caso - o proxy-MVPD que forneceu a autenticação do distribuidor.

## Uso da API Verifier {#using-verifier-api}

O `ITokenVerifier` A classe define métodos usados para validar a autenticidade do token para um determinado recurso. Use o `ITokenVerifier` métodos para analisar um token recebido em resposta a um `setToken()` solicitação.


O `isValid()` é o principal meio de validar um token. Leva um argumento, uma ID de recurso. Se você passar uma ID de recurso nula, o método validará somente a autenticidade do token e o período de validade.


O `isValid()` retorna um destes valores de status:



| VALID_TOKEN | Todas as validações foram bem-sucedidas |
|--------------------|-----------------------------------------|
| INVALID_TOKEN_FORMAT | O formato do token é inválido |
| INVALID_SIGNATURE | Não foi possível validar a autenticidade do token |
| TOKEN_EXPIRED | O TTL do token não é válido |
| INVALID_RESOURCE_ID | Token inválido para o recurso especificado |
| ERROR_UNKNOWN | O token ainda não foi validado |

Métodos adicionais fornecem acesso específico à ID do recurso, ao tempo emitido e ao tempo de vida de um determinado token.

* Use `getResourceID()` para recuperar a ID de recurso associada ao token e compará-la com a ID retornada da solicitação setToken() .
* Use `getTimeIssued()` para recuperar a hora em que o token foi emitido.
* Use `getTimeToLive()` para recuperar o TTL.
* Use `getUserSessionGUID()` para recuperar um GUID anônimo definido pelo MVPD.
* Use `getMvpdId()` para recuperar a ID do MVPD que autenticou o usuário.
* Use `getProxyMvpdId()` para recuperar a ID do MVPD do Proxy que autenticou o usuário.

## Código de exemplo {#sample-code}

O arquivo Media Token Verifier contém uma implementação de referência (`com.adobe.entitlement.test.EntitlementVerifierTest.java`) e um exemplo de chamada da API com a classe de teste. Esta amostra (`com.adobe.entitlement.text.EntitlementVerifierTest.java`) ilustra a integração da biblioteca de verificação de token em um servidor de mídia.


```Java
package com.adobe.entitlement.test; 
import com.adobe.entitlement.verifier.CryptoDataHolder;
import com.adobe.entitlement.verifier.ITokenVerifier;
import com.adobe.entitlement.verifier.ITokenVerifierFactory;
import com.adobe.entitlement.verifier.SimpleTokenPKISignatureVerifierFactory;
import com.adobe.tve.crypto.SignatureVerificationCredential; 
import java.io.InputStream; 

public class EntitlementVerifierTest { 
    String mRequestorID = null;
    String mTokenToVerify = null;
    String mPathToCertificate = null;
    String mKeystoreType = null;
    String mKeystorePasswd = null;
    String mResourceID = null;

    public static void main(String[] args) { 
        if (args == null || args.length < 2 ) {
            System.out.println("Incorrect args: Usage: EntitlementVerifierTest requestorID tokenToVerify [resourceID]");
            return;
        } 
        String requestorID = args[0];
        String tokenToVerify = args[1];
        String pathToCertificate = "media_token_keystore.jks"; // the default keystore provided in the entitlement jar 
        String keystoreType = "jks";
        String keystorePasswd = "123456"; // password for the default keystore 
        if (requestorID == null || tokenToVerify == null) {
            System.out.println("One or more arguments is null");
            return;
        } 
        System.out.println("RequestorID: " + requestorID);
        System.out.println("token: " + tokenToVerify);
        System.out.println("cert: " + pathToCertificate);
        System.out.println("keystoretype: " + keystoreType);
        System.out.println("keystore passwd: " + keystorePasswd);
        String resourceID = null;
        if (args.length > 2) {
            resourceID = args[2];
        }
        System.out.println("Resource ID: " + resourceID);
        EntitlementVerifierTest verifier = new EntitlementVerifierTest(requestorID,
            tokenToVerify, pathToCertificate, keystoreType, keystorePasswd, resourceID);
        verifier.verifyToken();
    } 

    protected EntitlementVerifierTest(String inRequestorID,
                                      String inTokenToVerify,
                                      String inPathToCertificate,
                                      String inKeystoreType,
                                      String inKeystorePasswd, String inResourceID) {
        mRequestorID = inRequestorID;
        mTokenToVerify = inTokenToVerify;
        mPathToCertificate = inPathToCertificate;
        mKeystoreType = inKeystoreType;
        mKeystorePasswd = inKeystorePasswd;
        mResourceID = inResourceID;
    } 

    protected void verifyToken() {
        // It is expected that the SignatureVerificationCredential and 
        // CryptoDataHolder could be created at Init time in a web application 
        // and be reused for all token verifications. 
        CryptoDataHolder cryptoData = createCryptoDataHolder(mPathToCertificate, mKeystoreType, mKeystorePasswd);
        ITokenVerifierFactory tokenVerifierFactory = new SimpleTokenPKISignatureVerifierFactory();
        ITokenVerifier tokenVerifier = tokenVerifierFactory.getInstance(mRequestorID, mTokenToVerify, cryptoData);
        ITokenVerifier.eReturnValue status = tokenVerifier.isValid(mResourceID);
        System.out.println("Is token Valid? : " + status.toString());
        System.out.println("Token User ID: " + tokenVerifier.getUserSessionGUID());
        System.out.println("Token was generated at: " + tokenVerifier.getTimeIssued());

        System.out.println("Token Mvpd ID: " + tokenVerifier.getMvpdId());
        System.out.println("Token Proxy Mvpd ID: " + tokenVerifier.getProxyMvpdId());
    } 
    protected CryptoDataHolder createCryptoDataHolder(String pathToCertificate,
                                                      String keystoreType, String keystorePasswd) {
        SignatureVerificationCredential verificationCredential =
            readShortTokenVerificationCredential(pathToCertificate, keystoreType, keystorePasswd);
        CryptoDataHolder cryptoData = new CryptoDataHolder();
        cryptoData.setCertificateInfo(verificationCredential);
        return cryptoData;
    } 
    protected SignatureVerificationCredential readShortTokenVerificationCredential(String keystoreFile,
                                                                                   String keystoreType,
                                                                                   String keystorePasswd) {
        SignatureVerificationCredential cred = null; 
        if (keystoreFile != null){
            try {
                // load the keystore file 
                ClassLoader loader = EntitlementVerifierTest.class.getClassLoader();
                InputStream certInputStream =  loader.getResourceAsStream(keystoreFile);
                if (certInputStream != null) {
                    cred = new SignatureVerificationCredential(certInputStream, keystorePasswd, keystoreType);          
                }
            }
            catch (Exception e) {
                System.out.println("Error creating short token server credentials: " + e.getMessage());
            }
        }
        if (cred == null) {
            System.out.println("Error creating short token server credentials");
        } 
        return cred;
    } 
}
```
