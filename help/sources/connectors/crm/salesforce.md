---
title: Panoramica di Salesforce Source Connector
description: Scopri come collegare Salesforce a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: d8d9303e358c66c4cd891d6bf59a801c09a95f8e
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 0%

---

# [!DNL Salesforce]

>[!IMPORTANT]
>
>È ora possibile utilizzare l&#39;origine [!DNL Salesforce] quando si esegue Adobe Experience Platform su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../landing/multi-cloud.md).

>[!WARNING]
>
>L&#39;autenticazione di base per l&#39;origine [!DNL Salesforce] diventerà obsoleta a gennaio 2026. È necessario passare all&#39;autenticazione delle credenziali client OAuth 2 per continuare a utilizzare l&#39;origine e l&#39;acquisizione dei dati dall&#39;account [!DNL Salesforce] in Experience Platform.

Adobe Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un sistema CRM di terze parti. Il supporto per i provider di gestione delle relazioni con i clienti include [!DNL Salesforce].

## Configura l&#39;origine [!DNL Salesforce] per Experience Platform su Azure {#azure}

Segui i passaggi seguenti per scoprire come configurare l&#39;account [!DNL Salesforce] per Experience Platform su Azure.

### Indirizzo IP in cui è inserita nell&#39;elenco Consentiti la connessione ad Azure

