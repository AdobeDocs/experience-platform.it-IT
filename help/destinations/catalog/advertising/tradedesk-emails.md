---
title: Il Trade Desk - Connessione CRM
description: Attiva i profili nel tuo account di Trade Desk per il targeting e l’eliminazione del pubblico in base ai dati CRM.
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 5%

---

# Connessione [!DNL Trade Desk] - CRM

>[!IMPORTANT]
>
>Con il rilascio dell’EUID (European Unified ID), nel [catalogo delle destinazioni](/help/destinations/catalog/overview.md) ora vengono visualizzate due destinazioni [!DNL The Trade Desk - CRM].
>* Se i dati vengono originati nell’UE, utilizza la destinazione **[!DNL The Trade Desk - CRM (EU)]**.
>* Se i dati vengono originati nelle aree geografiche APAC o NAMER, utilizza la destinazione **[!DNL The Trade Desk - CRM (NAMER & APAC)]**.
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team *[!DNL Trade Desk]*. Per richieste di informazioni o richieste di aggiornamento, contatta il tuo rappresentante [!DNL Trade Desk].

## Panoramica {#overview}

Scopri come attivare i profili nell&#39;account [!DNL Trade Desk] per il targeting e l&#39;eliminazione del pubblico in base ai dati CRM.

Questo connettore invia dati all&#39;endpoint di prime parti [!DNL The Trade Desk]. L&#39;integrazione tra Adobe Experience Platform e [!DNL The Trade Desk] non supporta l&#39;esportazione dei dati nell&#39;endpoint di terze parti [!DNL The Trade Desk].

[!DNL The Trade Desk(TTD)] non gestisce direttamente il file di caricamento degli indirizzi e-mail in alcun momento e [!DNL The Trade Desk] non memorizza le e-mail non elaborate (senza hash).

>[!TIP]
>
>Utilizza [!DNL The Trade Desk] destinazioni CRM per la mappatura dei dati CRM, ad esempio e-mail o indirizzo e-mail con hash. Utilizza [altra destinazione Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) nel catalogo Adobe Experience Platform per cookie e mappature ID dispositivo.

## Prerequisiti {#prerequisites}

>[!IMPORTANT]
>
>Prima di poter attivare i tipi di pubblico per il Trade Desk, è necessario contattare l&#39;account manager [!DNL Trade Desk] per firmare il contratto di onboarding CRM. [!DNL The Trade Desk] abiliterà l&#39;uso di UID2/EUID e condividerà altri dettagli per aiutarti a configurare la tua destinazione.

## Requisiti di corrispondenza ID {#id-matching-requirements}

A seconda del tipo di ID inseriti in Adobe Experience Platform, devi rispettare i requisiti corrispondenti. Per ulteriori informazioni, consulta la [panoramica dello spazio dei nomi delle identità](/help/identity-service/features/namespaces.md).

## Identità supportate {#supported-identities}

[!DNL The Trade Desk] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Segui le istruzioni riportate nella sezione sui requisiti di corrispondenza ID e utilizza gli spazi dei nomi appropriati rispettivamente per gli indirizzi e-mail in testo normale e con hash.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| E-mail | Indirizzi e-mail (testo non crittografato) | Immettere `email` come identità di destinazione se l&#39;identità di origine è uno spazio dei nomi o un attributo di posta elettronica. |
| Email_LC_SHA256 | Gli indirizzi e-mail devono avere un hash utilizzando SHA256 e lettere minuscole. Non potrai modificare questa impostazione in un secondo momento. | Immettere `hashed_email` come identità di destinazione se l&#39;identità di origine è uno spazio dei nomi o un attributo Email_LC_SHA256. |

{style="table-layout:auto"}

## Requisiti di hashing delle e-mail {#hashing-requirements}

Puoi eseguire l’hashing degli indirizzi e-mail prima di acquisirli in Adobe Experience Platform o utilizzare indirizzi e-mail non elaborati.

Per informazioni sull&#39;acquisizione di indirizzi e-mail in Experience Platform, consulta la [panoramica sull&#39;acquisizione batch](/help/ingestion/batch-ingestion/overview.md).

Se scegli di eseguire l’hash degli indirizzi e-mail da solo, assicurati di soddisfare i seguenti requisiti:

