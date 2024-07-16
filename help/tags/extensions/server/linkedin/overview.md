---
title: Estensione di inoltro eventi API LinkedIn Conversions
description: Questa estensione per l’inoltro di eventi Adobe Experience Platform consente di misurare le prestazioni della campagna di marketing LinkedIn.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 411e7b77-081e-4139-ba34-04468e519ea5
source-git-commit: 0d6ade1a0b6c00a4f87395d476dd7e7915489ea5
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 2%

---

# Estensione API Conversions [!DNL LinkedIn]

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) è uno strumento di monitoraggio delle conversioni che crea una connessione diretta tra i dati di marketing dal server dell&#39;inserzionista e [!DNL LinkedIn]. Ciò consente agli inserzionisti di valutare l&#39;efficacia delle campagne di marketing [!DNL LinkedIn] indipendentemente dalla posizione della conversione e di utilizzare queste informazioni per promuovere l&#39;ottimizzazione della campagna. L&#39;estensione [!DNL LinkedIn Conversions API] può contribuire a rafforzare le prestazioni e a ridurre i costi per azione con un&#39;attribuzione più completa, una maggiore affidabilità dei dati e una distribuzione ottimizzata.

## Prerequisiti {#prerequisites}

Devi [creare una regola di conversione](https://www.linkedin.com/help/lms/answer/a1657171) nel tuo account [!DNL LinkedIn Campaign Manager]. [!DNL Adobe] consiglia di includere &quot;CAPI&quot; all&#39;inizio del nome della regola di conversazione per distinguerlo dagli altri tipi di regole di conversione configurati.

### Creare un segreto e un elemento dati

Crea un nuovo [!DNL LinkedIn] [segreto di inoltro eventi](../../../ui/event-forwarding/secrets.md) e fornisci un nome univoco che indichi il membro che esegue l&#39;autenticazione. Verrà utilizzato per autenticare la connessione al tuo account mantenendo protetto il valore.

Quindi, [crea un elemento dati](../../../ui/managing-resources/data-elements.md#create-a-data-element) utilizzando l&#39;estensione [!UICONTROL Core] e un tipo di elemento dati [!UICONTROL Secret] per fare riferimento al segreto `LinkedIn` appena creato.

## Installa e configura l&#39;estensione [!DNL LinkedIn] {#install}

Per installare l&#39;estensione, [crea una proprietà di inoltro eventi](../../../ui/event-forwarding/overview.md#properties) o seleziona una proprietà esistente da modificare.

Seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. Nella scheda **[!UICONTROL Catalogo]**, seleziona l&#39;estensione **[!UICONTROL LinkedIn]**, quindi seleziona **[!UICONTROL Installa]**.

![Il catalogo delle estensioni mostra la scheda delle estensioni [!DNL LinkedIn] che evidenzia l&#39;installazione.](../../../images/extensions/server/linkedin/install-extension.png)

Nella schermata successiva, immettere il segreto dell&#39;elemento dati creato in precedenza nel campo `Access Token`. Il segreto dell&#39;elemento dati conterrà il token OAuth 2 [!DNL LinkedIn]. Al termine, seleziona **[!UICONTROL Salva]**.

![Pagina di configurazione dell&#39;estensione [!DNL LinkedIn] con il campo [!UICONTROL Token di accesso] e [!UICONTROL Salva] evidenziati.](../../../images/extensions/server/linkedin/configure-extension.png)

## Crea una regola [!DNL Send Conversion] {#tracking-rule}

Una volta configurati tutti gli elementi dati, puoi iniziare a creare regole di inoltro degli eventi che determinano quando e come verranno inviati gli eventi a [!DNL LinkedIn].

Crea una nuova [regola](../../../ui/managing-resources/rules.md) di inoltro eventi nella proprietà di inoltro eventi. In **[!UICONTROL Azioni]**, aggiungi una nuova azione e imposta l&#39;estensione su **[!UICONTROL LinkedIn]**. Quindi, selezionare **[!UICONTROL Invia conversione]** per **[!UICONTROL Tipo azione]**.

![Visualizzazione delle regole di proprietà di inoltro eventi, con i campi necessari per aggiungere una configurazione dell&#39;azione della regola di inoltro eventi evidenziati.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

Dopo la selezione, vengono visualizzati controlli aggiuntivi per configurare ulteriormente l’evento. Seleziona **[!UICONTROL Mantieni modifiche]** per salvare la regola.

**[!UICONTROL Dati utente]**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL E-mail] | Indirizzo e-mail del contatto associato all’evento di conversione. Il valore e-mail verrà codificato dal codice di estensione in SHA256, a meno che il valore fornito non sia già una stringa SHA256. |
| [!UICONTROL UUID tracciamento annunci prime parti LinkedIn] | Questo è un ID cookie di prima parte. Gli inserzionisti devono abilitare il tracciamento avanzato delle conversioni da [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) per attivare i cookie di prime parti che aggiungono un parametro dell&#39;ID clic `li_fat_id` agli URL di clic. |
| [!UICONTROL Dati informazioni cliente] | Questo campo contiene un oggetto JSON con attributi aggiuntivi che verranno inviati insieme al messaggio.<br><br>Con l&#39;opzione **[!UICONTROL Raw]**, puoi incollare l&#39;oggetto JSON direttamente nel campo di testo fornito, oppure puoi selezionare l&#39;icona dell&#39;elemento dati (![icona del set di dati](../../../images/extensions/server/aws/data-element-icon.png)) per effettuare una selezione da un elenco di elementi dati esistenti per rappresentare i dati.<br><br>È inoltre possibile utilizzare l&#39;opzione **[!UICONTROL Editor coppie chiave-valore JSON]** per aggiungere manualmente ogni coppia chiave-valore tramite un editor di interfaccia utente. Ogni valore può essere rappresentato da un input non elaborato, oppure è possibile selezionare un elemento dati. I valori chiave accettati sono: `firstName`, `lastName`, `companyName`, `title` e `country`. |

{style="table-layout:auto"}

![La sezione [!DNL User Data] che mostra l&#39;input di dati di esempio nei campi.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL Dati conversione]**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL Conversione] | ID della regola di conversione creata in [LinkedIn Campaign Manager](https://www.linkedin.com/help/lms/answer/a1657171). Selezionare la regola di conversione per ottenere l&#39;ID, quindi copiare l&#39;ID dall&#39;URL del browser (ad esempio, `/campaignmanager/accounts/508111232/conversions/15588877`) come `/conversions/<id>`. |
| [!UICONTROL Tempo di conversione] | Ogni timestamp in millisecondi in cui si è verificato l’evento di conversione. <br><br> Nota: se l&#39;origine registra il timestamp di conversione in secondi, inserire 000 alla fine per trasformarlo in millisecondi. |
| [!UICONTROL Valuta] | Codice valuta in formato ISO. |
| [!UICONTROL Importo] | Valore della conversione in stringa decimale (ad esempio, &quot;100.05&quot;). |
| [!UICONTROL ID evento] | L’ID univoco generato dagli inserzionisti per indicare ogni evento. Questo campo è facoltativo ed è utilizzato per la [deduplicazione](https://learn.microsoft.com/en-us/linkedin/marketing/conversions/deduplication?view=li-lms-2024-02). |

{style="table-layout:auto"}

![La sezione [!DNL Conversion Data] che mostra dati di esempio nei campi.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL Sostituzioni configurazione]**

>NOTA
>
>Il campo [!UICONTROL Sostituzioni configurazione] consente a un utente di impostare un token di accesso [!DNL LinkedIn] diverso in ogni regola, consentendo a ogni regola di utilizzare un token di accesso che può avere accesso a diversi account annuncio [!DNL LinkedIn].

| Input | Descrizione |
| --- | --- |
| [!UICONTROL Token di accesso] | Il token di accesso [!DNL LinkedIn]. |

![La sezione [!DNL Configuration Overrides] che mostra l&#39;input di dati di esempio nel campo.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## Passaggi successivi

Questa guida illustra come inviare dati a [!DNL LinkedIn] utilizzando l&#39;estensione di inoltro eventi [!DNL LinkedIn Conversions API]. Per ulteriori informazioni sulle funzionalità di inoltro eventi in [!DNL Adobe Experience Platform], leggere la [panoramica sull&#39;inoltro eventi](../../../ui/event-forwarding/overview.md).

Per informazioni dettagliate su come eseguire il debug dell&#39;implementazione utilizzando lo strumento di monitoraggio Experience Platform Debugger e inoltro eventi, leggere la [panoramica Adobe Experience Platform Debugger](../../../../debugger/home.md) e le [attività di monitoraggio nell&#39;inoltro eventi](../../../ui/event-forwarding/monitoring.md).
