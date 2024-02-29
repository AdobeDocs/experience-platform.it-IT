---
title: Pubblico dell’account
description: Scopri come creare e utilizzare i tipi di pubblico dell’account per eseguire il targeting dei profili dell’account nelle destinazioni a valle.
badgeB2B: label="Edizione B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Edizione B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: 7d630c3673304060ad26375955602440a495f354
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 0%

---

# Pubblico dell’account

>[!AVAILABILITY]
>
>I tipi di pubblico dell’account sono disponibili solo in [Edizione B2B di Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2b) e [Edizione B2P di Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2p).

Con la segmentazione dell’account, Adobe Experience Platform ti consente di rendere l’esperienza di segmentazione del marketing completamente semplice e sofisticata, dal pubblico basato sulle persone a quello basato sull’account.

I tipi di pubblico dell’account possono essere utilizzati come input per le destinazioni basate su account, consentendoti di eseguire il targeting delle persone all’interno di tali account nei servizi a valle. Ad esempio, puoi utilizzare tipi di pubblico basati sull’account per recuperare i record di tutti gli account che lo fanno **non** disporre di informazioni di contatto per qualsiasi persona con il titolo di Chief Operating Officer (COO) o Chief Marketing Officer (CMO).

## Terminologia {#terminology}

Prima di iniziare a utilizzare i tipi di pubblico dell’account, esamina le differenze tra i diversi tipi di pubblico:

- **Pubblico dell’account**: un pubblico di tipo account è un pubblico che viene creato con **account** dati del profilo. I dati del profilo account possono essere utilizzati per creare tipi di pubblico mirati alle persone negli account a valle. Per ulteriori informazioni sui profili dell’account, consulta [panoramica del profilo account](../../rtcdp/accounts/account-profile-overview.md).
- **Pubblico persone**: un pubblico di tipo Persone è un pubblico che viene creato con **cliente** dati del profilo. I dati del profilo cliente possono essere utilizzati per creare tipi di pubblico mirati alla clientela della tua azienda. Per ulteriori informazioni sui profili dei clienti, consulta [Panoramica del profilo cliente in tempo reale](../../profile/home.md).
- **Pubblico potenziale**: un pubblico potenziale è un pubblico che viene creato con **potenziale cliente** dati del profilo. I dati del profilo del potenziale cliente possono essere utilizzati per creare tipi di pubblico da utenti non autenticati. Per ulteriori informazioni sui profili potenziali, consulta la sezione [panoramica del profilo di prospect](../../profile/ui/prospect-profile.md).

## Accesso {#access}

Per accedere ai tipi di pubblico dell’account, seleziona **[!UICONTROL Tipi di pubblico]** nel **[!UICONTROL Account]** sezione.

![Il pulsante Tipi di pubblico è evidenziato nella sezione Account.](../images/ui/account-audiences/select.png)

Il [!UICONTROL Sfoglia] viene visualizzata una pagina con un elenco di tutti i tipi di pubblico dell’account per l’organizzazione.

![Vengono visualizzati i tipi di pubblico dell’account appartenenti all’organizzazione.](../images/ui/account-audiences/browse.png)

Questa vista elenca informazioni sul pubblico, tra cui nome, conteggio dei profili, origine, stato del ciclo di vita, data di creazione e data dell’ultimo aggiornamento.