* Rimuovere gli spazi iniziali e finali.
* Converte tutti i caratteri ASCII in minuscolo.
* In `gmail.com` indirizzi e-mail, rimuovi i seguenti caratteri dalla parte del nome utente dell&#39;indirizzo e-mail:
   * Il punto (. (codice ASCII 46). Ad esempio, normalizzare `jane.doe@gmail.com` in `janedoe@gmail.com`.
   * Il segno più (+ (codice ASCII 43)) e tutti i caratteri successivi. Ad esempio, normalizzare `janedoe+home@gmail.com` in `janedoe@gmail.com`.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (e-mail o e-mail con hash) utilizzati nella destinazione Trade Desk. |
| Frequenza di esportazione | **[!UICONTROL Batch giornaliero]** | Poiché un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il profilo (identità) viene aggiornato una volta al giorno a valle della piattaforma di destinazione. Ulteriori informazioni sulle [esportazioni batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

### Autentica nella destinazione {#authenticate}

La destinazione CRM [!DNL The Trade Desk] è un caricamento di file batch giornaliero e non richiede l&#39;autenticazione da parte dell&#39;utente.

### Inserisci i dettagli della destinazione {#fill-in-details}

Prima di poter inviare o attivare i dati sul pubblico a una destinazione, devi impostare una connessione alla tua piattaforma di destinazione. Durante la [configurazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Tipo di account]**: scegliere l&#39;opzione **[!UICONTROL Account esistente]**.
* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID inserzionista]**: [!DNL Trade Desk Advertiser ID], che può essere condiviso dal tuo Account Manager [!DNL Trade Desk] o che si trova in [!DNL Advertiser Preferences] nell&#39;interfaccia utente [!DNL Trade Desk].

![Schermata dell&#39;interfaccia utente di Experience Platform che mostra come compilare i dettagli della destinazione.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Quando ci si connette alla destinazione, l’impostazione di un criterio di governance dei dati è completamente facoltativa. Per ulteriori dettagli, consulta la [panoramica sulla governance dei dati](/help/data-governance/policies/overview.md) di Experience Platform.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in una destinazione.

Nella pagina **[!UICONTROL Pianificazione]** è possibile configurare la pianificazione e i nomi dei file per ogni pubblico che si sta esportando. La configurazione della pianificazione è obbligatoria, ma il nome del file è facoltativo.

![Schermata dell&#39;interfaccia utente di Experience Platform per pianificare l&#39;attivazione del pubblico.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Tutti i tipi di pubblico attivati nella destinazione CRM [!DNL The Trade Desk] vengono automaticamente impostati su una frequenza giornaliera e su un&#39;esportazione di file completa.

![Schermata dell&#39;interfaccia utente di Experience Platform per pianificare l&#39;attivazione del pubblico.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

Nella pagina **[!UICONTROL Mapping]** è necessario selezionare gli attributi o gli spazi dei nomi delle identità dalla colonna di origine e mappare alla colonna di destinazione.

![Schermata dell&#39;interfaccia utente di Experience Platform per mappare l&#39;attivazione del pubblico.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Di seguito è riportato un esempio di mapping di identità corretto durante l&#39;attivazione di tipi di pubblico nella destinazione CRM [!DNL The Trade Desk].

>[!IMPORTANT]
>
> La destinazione CRM [!DNL The Trade Desk] non accetta indirizzi e-mail non elaborati e con hash come identità nello stesso flusso di attivazione. Crea flussi di attivazione separati per gli indirizzi e-mail non elaborati e con hash.

Selezione dei campi di origine:

* Seleziona lo spazio dei nomi o l&#39;attributo `Email` come identità di origine se utilizzi l&#39;indirizzo e-mail non elaborato al momento dell&#39;acquisizione dei dati.
* Se all&#39;inserimento dei dati in Experience Platform si esegue l&#39;hashing degli indirizzi e-mail dei clienti, seleziona lo spazio dei nomi o l&#39;attributo `Email_LC_SHA256` come identità di origine.

Selezione dei campi di destinazione:

* Immettere `email` come identità di destinazione quando lo spazio dei nomi o l&#39;attributo di origine è `Email`.
* Immettere `hashed_email` come identità di destinazione quando lo spazio dei nomi o l&#39;attributo di origine è `Email_LC_SHA256`.

## Convalida esportazione dati {#validate}

Per verificare che i dati vengano esportati correttamente da Experience Platform e in [!DNL The Trade Desk], trovare i tipi di pubblico nella sezione dati di Adobe 1PD all&#39;interno di [!DNL The Trade Desk] Data Management Platform (DMP). Di seguito sono riportati i passaggi per trovare l&#39;ID corrispondente nell&#39;interfaccia utente [!DNL Trade Desk]:

1. Selezionare innanzitutto la scheda **[!UICONTROL Dati]** e rivedere la sezione **[!UICONTROL Prime parti]**.
2. Scorri verso il basso la pagina, sotto **[!UICONTROL Dati importati]**, troverai il **[!UICONTROL riquadro 1PD di Adobe]**.
3. Fai clic sul riquadro**[!UICONTROL Adobe 1PD]** per visualizzare l&#39;elenco di tutti i tipi di pubblico attivati nella destinazione [!DNL Trade Desk] per l&#39;inserzionista. È inoltre possibile utilizzare la funzione di ricerca.
4. L&#39;ID segmento # di Experience Platform verrà visualizzato come Nome segmento nell&#39;interfaccia utente [!DNL Trade Desk].

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
