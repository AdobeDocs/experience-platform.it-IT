---
title: Pubblico dell’account
description: Scopri come creare e utilizzare i tipi di pubblico dell’account per eseguire il targeting dei profili dell’account nelle destinazioni a valle.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Edizione B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: fd0a495d68d6a09ccca66c400993d2e72673321c
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 21%

---

# Pubblico dell’account

>[!AVAILABILITY]
>
>I tipi di pubblico dell&#39;account sono disponibili solo in [B2B edition di Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2b) e nell&#39;edizione [B2P di Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2p).

Con la segmentazione dell’account, Adobe Experience Platform ti consente di rendere l’esperienza di segmentazione del marketing completamente semplice e sofisticata, dal pubblico basato sulle persone a quello basato sull’account.

I tipi di pubblico dell’account possono essere utilizzati come input per le destinazioni basate su account, consentendoti di eseguire il targeting delle persone all’interno di tali account nei servizi a valle. Ad esempio, puoi utilizzare i tipi di pubblico basati sull&#39;account per recuperare i record di tutti gli account che **non** hanno informazioni di contatto per qualsiasi persona con il titolo di Chief Operating Officer (COO) o Chief Marketing Officer (CMO).

## Terminologia {#terminology}

Prima di iniziare a utilizzare i tipi di pubblico dell’account, esamina le differenze tra i diversi tipi di pubblico:

- **Tipi di pubblico dell&#39;account**: un pubblico dell&#39;account è un pubblico creato utilizzando i dati del profilo **account**. I dati del profilo account possono essere utilizzati per creare tipi di pubblico mirati alle persone negli account a valle. Per ulteriori informazioni sui profili dell&#39;account, leggere la [panoramica del profilo dell&#39;account](../../rtcdp/accounts/account-profile-overview.md).
- **Pubblico persone**: un pubblico persone è un pubblico creato utilizzando i dati del profilo **cliente**. I dati del profilo cliente possono essere utilizzati per creare tipi di pubblico mirati alla clientela della tua azienda. Per ulteriori informazioni sui profili cliente, leggere la [Panoramica del profilo cliente in tempo reale](../../profile/home.md).
- **Pubblico potenziale**: un pubblico potenziale è un pubblico creato utilizzando i dati del profilo **prospect**. I dati del profilo del potenziale cliente possono essere utilizzati per creare tipi di pubblico da utenti non autenticati. Per ulteriori informazioni sui profili di potenziali clienti, leggere la [panoramica dei profili di potenziali clienti](../../profile/ui/prospect-profile.md).

## Accesso {#access}

Per accedere ai tipi di pubblico dell&#39;account, seleziona **[!UICONTROL Tipi di pubblico]** nella sezione **[!UICONTROL Account]**.

![Il pulsante Tipi di pubblico è evidenziato nella sezione Account.](../images/ui/account-audiences/select.png)

Viene visualizzata la pagina [!UICONTROL Sfoglia], con un elenco di tutti i tipi di pubblico dell&#39;account per l&#39;organizzazione.