Puoi anche utilizzare la funzionalità di ricerca e filtro per cercare e ordinare rapidamente tipi di pubblico specifici per l’account. Ulteriori informazioni su questa funzione sono disponibili nella [guida all’interfaccia utente di segmentazione](./overview.md#manage-audiences).

## Creare un pubblico {#create}

>[!NOTE]
>
>I tipi di pubblico dell’account vengono valutati utilizzando **batch** e verranno valutati ogni 24 ore.

Per creare un pubblico di tipo account, seleziona **[!UICONTROL Creare un pubblico]** il [!UICONTROL Sfoglia] pagina.

![Il [!UICONTROL Creare un pubblico] nella pagina di navigazione del pubblico dell’account.](../images/ui/account-audiences/select-create-audience.png)

Viene visualizzato il Generatore di segmenti. Gli attributi dell’account e i tipi di pubblico vengono visualizzati sulla barra di navigazione a sinistra. Sotto [!UICONTROL Attributi] , puoi aggiungere attributi personalizzati e creati da Platform.

![Viene visualizzato il Generatore di segmenti. Vengono visualizzati solo gli attributi e i tipi di pubblico.](../images/ui/account-audiences/segment-builder.png)

Durante la creazione del pubblico dell’account, tieni presente che gli eventi sono elencati in **[!UICONTROL Persone]**, anziché essere la propria scheda, in quanto questi attributi sono associati alle persone.

![La posizione in cui trovare gli eventi, che si trova all’interno del [!UICONTROL Persone] cartella, viene evidenziato.](../images/ui/account-audiences/attributes.png)

Sotto [!UICONTROL Tipi di pubblico] , puoi aggiungere tipi di pubblico basati sulle persone creati in precedenza da utilizzare per la creazione del pubblico del tuo account.

![Viene evidenziata la scheda Tipi di pubblico nel Generatore di segmenti.](../images/ui/account-audiences/audiences.png)

Per ulteriori informazioni sull’utilizzo del Generatore di segmenti, consulta la sezione [Guida dell’interfaccia utente di Segment Builder](./segment-builder.md).

## Attiva pubblico {#activate}

>[!NOTE]
>
>Solo un numero limitato di destinazioni supporta i tipi di pubblico dell’account. Prima di continuare, assicurati che la destinazione da attivare supporti i tipi di pubblico dell&#39;account.

Dopo aver creato il pubblico del tuo account, puoi attivarlo in altri servizi a valle.

Seleziona il pubblico da attivare, seguito da **[!UICONTROL Attiva nella destinazione]**.

![Il [!UICONTROL Attiva nella destinazione] nel menu Azioni rapide per il pubblico selezionato.](../images/ui/account-audiences/activate.png)

Il [!UICONTROL Attiva destinazione] viene visualizzata. Per ulteriori informazioni sul processo di attivazione, comprese le destinazioni supportate e i dettagli sulle mappature dei campi, leggi [attivare il pubblico dell’account](/help/destinations/ui/activate-account-audiences.md) esercitazione.

## Passaggi successivi {#next-steps}

Dopo aver letto questa guida, ora hai una migliore comprensione di come creare e utilizzare i tipi di pubblico del tuo account in Adobe Experience Platform. Per scoprire come utilizzare altri tipi di pubblico in Platform, leggi la sezione [Guida dell’interfaccia utente di Segmentation Service](./overview.md).

## Appendice {#appendix}

La sezione seguente fornisce informazioni aggiuntive sui tipi di pubblico dell’account.

### Convalida segmentazione account {#validation}

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_eventLookbackWindow"
>title="Errore intervallo di lookback massimo"
>abstract="L’intervallo di lookback massimo per gli eventi esperienza è di 30 giorni."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxDepth"
>title="Errore di profondità massima del contenitore nidificato"
>abstract="La profondità massima dei contenitori nidificati è **5**. Ciò significa che **non può** avere più di cinque contenitori nidificati durante la creazione del pubblico."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxBreadth"
>title="Errore importo massimo regole"
>abstract="Il numero massimo di regole all’interno di un singolo contenitore è **5**. Questo significa che **non può** avere più di cinque regole in un singolo contenitore durante la creazione del pubblico."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_crossEntityMaxDepth"
>title="Errore importo massimo entità incrociata"
>abstract="Il numero massimo di entità incrociate utilizzabili all’interno di un singolo pubblico è **5**. Un’entità incrociata si verifica quando si passa da un’entità all’altra all’interno del pubblico. Ad esempio, passare da un account a una persona a un elenco di marketing."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowCustomEntity"
>title="Errore di entità personalizzata"
>abstract="Le entità personalizzate sono **non** consentito."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_b2bBuiltInEntities"
>title="Errore di entità B2B non valido"
>abstract="È consentito utilizzare solo le seguenti entità B2B: `_xdm.context.account`, `_xdm.content.opportunity`, `_xdm.context.profile`, `_xdm.context.experienceevent`, `_xdm.context.account-person`, `_xdm.classes.opportunity-person`, `_xdm.classes.marketing-list-member`, `_xdm.classes.marketing-list`, `_xdm.context.campaign-member`, e `_xdm.classes.campaign`."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_rhsMaxOptions"
>title="Errore di valori massimi"
>abstract="Il numero massimo di valori che è possibile controllare per un singolo campo è **50**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByReference"
>title="Errore evento inSegment"
>abstract="Gli eventi inSegment sono **non** consentito."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByValue"
>title="Errore evento inSegment"
>abstract="Gli eventi inSegment sono **non** consentito."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowSequentialEvents"
>title="Errore eventi sequenziali"
>abstract="Gli eventi sequenziali sono **non** consentito."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowMaps"
>title="Errore di proprietà Map-type"
>abstract="Le proprietà di tipo mappa sono **non** consentito."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxNestedAggregationDepth"
>title="Errore massimo di profondità entità nidificata"
>abstract="La profondità massima degli array nidificati è **5**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxObjectNestingLevel"
>title="Errore di quantità massima di oggetti nidificati"
>abstract="Il numero massimo di oggetti nidificati consentito è **10**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_generic"
>title="Violazione vincolo"
>abstract="Il pubblico viola un vincolo. Per ulteriori informazioni, leggere il documento collegato."

Quando si utilizzano i tipi di pubblico dell’account, il pubblico **deve** rispettare i seguenti vincoli:

>[!NOTE]
>
>L&#39;elenco seguente mostra **predefinito** vincoli per il pubblico dell’account. Questi valori **maggio** a seconda delle impostazioni implementate dall’amministratore della tua organizzazione.

- L’intervallo di lookback massimo per gli eventi esperienza è **30 giorni**.
- La profondità massima dei contenitori nidificati è **5**.
   - Ciò significa che **non può** avere più di cinque contenitori nidificati durante la creazione del pubblico.
- Il numero massimo di regole all’interno di un singolo contenitore è **5**.
   - Ciò significa che il pubblico **non può** hai più di cinque regole che compongono il pubblico.
- Il numero massimo di entità incrociate utilizzabili è **5**.
   - Un’entità incrociata si verifica quando si passa da un’entità all’altra all’interno del pubblico. Ad esempio, passare da un account a una persona a un elenco di marketing.
- Entità personalizzate **non può** essere utilizzati.
- Il numero massimo di valori che è possibile controllare per un singolo campo è **50**.
   - Ad esempio, se hai un campo &quot;Nome città&quot;, puoi confrontare tale valore con 50 nomi di città.
- Pubblico dell’account **non può** utilizzare `inSegment` eventi.
- Pubblico dell’account **non può** utilizzare eventi sequenziali.
- Pubblico dell’account **non può** utilizzare le mappe.
- La profondità massima degli array nidificati è **5**.
- Il numero massimo di oggetti nidificati è **10**.
