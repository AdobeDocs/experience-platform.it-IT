---
title: Connessione SAP Commerce
description: Utilizzare il connettore di destinazione SAP Commerce per aggiornare i record dei clienti nell'account SAP.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 3bd1a2a7-fb56-472d-b9bd-603b94a8937e
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 3%

---

# Connessione [!DNL SAP Commerce]

[!DNL SAP Commerce], precedentemente noto come [[!DNL Hybris]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), è una soluzione di piattaforma di e-commerce basata su cloud per le aziende B2B e B2C e disponibile come parte del portafoglio SAP Customer Experience. [[!DNL SAP] La fatturazione dell&#39;abbonamento](https://www.sap.com/products/financial-management/subscription-billing.html) è un prodotto incluso nel portfolio e consente la gestione completa del ciclo di vita dell&#39;abbonamento con esperienze di vendita e pagamento semplificate tramite integrazioni standardizzate.

Questa [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) utilizza la [[!DNL SAP Subscription Billing] API di gestione clienti](https://api.sap.com/api/BusinessPartner_APIs/path/PUT_customers-customerNumber), per aggiornare i dettagli del cliente entro [!DNL SAP Commerce] da un pubblico Experience Platform esistente dopo l&#39;attivazione.

Le istruzioni per l&#39;autenticazione nell&#39;istanza [!DNL SAP Commerce] sono riportate di seguito, nella sezione [Autentica nella destinazione](#authenticate).

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione [!DNL SAP Commerce], ecco un esempio di caso d&#39;uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

I clienti [!DNL SAP Commerce] memorizzano informazioni su singoli utenti o entità organizzative che interagiscono con la tua azienda. Il tuo team utilizza i clienti esistenti in [!DNL SAP Commerce] per creare i tipi di pubblico di Experience Platform. Dopo aver inviato questi tipi di pubblico a [!DNL SAP Commerce], le informazioni vengono aggiornate e a ciascun cliente viene assegnata una proprietà con il relativo valore come nome del pubblico che indica a quale pubblico appartiene il cliente.

## Prerequisiti {#prerequisites}

Consultare le sezioni seguenti per eventuali prerequisiti da impostare in Experience Platform e [!DNL SAP Commerce] e per informazioni da raccogliere prima di utilizzare la destinazione [!DNL SAP Commerce].

### Experience Platform prerequisiti {#prerequisites-in-experience-platform}

Prima di attivare i dati nella destinazione [!DNL SAP Commerce], è necessario disporre di uno [schema](/help/xdm/schema/composition.md), un [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) e [tipi di pubblico](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) creati in [!DNL Experience Platform].

Se hai bisogno di indicazioni sugli stati del pubblico, consulta la documentazione di Experience Platform per il gruppo di campi dello schema [Dettagli appartenenza pubblico](/help/xdm/field-groups/profile/segmentation.md).

### Prerequisiti per la destinazione [!DNL SAP Commerce] {#prerequisites-destination}

Per esportare i dati da Platform al tuo account [!DNL SAP Commerce], tieni presente i seguenti prerequisiti:

#### Devi avere un account [!DNL SAP Subscription Billing] {#prerequisites-account}

Per esportare i dati da Platform all&#39;account [!DNL SAP Commerce], è necessario disporre di un account [!DNL SAP Subscription Billing]. Se non disponi di un account di fatturazione valido, contatta il tuo account manager [!DNL SAP]. Per ulteriori informazioni, consultare il documento [[!DNL SAP] Configurazione piattaforma](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf).

#### Generare una chiave di servizio {#prerequisites-service-key}

* La chiave del servizio [!DNL SAP Commerce] ti consente di accedere all&#39;API [!DNL SAP Subscription Billing] tramite Experience Platform. Per creare una chiave di servizio, consultare [!DNL SAP Commerce] [creare una chiave di servizio con ID client e segreto client](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/87c11a0f5dc3494eaf3baa355925c030.html#create-a-service-key-with-client-id-and-client-secret). [!DNL SAP Commerce] richiede quanto segue:
   * ID client
   * Segreto client
   * URL. Schema URL: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Questo valore verrà utilizzato successivamente per ottenere i valori per `Region` e `Endpoint`.

+++Seleziona per visualizzare un esempio della chiave del servizio

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

#### Crea riferimenti personalizzati in [!DNL SAP Subscription Billing] {#prerequisites-custom-reference}

Per aggiornare lo stato del pubblico di Experience Platform in [!DNL SAP Subscription Billing], è necessario un campo di riferimento personalizzato per ogni pubblico selezionato in Platform.

Per creare i riferimenti personalizzati, accedere all&#39;account [!DNL SAP Subscription Billing] e passare alla pagina **[Dati e configurazione principali]** > **[Riferimenti personalizzati]**. Quindi, seleziona **[!UICONTROL Crea]** per aggiungere un nuovo riferimento per ogni pubblico selezionato in Platform. Questi nomi dei campi di riferimento saranno necessari nel passaggio successivo di [Pianifica esportazione pubblico ed esempio](#schedule-segment-export-example).

Di seguito è riportato un esempio di come creare un **[!UICONTROL tipo di riferimento]** personalizzato in [!DNL SAP Subscription Billing]:
![Immagine che mostra dove creare un riferimento personalizzato nella fatturazione dell&#39;abbonamento SAP.](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

Per ulteriori informazioni, consulta la documentazione [!DNL SAP Subscription Billing] [riferimenti personalizzati](https://help.sap.com/docs/CLOUD_TO_CASH_OD/80d121f216af43648e79664efe5595f7/85696a63c8d8453a934e86c9413a25cf.html?version=2023-11-27).

### Raccogli le credenziali richieste {#gather-credentials}

Per connettere [!DNL SAP Commerce] a Experience Platform, è necessario fornire i valori per le proprietà di connessione seguenti:

| Credenziali | Descrizione |
| --- | --- |
| ID client | Il valore di `clientId` dalla chiave del servizio. |
| Segreto client | Il valore di `clientSecret` dalla chiave del servizio. |
| Endpoint | Il valore di `url` dalla chiave del servizio è simile a `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| Area geografica | La posizione del centro dati. L&#39;area è presente in `url` e ha un valore simile a `eu10` o `us10`. Ad esempio, se `url` è `https://eu10.revenue.cloud.sap/api`, è necessario `eu10`. |

## Guardrail {#guardrails}

Le richieste API a [!DNL SAP Cloud Management service] sono soggette a [Limiti di frequenza](https://help.sap.com/docs/btp/sap-business-technology-platform/account-administration-rate-limiting). Quando il limite di frequenza viene superato, verrà rilevato un codice di stato di risposta `HTTP 429 Too Many Requests`.

## Identità supportate {#supported-identities}

[!DNL SAP Commerce] supporta l&#39;aggiornamento delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
| --- | --- | --- |
| `customerNumberSAP` | Identificatore del cliente individuale o aziendale già presente nell&#39;account [!DNL SAP Commerce]. | Obbligatorio |

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive tutti i tipi di pubblico che puoi esportare in questa destinazione.

Questa destinazione supporta l&#39;attivazione di tutti i tipi di pubblico generati tramite l&#39;Experience Platform [Servizio di segmentazione](../../../segmentation/home.md).

Questa destinazione supporta anche l’attivazione dei tipi di pubblico descritti nella tabella seguente.

| Tipo di pubblico | Supportato | Descrizione |
| ------------- | --------- | ----------- |
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li>Stai esportando tutti i membri di un pubblico, insieme ai campi di schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base al mapping dei campi.</li><li> Per ogni pubblico selezionato in Platform, l&#39;attributo aggiuntivo [!DNL SAP Commerce] corrispondente viene aggiornato con il relativo stato da Platform.</li></ul> |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | <ul><li>Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Quando un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Gestione destinazioni]** [controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

In **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**, cerca [!DNL SAP Commerce]. In alternativa, è possibile individuarlo nella categoria **[!UICONTROL eCommerce]**.

### Autenticarsi nella destinazione {#authenticate}

Compila i campi obbligatori di seguito. Per ulteriori informazioni, consultare la sezione [Generare una chiave di servizio](#prerequisites-service-key).

| Campo | Descrizione |
| --- | --- |
| **[!UICONTROL ID client]** | Il valore di `clientId` dalla chiave del servizio. |
| **[!UICONTROL Segreto client]** | Il valore di `clientSecret` dalla chiave del servizio. |
| **[!UICONTROL Endpoint]** | Il valore di `url` dalla chiave del servizio è simile a `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| **[!UICONTROL Area]** | La posizione del centro dati. L&#39;area è presente in `url` e ha un valore simile a `eu10` o `us10`. Ad esempio, se `url` è `https://eu10.revenue.cloud.sap/api`, è necessario `eu10`. |

Per eseguire l&#39;autenticazione nella destinazione, selezionare **[!UICONTROL Connetti alla destinazione]**.
![Immagine dall&#39;interfaccia utente di Platform che mostra come eseguire l&#39;autenticazione nella destinazione.](../../assets/catalog/ecommerce/sap-commerce/authenticate-destination.png)

Se i dettagli forniti sono validi, nell&#39;interfaccia utente viene visualizzato lo stato **[!UICONTROL Connesso]** con un segno di spunta verde. A questo punto è possibile procedere al passaggio successivo.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Immagine dall&#39;interfaccia utente di Platform che mostra i dettagli della destinazione da compilare dopo l&#39;autenticazione.](../../assets/catalog/ecommerce/sap-commerce/destination-details.png)

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Tipo di cliente]**: seleziona ***Individuale*** o ***Aziendale*** a seconda delle entità del pubblico. Lo [!DNL SAP Subscription Billing] [schema](https://api.sap.com/api/BusinessPartner_APIs/schema) cambia i campi obbligatori in base a questa selezione mappata all&#39;attributo `customerType`. Se la selezione è ***Aziendale***, le mappature obbligatorie come `firstName` e `lastName` richieste per un singolo cliente verranno ignorate e `company` diventerà obbligatorio e viceversa.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

Per inviare correttamente i dati sul pubblico da Adobe Experience Platform alla destinazione [!DNL SAP Commerce], è necessario eseguire il passaggio di mappatura dei campi. La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione. Per mappare correttamente i campi XDM ai campi di destinazione [!DNL SAP Commerce], effettua le seguenti operazioni:

#### Mappa l&#39;identità `customerNumberSAP`

L&#39;identità `customerNumberSAP` è una mappatura obbligatoria per questa destinazione. Segui i passaggi seguenti per mapparla:

1. Nel passaggio **[!UICONTROL Mapping]**, seleziona **[!UICONTROL Aggiungi nuovo mapping]**. Ora è possibile visualizzare una nuova riga di mappatura sullo schermo.
   ![Schermata dell&#39;interfaccia utente di Platform con il pulsante Aggiungi nuova mappatura evidenziato.](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. Nella finestra **[!UICONTROL Seleziona campo di origine]**, scegli **[!UICONTROL Seleziona spazio dei nomi identità]** e seleziona `customerNumberSAP`.
   ![Schermata dell&#39;interfaccia utente di Platform che seleziona e-mail come attributo di origine da mappare come identità.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-identity.png)
1. Nella finestra **[!UICONTROL Seleziona campo di destinazione]**, scegli **[!UICONTROL Seleziona spazio dei nomi identità]** e seleziona l&#39;identità `customerNumber`.
   ![Schermata dell&#39;interfaccia utente di Platform che seleziona le e-mail come attributo di destinazione da mappare come identità.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-identity.png)

| Campo origine | Campo di destinazione | Obbligatorio |
| --- | --- | --- |
| `IdentityMap: customerNumberSAP` | `Identity: customerNumber` | Sì |

Di seguito è riportato un esempio con la mappatura di identità:
![Immagine dall&#39;interfaccia utente di Platform che mostra un esempio di mapping di identità customerNumber.](../../assets/catalog/ecommerce/sap-commerce/mapping-identities.png)

#### Mappatura degli attributi

Per aggiungere altri attributi da aggiornare tra lo schema del profilo XDM e l&#39;account [!DNL SAP Subscription Billing], ripeti i passaggi seguenti:

1. Nel passaggio **[!UICONTROL Mapping]**, seleziona **[!UICONTROL Aggiungi nuovo mapping]**. Ora è possibile visualizzare una nuova riga di mappatura sullo schermo.
   ![Schermata dell&#39;interfaccia utente di Platform con il pulsante Aggiungi nuova mappatura evidenziato.](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. Nella finestra **[!UICONTROL Seleziona campo di origine]**, scegli la categoria **[!UICONTROL Seleziona attributi]** e seleziona l&#39;attributo XDM.
   ![Schermata dell&#39;interfaccia utente di Platform che seleziona Cognome come attributo di origine.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-attribute.png)
1. Nella finestra **[!UICONTROL Seleziona campo di destinazione]**, scegli la categoria **[!UICONTROL Seleziona attributi personalizzati]** e digita il nome dell&#39;attributo [!DNL SAP Subscription Billing] dall&#39;elenco degli attributi [schema](https://api.sap.com/api/BusinessPartner_APIs/schema) del cliente.
   ![Schermata dell&#39;interfaccia utente di Platform in cui lastName è definito come attributo di destinazione.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-attribute.png)

>[!IMPORTANT]
>
> I nomi dei campi di destinazione fanno distinzione tra maiuscole e minuscole e devono corrispondere ai nomi degli attributi [!DNL SAP Subscription Billing]. L&#39;unica eccezione è `country`, dove è necessario utilizzare `countryCode`. [!DNL SAP Subscription Billing] supporta i codici paese alpha-2 (ISO 3166). Il valore fa distinzione tra maiuscole e minuscole e deve essere compreso tra 0 e 3 caratteri. Assicurarsi quindi di fornire esattamente come definito in caso di errori: `The country code {} does not exist` o `size must be between 0 and 3`.

#### Mappa gli attributi `mandatory` per il tipo di cliente selezionato

I mapping di attributi obbligatori dipendono dal **[!UICONTROL Tipo di cliente]** selezionato. Per mappare gli attributi obbligatori, seleziona una delle opzioni seguenti:

>[!BEGINTABS]

>[!TAB Cliente singolo]

| Campo origine | Campo di destinazione | Obbligatorio |
| --- | --- | --- |
| `xdm: person.lastName` | `Attribute: lastName` | Sì |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | Sì |

>[!TAB Cliente aziendale]

| Campo origine | Campo di destinazione | Obbligatorio |
| --- | --- | --- |
| `xdm: b2b.companyName` | `Attribute: company` | Sì |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | Sì |

>[!ENDTABS]

#### Mappatura di attributi aggiuntivi

Puoi quindi aggiungere altre mappature tra lo schema del profilo XDM e gli attributi [!DNL SAP Subscription Billing] [schema](https://api.sap.com/api/BusinessPartner_APIs/schema) per un cliente, come illustrato di seguito:

>[!BEGINTABS]

>[!TAB Cliente singolo]

| Campo origine | Campo di destinazione | Obbligatorio |
| --- | --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstName` | No |
| `xdm: workAddress.street1` | `Attribute: street` | No |
| `xdm: workAddress.city` | `Attribute: city` | No |

Di seguito è riportato un esempio con mappature di attributi obbligatorie e facoltative in cui il cliente è un singolo utente:
![Immagine dall&#39;interfaccia utente di Platform che mostra un esempio con mapping di attributi obbligatori e facoltativi in cui il cliente è un singolo utente.](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-individual.png)

>[!TAB Cliente aziendale]

| Campo origine | Campo di destinazione | Obbligatorio |
| --- | --- | --- |
| `xdm: workAddress.street1` | `Attribute: street` | No |
| `xdm: workAddress.city` | `Attribute: city` | No |

Di seguito è riportato un esempio con mappature di attributi obbligatorie e facoltative in cui il cliente è un’azienda:
![Immagine dall&#39;interfaccia utente di Platform che mostra un esempio con mapping di attributi obbligatori e facoltativi in cui il cliente è un&#39;azienda.](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-corporate.png)

>[!ENDTABS]

Al termine della fornitura dei mapping per la connessione di destinazione, selezionare **[!UICONTROL Avanti]**.

### Esempio di esportazione e pianificazione di un pubblico {#schedule-segment-export-example}

Quando esegui il passaggio [Pianifica esportazione pubblico](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling), devi mappare manualmente i tipi di pubblico di Platform agli [attributi](#prerequisites-attribute) in [!DNL SAP Subscription Billing].

Di seguito è riportato un esempio del passaggio di esportazione Pianifica pubblico, con la posizione dell&#39;[!DNL SAP Commerce] **[!UICONTROL ID mappatura]** evidenziato:
![Immagine da Platform che mostra l&#39;esportazione del pubblico di pianificazione con ID di mappatura popolati.](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export.png)

A questo scopo, seleziona ogni segmento, quindi immetti il nome del riferimento personalizzato da [!DNL SAP Subscription Billing] nel campo del connettore di destinazione [!DNL SAP Commerce] **[!UICONTROL ID mappatura]**. Per istruzioni sulla creazione di riferimenti personalizzati, consulta la sezione [Creare riferimenti personalizzati in [!DNL SAP Subscription Billing]](#prerequisites-custom-reference).

>[!IMPORTANT]
>
> Non utilizzare l’etichetta di riferimento personalizzata come valore.
>![Immagine che indica che non si deve utilizzare il valore dell&#39;etichetta di riferimento personalizzata per la mappatura.](../../assets/catalog/ecommerce/sap-commerce/custom-reference-dont-use-label-for-mapping.png)

Se ad esempio il pubblico Experience Platform selezionato è `sap_audience1` e si desidera che il relativo stato venga aggiornato nel riferimento personalizzato `SAP_1` di [!DNL SAP Subscription Billing], specificare questo valore nel campo [!DNL SAP_Commerce] **[!UICONTROL ID mappatura]**.

Di seguito è riportato un esempio di **[!UICONTROL tipo di riferimento]** da [!DNL SAP Subscription Billing]:
![Immagine che mostra dove creare un riferimento personalizzato nella fatturazione dell&#39;abbonamento SAP.](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

Di seguito è riportato un esempio del passaggio Pianifica esportazione pubblico, con un pubblico selezionato e il corrispondente [!DNL SAP Commerce] **[!UICONTROL ID mappatura]** evidenziato:
![Immagine da Platform che mostra l&#39;esportazione del pubblico di pianificazione con ID di mappatura popolati.](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export-example.png)

Come mostrato, il valore all&#39;interno del campo **[!UICONTROL ID mappatura]** deve corrispondere esattamente al valore [!DNL SAP Subscription Billing] **[!UICONTROL Tipo riferimento]**.

Ripeti questa sezione per ogni pubblico di Platform attivato.

In base all’immagine mostrata sopra in cui hai selezionato due tipi di pubblico, la mappatura sarà la seguente:

| Nome pubblico [!DNL SAP Commerce] | [!DNL SAP Subscription Billing] **[!UICONTROL Tipo di riferimento]** | [!DNL SAP Commerce] **[!UICONTROL Valore di mappatura ID]** |
| --- | --- | --- |
| sap_audience1 | `SAP_1` | `SAP_1` |
| Pubblico SAP2 | `SAP_2` | `SAP_2` |

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare di aver impostato correttamente la destinazione, segui i passaggi seguenti:

Accedi all&#39;account [!DNL SAP Subscription Billing], quindi passa alla pagina **[!UICONTROL Contatti]** per verificare gli stati del pubblico. L’elenco può essere configurato in modo da visualizzare le colonne per i riferimenti personalizzati e gli stati del pubblico corrispondenti.
![Immagine della fatturazione dell&#39;abbonamento SAP che mostra la pagina di panoramica del cliente con intestazioni di colonna che mostrano il nome del pubblico e le celle dello stato del pubblico](../../assets/catalog/ecommerce/sap-commerce/customer-overview.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Errori e risoluzione problemi {#errors-and-troubleshooting}

Per un elenco dei possibili tipi di errore e dei relativi codici di risposta, fare riferimento alla pagina della documentazione [[!DNL SAP Subscription Billing] Tipi di errore](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/1a6a0dd6129c48e8b235190a1b5409fa.html).

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate ulteriori informazioni utili dalla documentazione di [!DNL SAP]:
* [Fatturazione sottoscrizione SAP integrata](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/e4b8badf7d124026991e4ab6b57d2a33.html)

### Changelog

Questa sezione acquisisce le funzionalità e i significativi aggiornamenti alla documentazione apportati al connettore di destinazione.

+++ Visualizza changelog

| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Gennaio 2024 | Versione iniziale | Versione di destinazione iniziale e pubblicazione della documentazione. |

{style="table-layout:auto"}

+++
