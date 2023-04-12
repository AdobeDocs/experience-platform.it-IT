---
title: Proprietà
description: Scopri come Adobe Experience Platform organizza e raggruppa le estensioni, gli ambienti e le librerie per la tua organizzazione.
exl-id: e5b4a853-c23e-498c-9e20-e773ea1de88b
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 95%

---

# Proprietà

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

## Proprietà web

Una proprietà web è una raccolta di regole, elementi dati, estensioni configurate, ambienti e librerie. Ogni proprietà web ha un proprio set di codici da incorporare e può essere distribuita su qualsiasi numero di siti web distinti (con domini diversi).

## Proprietà mobili

Un tipo di proprietà mobile può contenere più applicazioni. Ad esempio, in una proprietà mobile puoi gestire lo stesso set di regole ed estensioni tra più applicazioni iOS e Android.

## Best practice per la pianificazione delle proprietà {#best-practices-for-planning-properties}

Ogni implementazione di tag in Adobe Experience Platform può essere molto diversa. Possiedono un’ampia varietà di esigenze di raccolta dati, utilizzo delle variabili, estensioni, tag di terze parti, altri sistemi e tecnologie, persone, team, aree geografiche e così via. Devi strutturare le proprietà in modo che corrispondano al flusso di lavoro e ai processi della tua organizzazione.

Considera quanto segue durante la pianificazione delle proprietà:

* Struttura del codice
* Dati
* Variabili
* Estensioni, tag e sistemi
* Persone

### Struttura del codice

I siti sono basati su HTML, le app mobile sul codice. Se i modelli HTML o le basi di codice sottostanti sono gli stessi per più siti e applicazioni, è consigliabile utilizzare una singola proprietà tag per gestire più siti o app.

### Dati

I dati che raccoglierai in tutti i tuoi siti Web e applicazioni sono molto simili, simili o univoci?

Se i dati da raccogliere sono simili, potrebbe essere meglio raggruppare tali siti o applicazioni in una proprietà per evitare di duplicare le regole o copiarle da una proprietà all&#39;altra.

Se invece ogni sito o applicazione ha esigenze di raccolta dati diverse, potrebbe essere preferibile usare proprietà distinte. Questo metodo ti consente di controllare la raccolta dei dati in modo più specifico, senza utilizzare grandi quantità di logica condizionale negli script personalizzati.

### Variabili

Così come i dati, le variabili che imposterai in [!DNL Analytics] e altre estensioni sono molto simili, simili o univoche?

Ad esempio, se utilizzi eVar27 per lo stesso valore di origine in tutti i siti Web o applicazioni, è meglio raggruppare tali siti o applicazioni in modo da poter impostare le variabili comuni in una sola proprietà.

### Estensioni, tag e sistemi

Le estensioni, i tag e i sistemi che stai per implementare sono molto simili, in parte simili o univoci?

Se le estensioni, i tag e i sistemi che stai per implementare sono molto simili nei vari siti o applicazioni, puoi includerli nella stessa proprietà.

Se distribuisci [!DNL Adobe Analytics] in un solo sito o in un&#39;applicazione e anche gli altri tag ed estensioni sono univoci, puoi creare proprietà separate per avere un maggiore controllo.

Ad esempio, se distribuisci [!DNL Adobe Analytics], [!DNL Target] e le stesse estensioni di terze parti in tutti i siti o applicazioni, è un buon motivo per raggrupparli.

### Persone

I singoli utenti, i team e le organizzazioni che lavorano in Adobe Experience Platform avranno bisogno dell’accesso a tutti i tuoi siti web e applicazioni, ad alcuni di essi o solo a uno?

Le funzioni di User Management ti consentono di assegnare ruoli diversi a utenti diversi per tutte le proprietà o in base alle proprietà. Se un utente dispone di diritti sufficienti può eseguire azioni amministrative in tutte le proprietà di tale organizzazione Platform. Tutti gli altri ruoli possono essere assegnati in base alla singola proprietà. Puoi anche nascondere una proprietà per determinati utenti (non amministratori) non assegnando loro alcun ruolo nella proprietà.

## Pagina Proprietà

Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Per il web esiste un solo codice di incorporamento di pubblicazione per ogni proprietà. Per i dispositivi mobili esiste un ID app di configurazione per proprietà.

