---
title: Panoramica di Salesforce Source Connector
description: Scopri come collegare Salesforce a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: f62e13e97cc82fef759d06b94337f4cc25d4fb10
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 0%

---

# [!DNL Salesforce]

>[!IMPORTANT]
>
>È ora possibile utilizzare l&#39;origine [!DNL Salesforce] quando si esegue Adobe Experience Platform su Amazon Web Services (AWS). Un Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta l&#39;[panoramica sul cloud multiplo di Experience Platform](../../../landing/multi-cloud.md).

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un sistema CRM di terze parti. Il supporto per i provider di gestione delle relazioni con i clienti include [!DNL Salesforce].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Mappatura campo da [!DNL Salesforce] a XDM

Per stabilire una connessione di origine tra [!DNL Salesforce] e Platform, i campi dati di origine [!DNL Salesforce] devono essere mappati sui campi XDM di destinazione appropriati prima di essere acquisiti in Platform.

Per informazioni dettagliate sulle regole di mappatura dei campi tra [!DNL Salesforce] set di dati e Platform, consulta:

- [Contatti](../adobe-applications/mapping/salesforce.md#contact)
- [Lead](../adobe-applications/mapping/salesforce.md#lead)
- [Account](../adobe-applications/mapping/salesforce.md#account)
- [Opportunità](../adobe-applications/mapping/salesforce.md#opportunity)
- [Ruoli di contatto opportunità](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campagne](../adobe-applications/mapping/salesforce.md#campaign)
- [Membri della campagna](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Relazione contatto account](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Configurare l&#39;utilità di generazione automatica dello spazio dei nomi e dello schema [!DNL Salesforce]

Per utilizzare l&#39;origine [!DNL Salesforce] come parte di [!DNL B2B-CDP], è necessario prima impostare un&#39;utilità [!DNL Postman] per generare automaticamente gli spazi dei nomi e gli schemi [!DNL Salesforce]. La documentazione seguente fornisce ulteriori informazioni sulla configurazione dell&#39;utilità [!DNL Postman]:

- È possibile scaricare la raccolta di utilità di generazione automatica dello spazio dei nomi e dello schema e l&#39;ambiente da questo [archivio GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Per informazioni sull&#39;utilizzo delle API di Platform, inclusi i dettagli su come raccogliere i valori per le intestazioni richieste e leggere chiamate API di esempio, consulta la guida introduttiva [alle API di Platform](../../../landing/api-guide.md).
- Per informazioni su come generare le credenziali per le API di Platform, consulta l&#39;esercitazione su [autenticazione e accesso alle API di Experience Platform](../../../landing/api-authentication.md).
- Per informazioni sulla configurazione di [!DNL Postman] per le API di Platform, consulta l&#39;esercitazione su [configurazione della console per sviluppatori e  [!DNL Postman]](../../../landing/postman.md).

Con una console per sviluppatori Platform e [!DNL Postman] configurati, puoi iniziare ad applicare i valori di ambiente appropriati all&#39;ambiente [!DNL Postman].

+++Visualizza la guida della tabella delle variabili

La tabella seguente contiene valori di esempio e informazioni aggiuntive sul popolamento dell&#39;ambiente [!DNL Postman]:

| Variable | Descrizione | Esempio |
| --- | --- | --- |
| `CLIENT_SECRET` | Identificatore univoco utilizzato per generare `{ACCESS_TOKEN}`. Per informazioni su come recuperare `{CLIENT_SECRET}`, consulta il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md). | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Il JSON Web Token (JWT) è una credenziale di autenticazione utilizzata per generare {ACCESS_TOKEN}. Per informazioni su come generare `{JWT_TOKEN}`, consulta il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md). | `{JWT_TOKEN}` |
| `API_KEY` | Identificatore univoco utilizzato per autenticare le chiamate alle API Experience Platform. Per informazioni su come recuperare `{API_KEY}`, consulta il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md). | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Il token di autorizzazione necessario per completare le chiamate alle API Experience Platform. Per informazioni su come recuperare `{ACCESS_TOKEN}`, consulta il tutorial su [autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md). | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Il contenitore `global` contiene tutte le classi, i gruppi di campi dello schema, i tipi di dati e gli schemi standard forniti dal partner Adobe e Experience Platform. Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su `global`. | `global` |
| `PRIVATE_KEY` | Credenziali utilizzate per autenticare l&#39;istanza [!DNL Postman] in Experience Platform API. Per istruzioni su come recuperare {PRIVATE_KEY}, consulta il tutorial sulla configurazione di Developer Console e [configurazione di Developer Console e [!DNL Postman]](../../../landing/postman.md). | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Credenziali utilizzate per l&#39;integrazione in Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS) fornisce il framework per l’autenticazione nei servizi Adobe. Per quanto riguarda [!DNL Marketo], questo valore è fisso ed è sempre impostato su: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Entità aziendale che può possedere o concedere in licenza prodotti e servizi e consentire l&#39;accesso ai propri membri. Per istruzioni su come recuperare le informazioni di `{ORG_ID}`, consulta il tutorial su [come configurare la console per sviluppatori e  [!DNL Postman]](../../../landing/postman.md). | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nome della partizione sandbox virtuale in uso. | `prod` |
| `TENANT_ID` | ID utilizzato per garantire che le risorse create abbiano lo spazio dei nomi corretto e siano contenute all’interno dell’organizzazione. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | L’endpoint URL a cui stai effettuando chiamate API. Questo valore è fisso ed è sempre impostato su: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | ID univoco dell&#39;account [!DNL Marketo]. Per informazioni su come recuperare `munchkinId`, consulta il tutorial su [autenticazione dell&#39;istanza](../adobe-applications/marketo/marketo-auth.md). [!DNL Marketo]  | `123-ABC-456` |
| `sfdc_org_id` | L&#39;ID organizzazione per l&#39;account [!DNL Salesforce]. Per ulteriori informazioni sull&#39;acquisizione dell&#39;ID organizzazione [!DNL Salesforce], consulta la [[!DNL Salesforce] guida](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) seguente. | `00D4W000000FgYJUA0` |
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

## Configura l&#39;origine [!DNL Salesforce], ad Experience Platform su Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Un Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta l&#39;[panoramica sul cloud multiplo di Experience Platform](../../../landing/multi-cloud.md).

Segui i passaggi seguenti per scoprire come configurare l&#39;account [!DNL Salesforce], ad Experience Platform su Amazon Web Services (AWS).

### Prerequisiti

Per connettere l&#39;account [!DNL Salesforce] all&#39;Experience Platform in un&#39;area geografica AWS, è necessario disporre dei seguenti elementi:

- Un account [!DNL Salesforce] con accesso API.
- Un [!DNL Salesforce Connected App] che puoi quindi utilizzare per abilitare il flusso OAuth JWT_BEARER.
- Le autorizzazioni necessarie in [!DNL Salesforce] per accedere ai dati.

Per connettere l&#39;account [!DNL Salesforce] all&#39;Experience Platform su Amazon Web Services (AWS), è necessario aggiungere anche i seguenti indirizzi IP al inserisco nell&#39;elenco Consentiti di:

- `34.193.63.59`
- `44.217.93.240`
- `44.194.79.229`

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

- **Chiave consumer**: questa chiave consumer verrà utilizzata in seguito come ID client durante l&#39;autenticazione dell&#39;account [!DNL Salesforce] per l&#39;Experience Platform.
- **Segreto consumer**: in seguito utilizzerai questo segreto consumer come ID client durante l&#39;autenticazione dell&#39;account [!DNL Salesforce] per l&#39;Experience Platform.

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

Dopo aver completato la configurazione dei prerequisiti per l&#39;account [!DNL Salesforce], puoi procedere con la connessione dell&#39;account [!DNL Salesforce] per l&#39;Experience Platform e l&#39;acquisizione dei dati CRM. Per ulteriori informazioni, consulta la documentazione seguente:

### Connetti [!DNL Salesforce] a Platform tramite API

La documentazione seguente fornisce informazioni su come connettere [!DNL Salesforce] a Platform tramite API o tramite l&#39;interfaccia utente:

- [Creare una connessione di base Salesforce utilizzando l’API del servizio Flusso](../../tutorials/api/create/crm/salesforce.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine CRM utilizzando l’API del servizio Flusso](../../tutorials/api/collect/crm.md)

### Connetti [!DNL Salesforce] a Platform tramite l&#39;interfaccia utente

- [Creare una connessione sorgente Salesforce nell’interfaccia utente](../../tutorials/ui/create/crm/salesforce.md)
- [Creare un flusso di dati per una connessione CRM nell’interfaccia utente](../../tutorials/ui/dataflow/crm.md)