Prima di collegare le origini a Experience Platform in Azure, è necessario aggiungere al elenco Consentiti di indirizzi IP specifici per l’area geografica. La mancata aggiunta di indirizzi IP specifici per l’area geografica al elenco Consentiti può causare errori o non prestazioni durante l’utilizzo delle origini. Per ulteriori informazioni, leggere la pagina [Indirizzo IP/inserisco nell&#39;elenco Consentiti di](../../ip-address-allow-list.md).

>[!BEGINTABS]

>[!TAB VA7]

- `40.70.226.96/28`
- `40.70.226.32/28`
- `52.232.229.255`
- `52.232.229.253`
- `40.70.226.144/28`
- `40.70.226.64/28`
- `40.70.225.240/28`
- `40.70.225.224/28`
- `40.70.224.64/29`
- `40.70.226.80/28`
- `40.70.226.176/28`
- `52.232.229.230`
- `40.70.226.128/28`
- `40.70.226.0/28`
- `40.70.226.16/28`
- `52.138.119.167`
- `40.70.226.160/28`
- `40.70.226.192/28`
- `40.70.226.48/28`
- `20.96.243.176`
- `40.70.226.112/28`
- `40.70.226.208/28`

>[!TAB NLD2]

- `40.74.4.144/28`
- `40.74.3.176/28`
- `40.74.5.128/28`
- `40.74.4.176/28`
- `40.74.6.112/28`
- `40.74.7.128/28`
- `40.74.6.144/28`
- `51.105.144.81`
- `52.142.236.87`
- `40.74.6.80/28`
- `20.101.246.9`
- `40.74.7.208/28`
- `40.74.6.128/28`
- `40.74.7.176/28`
- `51.124.70.4`
- `40.74.7.144/28`
- `108.141.12.47`
- `20.50.23.153`
- `51.144.184.248/29`
- `40.74.7.160/28`
- `40.74.7.192/28`
- `51.105.144.1`
- `40.74.4.160/28`
- `40.74.6.96/28`

>[!TAB AUS5]

- `20.43.111.32/28`
- `20.43.110.144/28`
- `20.53.111.113`
- `20.227.32.175`
- `20.43.110.96/28`
- `20.43.110.64/28`
- `20.193.56.144/28`
- `20.43.110.192/28`
- `20.43.97.95`
- `20.43.111.16/28`
- `20.43.110.128/28`
- `20.40.185.111`
- `20.193.56.160/28`
- `20.43.110.112/28`
- `40.82.220.111`
- `20.43.111.0/28`
- `20.193.38.208/28`
- `20.43.110.80/28`
- `20.43.110.176/28`
- `20.43.110.48/28`
- `20.193.36.37`
- `20.43.110.208/28`
- `20.43.110.224/28`
- `20.43.110.160/28`
- `20.40.185.225`
- `20.43.110.240/28`
- `20.193.56.128/28`
- `20.40.185.185`

>[!TAB CAN2]

- `20.116.159.48/28`
- `20.116.159.144/28`
- `20.116.159.96/28`
- `20.220.243.238`
- `20.116.159.80/28`
- `20.116.159.32/28`
- `20.151.241.138`
- `4.172.28.20`
- `20.151.241.124`
- `20.116.248.0/28`
- `20.116.155.128/28`
- `20.116.159.64/28`
- `20.116.159.192/28`
- `20.116.159.176/28`
- `20.116.175.240/28`
- `20.116.248.16/28`
- `20.116.158.240/28`
- `20.116.159.112/28`
- `20.151.240.247`
- `20.151.241.173`
- `20.116.159.128/28`
- `20.116.159.160/28`
- `20.116.159.0/28`
- `20.104.5.248`
- `20.116.175.224/28`
- `20.116.159.208/28`
- `20.116.159.224/28`

>[!TAB GBR9]

- `20.162.155.16/28`
- `20.162.154.96/28`
- `20.26.64.0/28`
- `20.26.64.96/28`
- `20.162.154.64/28`
- `20.108.200.27`
- `20.162.154.80/28`
- `20.162.153.192/28`
- `20.108.200.61`
- `20.162.154.48/28`
- `20.162.154.192/28`
- `20.162.154.0/28`
- `20.26.64.16/28`
- `20.162.154.112/28`
- `20.162.153.32/28`
- `20.254.80.141`
- `20.162.153.208/28`
- `20.108.203.20`
- `20.26.64.48/28`
- `20.162.154.240/28`
- `20.162.154.208/28`
- `20.162.154.160/28`
- `20.108.205.182`
- `20.108.202.198`
- `20.162.154.32/28`
- `20.162.153.16/28`

>[!TAB IND2]

- `4.188.92.84`
- `4.224.5.224/28`
- `4.224.7.32/28`
- `4.188.92.87`
- `4.188.89.92`
- `4.224.5.112/28`
- `4.224.6.80/28`
- `4.224.144.224/28`
- `4.224.144.240/28`
- `4.224.6.96/28`
- `4.188.89.255`
- `4.188.94.32/28`
- `4.224.5.96/28`
- `4.224.6.64/28`
- `4.224.7.48/28`
- `4.224.5.208/28`
- `4.188.90.65`
- `4.224.6.16/28`
- `4.224.6.0/28`
- `4.224.5.192/28`
- `4.224.7.16/28`
- `4.188.90.67`
- `4.188.90.17`
- `4.188.94.48/28`
- `4.224.6.112/28`
- `4.224.5.240/28`
- `4.224.7.0/28`

>[!ENDTABS]

### Mappatura campo da [!DNL Salesforce] a XDM

Per stabilire una connessione di origine tra [!DNL Salesforce] e Experience Platform, i campi dei dati di origine [!DNL Salesforce] devono essere mappati sui campi XDM di destinazione appropriati prima di essere acquisiti in Experience Platform.

Per informazioni dettagliate sulle regole di mappatura dei campi tra [!DNL Salesforce] set di dati e Experience Platform, consulta:

- [Contatti](../adobe-applications/mapping/salesforce.md#contact)
- [Lead](../adobe-applications/mapping/salesforce.md#lead)
- [Account](../adobe-applications/mapping/salesforce.md#account)
- [Opportunità](../adobe-applications/mapping/salesforce.md#opportunity)
- [Ruoli di contatto opportunità](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campagne](../adobe-applications/mapping/salesforce.md#campaign)
- [Membri della campagna](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Relazione contatto account](../adobe-applications/mapping/salesforce.md#account-contact-relation)

### Configurare l&#39;utilità di generazione automatica dello spazio dei nomi e dello schema [!DNL Salesforce]

Per utilizzare l&#39;origine [!DNL Salesforce] come parte di [!DNL B2B-CDP], è necessario prima impostare un&#39;utilità [!DNL Postman] per generare automaticamente gli spazi dei nomi e gli schemi [!DNL Salesforce]. La documentazione seguente fornisce ulteriori informazioni sulla configurazione dell&#39;utilità [!DNL Postman]:

- È possibile scaricare la raccolta di utilità di generazione automatica dello spazio dei nomi e dello schema e l&#39;ambiente da questo [archivio GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Per informazioni sull&#39;utilizzo delle API di Experience Platform, inclusi i dettagli su come raccogliere i valori per le intestazioni richieste e leggere chiamate API di esempio, consulta la guida introduttiva [alle API di Experience Platform](../../../landing/api-guide.md).
- Per informazioni su come generare le credenziali per le API Experience Platform, consulta l&#39;esercitazione su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md).
- Per informazioni sulla configurazione di [!DNL Postman] per le API di Experience Platform, consulta l&#39;esercitazione su [configurazione della console per sviluppatori e  [!DNL Postman]](../../../landing/postman.md).

Con una console per sviluppatori Experience Platform e la configurazione di [!DNL Postman], puoi iniziare ad applicare i valori di ambiente appropriati all&#39;ambiente [!DNL Postman].

+++Visualizza la guida della tabella delle variabili

La tabella seguente contiene valori di esempio e informazioni aggiuntive sul popolamento dell&#39;ambiente [!DNL Postman]:

| Variable | Descrizione | Esempio |
| --- | --- | --- |
| `CLIENT_SECRET` | Identificatore univoco utilizzato per generare `{ACCESS_TOKEN}`. Per informazioni su come recuperare `{CLIENT_SECRET}`, consulta il tutorial su [autenticazione e accesso alle API di Experience Platform](../../../landing/api-authentication.md). | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Il JSON Web Token (JWT) è una credenziale di autenticazione utilizzata per generare {ACCESS_TOKEN}. Per informazioni su come generare `{JWT_TOKEN}`, consulta il tutorial su [autenticazione e accesso alle API di Experience Platform](../../../landing/api-authentication.md). | `{JWT_TOKEN}` |
| `API_KEY` | Identificatore univoco utilizzato per autenticare le chiamate alle API di Experience Platform. Per informazioni su come recuperare `{API_KEY}`, consulta il tutorial su [autenticazione e accesso alle API di Experience Platform](../../../landing/api-authentication.md). | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Il token di autorizzazione necessario per completare le chiamate alle API di Experience Platform. Per informazioni su come recuperare `{ACCESS_TOKEN}`, consulta il tutorial su [autenticazione e accesso alle API di Experience Platform](../../../landing/api-authentication.md). | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Il contenitore `global` contiene tutte le classi, i gruppi di campi di schema, i tipi di dati e gli schemi standard forniti dai partner Adobe e Experience Platform. Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su `global`. | `global` |
| `PRIVATE_KEY` | Credenziali utilizzate per autenticare l&#39;istanza [!DNL Postman] nelle API Experience Platform. Per istruzioni su come recuperare {PRIVATE_KEY}, consulta il tutorial sulla configurazione di Developer Console e [configurazione di Developer Console e [!DNL Postman]](../../../landing/postman.md). | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Credenziali utilizzate per l’integrazione in Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS) fornisce il framework per l’autenticazione nei servizi Adobe. Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Entità aziendale che può possedere o concedere in licenza prodotti e servizi e consentire l&#39;accesso ai propri membri. Per istruzioni su come recuperare le informazioni di `{ORG_ID}`, consulta il tutorial su [come configurare la console per sviluppatori e  [!DNL Postman]](../../../landing/postman.md). | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nome della partizione sandbox virtuale in uso. | `prod` |
| `TENANT_ID` | ID utilizzato per garantire che le risorse create abbiano lo spazio dei nomi corretto e siano contenute all’interno dell’organizzazione. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | L’endpoint URL a cui stai effettuando chiamate API. Questo valore è fisso ed è sempre impostato su: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | ID univoco dell&#39;account [!DNL Marketo]. Per informazioni su come recuperare `munchkinId`, consulta il tutorial su [autenticazione dell&#39;istanza](../adobe-applications/marketo/marketo-auth.md). [!DNL Marketo]  | `123-ABC-456` |
| `sfdc_org_id` | L&#39;ID organizzazione per l&#39;account [!DNL Salesforce]. Per ulteriori informazioni sull&#39;acquisizione dell&#39;ID organizzazione [!DNL Salesforce], consulta la [[!DNL Salesforce] guida](https://help.salesforce.com/articleView?id=000325251&type=1&mode=1) seguente. | `00D4W000000FgYJUA0` |
| `has_abm` | Valore booleano che indica se sei abbonato a [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Valore booleano che indica se sei abbonato a [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

+++

### Eseguire gli script

Dopo aver configurato la raccolta [!DNL Postman] e l&#39;ambiente, è ora possibile eseguire lo script tramite l&#39;interfaccia [!DNL Postman].

Nell&#39;interfaccia [!DNL Postman], selezionare la cartella principale dell&#39;utilità di generazione automatica, quindi selezionare **[!DNL Run]** dall&#39;intestazione superiore.

![cartella-radice](../../images/tutorials/create/salesforce/root-folder.png)

Viene visualizzata l&#39;interfaccia [!DNL Runner]. Da qui, assicurarsi che tutte le caselle di controllo siano selezionate, quindi selezionare **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

In caso di esito positivo, la richiesta crea gli spazi dei nomi e gli schemi B2B in base alle specifiche beta.

## Configura l&#39;origine [!DNL Salesforce] per Experience Platform su Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../landing/multi-cloud.md).

Segui i passaggi seguenti per scoprire come configurare l&#39;account [!DNL Salesforce] per Experience Platform su Amazon Web Services (AWS).

### Prerequisiti

Per connettere l&#39;account [!DNL Salesforce] ad Experience Platform in un&#39;area geografica AWS, è necessario disporre dei seguenti elementi:

- Un account [!DNL Salesforce] con accesso API.
- Un [!DNL Salesforce Connected App] che puoi quindi utilizzare per abilitare il flusso OAuth JWT_BEARER.
- Le autorizzazioni necessarie in [!DNL Salesforce] per accedere ai dati.

### Indirizzo IP da inserire nell&#39;elenco Consentiti per la connessione su AWS

Prima di collegare le origini a Experience Platform su AWS, è necessario aggiungere al elenco Consentiti di indirizzi IP specifici per l’area geografica. Per ulteriori informazioni, leggere la guida su [inserire nell&#39;elenco Consentiti degli indirizzi IP per la connessione ad Experience Platform su AWS](../../ip-address-allow-list.md).

### Crea un [!DNL Salesforce Connected App]

Innanzitutto, utilizza quanto segue per creare una coppia certificato/chiave di file PEM.

```shell
openssl req -newkey rsa:4096 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem  
```

1. Nel dashboard [!DNL Salesforce] selezionare le impostazioni (![Icona Impostazioni.](/help/images/icons/settings.png)) e quindi selezionare **[!DNL Setup]**.
2. Passare a [!DNL App Manager] e selezionare **[!DNL New Connection App]**.
3. Specifica un nome per l&#39;app e consenti la compilazione automatica degli altri campi.
4. Abilita la casella per [!DNL Enable OAuth Settings].
5. Imposta un URL di callback. Poiché non verrà utilizzato per JWT, puoi utilizzare `https://localhost`.
6. Abilita la casella per [!DNL Use Digital Signatures].
7. Carica il file cert.pem creato in precedenza.

#### Aggiungere le autorizzazioni richieste

Aggiungi le seguenti autorizzazioni:

1. Gestire i dati utente tramite API (API)
2. Accedere alle autorizzazioni personalizzate (custom_permissions)
3. Accedere al servizio URL di identità (ID, profilo, e-mail, indirizzo, telefono)
4. Accedere a identificatori univoci (openid)
5. Eseguire richieste in qualsiasi momento (refresh_token, offline_access)

Dopo aver aggiunto le autorizzazioni, assicurarsi di abilitare la casella per **[!DNL Issue JSON Web Token (JWT)-based access tokens for named user]**.

Selezionare **[!DNL Save]**, **[!DNL Continue]** e quindi **[!DNL Manage Customer Details]**. Utilizza il pannello dei dettagli del consumatore per recuperare quanto segue:

- **Chiave consumer**: in seguito utilizzerai questa chiave consumer come ID client durante l&#39;autenticazione dell&#39;account [!DNL Salesforce] in Experience Platform.
- **Segreto consumer**: in seguito utilizzerai questo segreto consumer come ID client durante l&#39;autenticazione dell&#39;account [!DNL Salesforce] in Experience Platform.

### Autorizza l&#39;utente [!DNL Salesforce] all&#39;app connessa

Segui i passaggi seguenti per ottenere l’autorizzazione all’utilizzo dell’app connessa:

1. Passa a **[!DNL Manage Connected Apps]**.
2. Seleziona **[!DNL Edit]**.
3. Configurare **[!DNL Permitted Users]** come **[!DNL Admin approved users are pre-authorized]**, quindi selezionare **[!DNL Save]**.
4. Passa a **[!DNL Settings]> [!DNL Manage Users] >[!DNL Profiles]**.
5. Modifica il profilo associato al tuo utente.
6. Passa a **[!DNL Connected App Access]**, quindi seleziona l&#39;app creata in un passaggio precedente.

### Genera token JWT bearer

Per generare il token JWT bearer, segui la procedura riportata di seguito.

#### Converti coppia di chiavi in pkcs12

Per generare il token JWT bearer, devi innanzitutto usare il seguente comando per convertire il certificato/coppia di chiavi in formato pkcs12. Durante questo passaggio, devi anche **impostare una password di esportazione** quando richiesto.

```shell
openssl pkcs12 -export -in cert.pem -inkey key.pem -name jwtcert >jwtcert.p12
```

#### Creare un keystore Java basato su pkcs12

Quindi, utilizza il seguente comando per creare un keystore Java basato sul pkcs12 appena generato. Durante questo passaggio, devi anche impostare una **password per il keystore di destinazione** quando richiesto. Inoltre, devi fornire la password di esportazione precedente come password del keystore di origine.

```shell
keytool -importkeystore -srckeystore jwtcert.p12 -destkeystore keystore.jks -srcstoretype pkcs12 -alias jwtcert
```

#### Verifica che il file keystroke.jks includa un alias jwtcert

Utilizzare quindi il comando follow per verificare che `keystroke.jks` includa un alias `jwtcert`. Durante questo passaggio, verrà richiesto di fornire la password del keystore di destinazione generata nel passaggio precedente.

```shell
keytool -keystore keystore.jks -list
```

#### Genera token firmato

Infine, utilizza la classe Java JWTExample seguente per generare il token firmato.

```java
package org.example;
 
import org.apache.commons.codec.binary.Base64;
 
import java.io.*;
import java.security.*;
import java.text.MessageFormat;
 
public class Main {
 
    public static void main(String[] args) {
 
        String header = "{\"alg\":\"RS256\"}";
        String claimTemplate = "'{'\"iss\": \"{0}\", \"sub\": \"{1}\", \"aud\": \"{2}\", \"exp\": \"{3}\"'}'";
 
        try {
            StringBuffer token = new StringBuffer();
 
            //Encode the JWT Header and add it to our string to sign
            token.append(Base64.encodeBase64URLSafeString(header.getBytes("UTF-8")));
 
            //Separate with a period
            token.append(".");
 
            //Create the JWT Claims Object
            String[] claimArray = new String[5];
            claimArray[0] = "{CLIENT_ID}";
            claimArray[1] = "{AUTHORIZED_SALESFORCE_USERNAME}";
            claimArray[2] = "{SALESFORCE_LOGIN_URL}";
            claimArray[3] = Long.toString((System.currentTimeMillis() / 1000) + 2629746*4);
            MessageFormat claims;
            claims = new MessageFormat(claimTemplate);
            String payload = claims.format(claimArray);
 
            //Add the encoded claims object
            token.append(Base64.encodeBase64URLSafeString(payload.getBytes("UTF-8")));
 
            //Load the private key from a keystore
            KeyStore keystore = KeyStore.getInstance("JKS");
            keystore.load(new FileInputStream("path/to/keystore"), "keystorepassword".toCharArray());
            PrivateKey privateKey = (PrivateKey) keystore.getKey("jwtcert", "privatekeypassword".toCharArray());
 
            //Sign the JWT Header + "." + JWT Claims Object
            Signature signature = Signature.getInstance("SHA256withRSA");
            signature.initSign(privateKey);
            signature.update(token.toString().getBytes("UTF-8"));
            String signedPayload = Base64.encodeBase64URLSafeString(signature.sign());
 
            //Separate with a period
            token.append(".");
 
            //Add the encoded signature
            token.append(signedPayload);
 
            System.out.println(token.toString());
 
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

| Proprietà | Configurazioni  |
| --- | --- |
| `claimArray[0]` | Aggiorna `claimArray[0]` con il tuo ID client. |
| `claimArray[1]` | Aggiorna `claimArray[1]` con il nome utente [!DNL Salesforce] autorizzato per l&#39;app. |
| `claimArray[2]` | Aggiorna `claimArray[2]` con l&#39;URL di accesso di [!DNL Salesforce]. |
| `claimArray[3]` | Aggiorna `claimArray[3]` con una data di scadenza formattata in millisecondi dall&#39;epoca. Ad esempio `3660624000000` è 12-31-2085. |
| `/path/to/keystore` | Sostituisci `/path/to/keystore` con il percorso corretto per keystore.jks |
| `keystorepassword` | Sostituisci `keystorepassword` con la password del keystore di destinazione. |
| `privatekeypassword` | Sostituisci `privatekeypassword` con la password del keystore di origine. |

## Passaggi successivi

Dopo aver completato la configurazione dei prerequisiti per l&#39;account [!DNL Salesforce], puoi procedere con la connessione dell&#39;account [!DNL Salesforce] ad Experience Platform e acquisire i dati di gestione delle relazioni con i clienti. Per ulteriori informazioni, consulta la documentazione seguente:

### Connetti [!DNL Salesforce] ad Experience Platform tramite API

La documentazione seguente fornisce informazioni su come connettere [!DNL Salesforce] ad Experience Platform tramite API o tramite l&#39;interfaccia utente:

- [Connettere Salesforce ad Experience Platform utilizzando l’API del servizio Flusso](../../tutorials/api/create/crm/salesforce.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine CRM utilizzando l’API del servizio Flusso](../../tutorials/api/collect/crm.md)

### Connetti [!DNL Salesforce] ad Experience Platform tramite l&#39;interfaccia utente

- [Creare una connessione sorgente Salesforce nell’interfaccia utente](../../tutorials/ui/create/crm/salesforce.md)
- [Creare un flusso di dati per una connessione CRM nell’interfaccia utente](../../tutorials/ui/dataflow/crm.md)