![Vengono visualizzati i tipi di pubblico dell&#39;account appartenenti all&#39;organizzazione.](../images/ui/account-audiences/browse.png)

Questa vista elenca informazioni sul pubblico, tra cui nome, conteggio dei profili, origine, stato del ciclo di vita, data di creazione e data dell’ultimo aggiornamento.

Puoi anche utilizzare la funzionalità di ricerca e filtro per cercare e ordinare rapidamente tipi di pubblico specifici per l’account. Ulteriori informazioni su questa funzione sono disponibili nella [Panoramica di Audience Portal](./audience-portal.md#manage-audiences).

## Crea pubblico {#create}

>[!NOTE]
>
>I tipi di pubblico dell&#39;account vengono valutati utilizzando la segmentazione **batch** e verranno valutati ogni 24 ore.

Per creare un pubblico per un account, seleziona **[!UICONTROL Crea pubblico]** nella pagina [!UICONTROL Sfoglia].

![Il pulsante [!UICONTROL Crea pubblico] è evidenziato nella pagina di navigazione del pubblico dell&#39;account.](../images/ui/account-audiences/select-create-audience.png)

Viene visualizzato il Generatore di segmenti. Gli attributi dell’account e i tipi di pubblico vengono visualizzati sulla barra di navigazione a sinistra. Nella scheda [!UICONTROL Attributi] puoi aggiungere attributi personalizzati e creati da Platform.

![Viene visualizzato il Generatore di segmenti. Si noti che vengono visualizzati solo gli attributi e i tipi di pubblico.](../images/ui/account-audiences/segment-builder.png)

Quando crei il pubblico dell&#39;account, tieni presente che gli eventi sono elencati in **[!UICONTROL Persone]**, anziché essere la loro scheda, poiché questi attributi sono associati alle persone.

![La posizione in cui trovare gli eventi, che si trova nella cartella [!UICONTROL Persone], è evidenziata.](../images/ui/account-audiences/attributes.png)

Nella scheda [!UICONTROL Tipi di pubblico] puoi aggiungere tipi di pubblico basati sulle persone creati in precedenza da utilizzare per la creazione del pubblico del tuo account.

![La scheda Tipi di pubblico nel Generatore di segmenti è evidenziata.](../images/ui/account-audiences/audiences.png)

Per ulteriori informazioni sull&#39;utilizzo del Generatore di segmenti, leggere la [Guida dell&#39;interfaccia utente del Generatore di segmenti](./segment-builder.md).

### Stabilire relazioni {#relationships}

Per impostazione predefinita, per il pubblico dell’account, l’interfaccia utente di Segment Builder mostra la relazione diretta tra un account e una persona. Tuttavia, per il pubblico dell’account sono disponibili altri tipi di relazione.

Per utilizzare i tipi di relazione alternativi, selezionare ![l&#39;icona delle impostazioni](../../images/icons/settings.png).

![L&#39;icona delle impostazioni è evidenziata nella sezione Campi.](../images/ui/account-audiences/select-settings.png)

Nella scheda [!UICONTROL Impostazioni], seleziona **[!UICONTROL Mostra selettori di relazioni]** nella sezione **[!UICONTROL Relazione di campi]**.

![L&#39;opzione Mostra selettori di relazioni è selezionata nella sezione Relazioni dei campi della scheda Impostazioni.](../images/ui/account-audiences/show-relation-selectors.png)

Seleziona di nuovo ![l&#39;icona impostazioni](../../images/icons/settings.png) per tornare alla scheda [!UICONTROL Campi]. È ora disponibile la sezione **[!UICONTROL Stabilire relazioni]**, che consente di stabilire come l&#39;account è connesso alla persona e come la persona è connessa all&#39;opportunità.

![Viene evidenziata la sezione Stabilire relazioni, in cui sono visualizzate le opzioni per la connessione di un account a una persona e per la connessione di una persona a un&#39;opportunità.](../images/ui/account-audiences/establish-relationships.png)

Quando connetti l’account alla persona, puoi scegliere tra le seguenti opzioni:

| Opzione | Descrizione |
| ------ | ----------- |
| Relazione diretta | Il collegamento diretto tra l’account e la persona. Specifica gli account a cui ogni persona è collegata tramite l&#39;array di valori `accountID` nell&#39;array `personComponents` nello schema persona. Questo percorso è il più utilizzato. |
| Relazione account-persona | Relazione tra l&#39;account e la persona, definita dall&#39;oggetto `accountPersonRelation`. Questo percorso consente inoltre a ogni persona di essere connessa a più account. Viene utilizzato quando l’organizzazione ha definito una tabella di relazione esplicita dai dati di origine. |
| Relazione opportunità-persona | Relazione tra l&#39;opportunità e la persona, definita dall&#39;oggetto `opportunityPersonRelation`. Consente di collegare la persona a un account passando dalla persona-opportunità all’opportunità all’account. Questo consente di descrivere in quali aziende la persona è associata alle opportunità. |

Quando connetti l’opportunità alla persona, puoi scegliere tra le seguenti opzioni:

| Opzione | Descrizione |
| ------ | ----------- |
| Account | Il collegamento diretto tra l’account e l’opportunità. Quando lo utilizzi in un pubblico di account, questo percorso collega tutte le persone dell’azienda all’opportunità. |
| Relazione opportunità-persona | La relazione tra l’opportunità e la persona, basata sull’oggetto opportunità-persona. Questo percorso collega solo le persone che sono state identificate come coinvolte in un’opportunità specifica a tale opportunità. |

Dopo aver stabilito la relazione desiderata, puoi aggiungere i tipi di pubblico necessari alla definizione del segmento.

## Attiva pubblico {#activate}

>[!NOTE]
>
>Solo un numero limitato di destinazioni supporta i tipi di pubblico dell’account. Prima di continuare, assicurati che la destinazione da attivare supporti i tipi di pubblico dell&#39;account.

Dopo aver creato il pubblico del tuo account, puoi attivarlo in altri servizi a valle.

Seleziona il pubblico da attivare, seguito da **[!UICONTROL Attiva nella destinazione]**.

![Il pulsante [!UICONTROL Attiva nella destinazione] è evidenziato nel menu Azioni rapide per il pubblico selezionato.](../images/ui/account-audiences/activate.png)

Viene visualizzata la pagina [!UICONTROL Attiva destinazione]. Per ulteriori informazioni sul processo di attivazione, incluse le destinazioni supportate e i dettagli sulle mappature dei campi, consulta l&#39;esercitazione [attivare i tipi di pubblico dell&#39;account](/help/destinations/ui/activate-account-audiences.md).

## Passaggi successivi {#next-steps}

Dopo aver letto questa guida, ora hai una migliore comprensione di come creare e utilizzare i tipi di pubblico del tuo account in Adobe Experience Platform. Per informazioni su come utilizzare altri tipi di pubblico in Platform, consulta la [Guida dell’interfaccia utente del servizio di segmentazione](./overview.md).

## Appendice {#appendix}

La sezione seguente fornisce informazioni aggiuntive sui tipi di pubblico dell’account.

### Convalida segmentazione account {#validation}

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_eventLookbackWindow"
>title="Errore intervallo massimo di lookback"
>abstract="L’intervallo massimo di lookback per gli eventi di Experience è di 30 giorni."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxDepth"
>title="Errore di profondità massima del contenitore nidificato"
>abstract="La profondità massima dei contenitori nidificati è **5**. Ciò significa che **non puoi** avere più di cinque contenitori nidificati durante la creazione del pubblico."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxBreadth"
>title="Errore quantità massima di regole"
>abstract="Il numero massimo di regole all’interno di un singolo contenitore è **5**. Questo significa che **non puoi** avere più di cinque regole in un singolo contenitore durante la creazione del pubblico."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_crossEntityMaxDepth"
>title="Errore quantità massima entità incrociate"
>abstract="Il numero massimo di entità incrociate utilizzabili all’interno di un singolo pubblico è **5**. Un’entità incrociata si verifica quando si passa da un’entità all’altra all’interno del pubblico. Ad esempio, passare da un account a una persona a un elenco di marketing."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowCustomEntity"
>title="Errore entità personalizzata"
>abstract="**Non** sono consentite entità personalizzate."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_b2bBuiltInEntities"
>title="Errore entità B2B non valida"
>abstract="È consentito utilizzare solo le seguenti entità B2B: `_xdm.context.account`, `_xdm.content.opportunity`, `_xdm.context.profile`, `_xdm.context.experienceevent`, `_xdm.context.account-person`, `_xdm.classes.opportunity-person`, `_xdm.classes.marketing-list-member`, `_xdm.classes.marketing-list`, `_xdm.context.campaign-member` e `_xdm.classes.campaign`."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_rhsMaxOptions"
>title="Errore valori massimi"
>abstract="Il numero massimo di valori che è possibile controllare per un singolo campo è **50**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByReference"
>title="Errore evento inSegment"
>abstract="Gli eventi inSegment **non** sono consentiti."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByValue"
>title="Errore evento inSegment"
>abstract="Gli eventi inSegment **non** sono consentiti."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowSequentialEvents"
>title="Errore eventi sequenziali"
>abstract="Gli eventi sequenziali **non** sono consentiti."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowMaps"
>title="Errore proprietà Map-type"
>abstract="Le proprietà Map-type **non** sono consentite."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxNestedAggregationDepth"
>title="Errore profondità massima entità nidificata"
>abstract="La profondità massima degli array nidificati è **5**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxObjectNestingLevel"
>title="Errore di quantità massima di oggetti nidificati"
>abstract="Il numero massimo di oggetti nidificati consentito è **10**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_generic"
>title="Violazione vincolo"
>abstract="Il pubblico viola un vincolo. Per ulteriori informazioni, leggi il documento collegato."

Quando si utilizzano i tipi di pubblico dell&#39;account, il pubblico **deve** rispettare i seguenti vincoli:

>[!NOTE]
>
>L&#39;elenco seguente mostra i vincoli **default** per i tipi di pubblico dell&#39;account. Questi valori **maggio** variano a seconda delle impostazioni implementate dall&#39;amministratore dell&#39;organizzazione.

- L&#39;intervallo di lookback massimo per gli eventi esperienza è **30 giorni**.
- La profondità massima dei contenitori nidificati è **5**.
   - Ciò significa che **non puoi** avere più di cinque contenitori nidificati durante la creazione del pubblico.
- Il numero massimo di regole in un singolo contenitore è **5**.
   - Ciò significa che il pubblico **non può** avere più di cinque regole che compongono il pubblico.
- Il numero massimo di entità incrociate utilizzabili è **5**.
   - Un’entità incrociata si verifica quando si passa da un’entità all’altra all’interno del pubblico. Ad esempio, passare da un account a una persona a un elenco di marketing.
- Impossibile utilizzare le entità personalizzate **1}.**
- Il numero massimo di valori che è possibile controllare per un singolo campo è **50**.
   - Ad esempio, se hai un campo &quot;Nome città&quot;, puoi confrontare tale valore con 50 nomi di città.
- Il pubblico dell&#39;account **non può** utilizzare `inSegment` eventi.
- Il pubblico dell&#39;account **non può** utilizzare eventi sequenziali.
- I tipi di pubblico dell&#39;account **non possono** utilizzare le mappe.
- La profondità massima degli array nidificati è **5**.
- Il numero massimo di oggetti nidificati è **10**.