Una proprietà può essere un raggruppamento di uno o più domini e sottodomini. Puoi gestire e tenere traccia di queste risorse in modo simile. Ad esempio, supponi di disporre di più siti Web basati su un modello e di voler tenere traccia delle stesse risorse su tutti. Puoi applicare una proprietà a più domini.

Il lato sinistro della schermata mostra le aziende dell&#39;organizzazione. Questa funzione è particolarmente utile se gestisci più account. Seleziona una società per visualizzarne le proprietà e i registri di controllo.

Ogni proprietà viene visualizzata nell&#39;elenco Proprietà.

L&#39;elenco Proprietà mostra le informazioni seguenti:

* Nome proprietà
* Piattaforma
* Stato

Fai clic su una proprietà per visualizzarne una panoramica. La panoramica mostra qualsiasi attività eseguita sulla proprietà. Inoltre, ne elenca le metriche e le estensioni.

## Creare o configurare una proprietà

Questa sezione fornisce indicazioni su come creare o configurare una proprietà tag in Adobe Experience Platform.

>[!NOTE]
>
>Solo un utente con i diritti sufficienti può creare una proprietà. Consulta [User Management](user-permissions.md).

Prima di iniziare, controlla [Best practice per la pianificazione delle proprietà](companies-and-properties.md#best-practices-for-planning-properties).

Passa alla pagina dell’azienda, quindi fai clic su **[!UICONTROL Aggiungi proprietà]**. In alternativa, seleziona una proprietà esistente dall’elenco e fai clic su **[!UICONTROL Configura]**.

![](../../images/property-settings.png)

### Per il Web

Segui le istruzioni per creare una proprietà web.

1. Compila i campi:

   **Name:** nome della proprietà.

   **Domains:** l’URL di base di tutti i siti in cui si intende distribuire questa proprietà.

1. (Avanzate) **[!UICONTROL Esegui componenti regola in sequenza]**. Seleziona questa casella di controllo per fare in modo che condizioni e azioni vengano eseguite dopo che quelle precedenti siano state completate.
1. (Avanzate) **[!UICONTROL Restituisci una stringa vuota per gli elementi di dati mancanti:]** se si fa riferimento a un elemento dati che non esiste in una libreria, in genere verrà restituito `undefined`. Seleziona questa casella di controllo se desideri invece che venga restituita una stringa vuota.
1. (Avanzate) **[!UICONTROL Configura per lo sviluppo di estensioni:]** seleziona questa casella di controllo se intendi installare estensioni di sviluppo create internamente.
1. Seleziona **[!UICONTROL Salva]**.

### Per dispositivi mobili

Segui le istruzioni per creare una proprietà mobile.

1. Compila i campi:

   * **Name:** nome della proprietà.
   * **Privacy:** per impostazione predefinita, l&#39;impostazione relativa alla privacy è impostata su Opted In (Consenti), ovvero che desideri che l&#39;SDK raccolga e invii dati alle soluzioni. Se selezioni Opted Out (Nega), per impostazione predefinita l&#39;SDK NON invierà dati alle soluzioni. Se selezioni l’impostazione Unknown (Sconosciuto), l’SDK farà in modo che l’applicazione chieda prima l’autorizzazione all’utente per la raccolta e la condivisione dei dati.

      >[!NOTE]
      >
      >Queste impostazioni possono essere ulteriormente controllate tramite API nell’app mobile.

   * **Use HTTPS:** scegli se tutte le comunicazioni di dati devono essere inviate tramite HTTP o HTTPS.

1. Seleziona **[!UICONTROL Salva]**.

Dopo la creazione della proprietà, Platform aggiunge automaticamente un host predefinito, un set di ambienti (Sviluppo, Staging e Produzione) e le estensioni predefinite.

## Eliminare una proprietà

Per eliminare una proprietà tag, effettua le seguenti operazioni.

>[!NOTE]
>
>La rimozione di una proprietà non può essere annullata. L&#39;autore della richiesta deve essere un utente di livello amministratore. Questa richiesta non può essere annullata.

1. Nell&#39;elenco Proprietà, seleziona la proprietà da eliminare.

   Puoi selezionare più proprietà da eliminare.

1. Fai clic su **[!UICONTROL Elimina]**, quindi conferma la rimozione della proprietà.
