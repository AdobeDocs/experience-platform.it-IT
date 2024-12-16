---
keywords: RTCDP;CDP;B2B edition;Real-time Customer Data Platform;real time customer data platform;real time cdp;b2b;cdp
solution: Experience Platform
title: Guida introduttiva di Real-time Customer Data Platform B2B edition
description: Utilizza questo scenario di esempio per configurare l’implementazione di Adobe Real-time Customer Data Platform B2B edition.
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: 90323c32833b0d8a2b4feb88b8eb851bc767c2f8
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---

# Guida introduttiva a Real-time Customer Data Platform B2B edition

Questo documento fornisce un flusso di lavoro end-to-end di alto livello per iniziare a utilizzare Real-time Customer Data Platform (CDP) B2B edition, utilizzando un caso d’uso di esempio per illustrare i concetti chiave.

La società tecnologica Bodea vuole combinare dati personali e di account provenienti da diverse fonti di dati in silos per indirizzare in modo efficace i clienti tramite e-mail e una campagna pubblicitaria LinkedIn per il suo nuovo prodotto. Bodea utilizza il Marketo Engage come piattaforma di automazione del marketing e deve segmentare un pubblico specifico per B2B da più CRM contenenti i dati dei clienti.

## Introduzione

Questo flusso di lavoro si basa su diversi servizi Adobe Experience Platform come parte della dimostrazione. Se desideri seguire il corso, ti consigliamo di avere una buona conoscenza dei seguenti servizi:

- [Experience Data Model (XDM)](../xdm/home.md)
- [Origini](../sources/home.md)
- [Segmentazione](../segmentation/home.md)
- [Destinazioni](../destinations/home.md)

## Creare schemi per i dati

Come parte della configurazione iniziale, il reparto IT di Bodea deve creare uno schema XDM per garantire che i propri dati seguano un formato standard quando vengono introdotti in Platform e siano utilizzabili tra diversi servizi e prodotti Adobe Experience Cloud di Platform (come Adobe Analytics e Adobe Target).

>[!WARNING]
>
>Segui i modelli di acquisizione descritti nella relativa documentazione di origine collegata a in questa esercitazione. Non è garantito il funzionamento di altri metodi di mappatura dei campi.

Adobe Experience Platform consente di generare automaticamente gli schemi e i namespace richiesti per le origini dati B2B. Questo strumento garantisce che gli schemi creati descrivano i dati in modo strutturato e riutilizzabile. Seguire gli spazi dei nomi [B2B e la documentazione dell&#39;utilità di generazione automatica dello schema](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) per un riferimento completo al processo di installazione.

Nell&#39;interfaccia utente di Adobe Experience Platform, l&#39;addetto al marketing di Bodea seleziona **[!UICONTROL Schemi]** nella barra a sinistra, seguito dalla scheda **[!UICONTROL Sfoglia]**. Poiché hanno utilizzato l’utility di generazione automatica del Marketo Engage, i nuovi schemi vuoti vengono visualizzati nell’elenco e hanno tutti il prefisso &quot;B2B&quot;.

![Scheda Sfoglia area di lavoro schema](./assets/b2b-tutorial/empty-b2b-schemas.png)

L&#39;utility di generazione automatica ha definito la struttura del modello dati per gli schemi utilizzando le classi B2B XDM standard (ad esempio [XDM Business Account](../xdm/classes/b2b/business-account.md) e [XDM Business Opportunity](../xdm/classes/b2b/business-opportunity.md)) che acquisiscono entità di dati B2B fondamentali. Inoltre, gli schemi B2B generati automaticamente su queste classi dispongono di relazioni prestabilite che consentono casi di utilizzo di segmentazione avanzata. Eventuali gruppi di campi aggiuntivi necessari per la struttura dati possono essere creati facilmente qui tramite l’interfaccia utente. Per ulteriori informazioni, consulta la [guida dell&#39;interfaccia utente XDM, aggiunta di gruppi di campi a una sezione di schema](../xdm/ui/resources/schemas.md#add-field-groups).

>[!NOTE]
> 
>Se non si utilizza l&#39;utilità di generazione automatica o se è necessario creare una nuova relazione, vedere l&#39;esercitazione [creazione di relazioni tra schemi B2B](../xdm/tutorials/relationship-b2b.md).

Real-Time Customer Profile unisce dati provenienti da origini diverse per creare profili consolidati di entità B2B chiave. Poiché i profili vengono generati in base a una singola classe, l’utility di generazione automatica imposta le relazioni tra schemi in base ai casi di utilizzo aziendali comuni. Di conseguenza, il team di Bodea è ora pronto per acquisire i dati in base ai propri schemi B2B.

>[!NOTE]
> 
>Gli spazi dei nomi di identità predefiniti, le chiavi primarie e le relazioni create per gli schemi dall&#39;utilità di generazione automatica sono facilmente individuabili nell&#39;area di lavoro Schema.
>
>![visualizzazione interfaccia utente predefinita identità schema e relazioni](./assets/b2b-tutorial/schema-identity-relationship.png)

## Inserire i dati in Experience Platform

Successivamente, l&#39;addetto al marketing di Bodea utilizza il connettore [Marketo Engage](../sources/connectors/adobe-applications/marketo/marketo.md) per acquisire i dati in Platform per l&#39;utilizzo nei servizi a valle. È inoltre possibile acquisire i dati utilizzando una delle origini approvate per Real-Time CDP B2B edition.

>[!NOTE]
> 
>Per scoprire quali connettori di origine sono disponibili per la tua organizzazione, puoi visualizzare il catalogo delle origini nell’interfaccia utente di Platform. Per accedere al catalogo, seleziona **Origini** nell&#39;area di navigazione a sinistra, quindi seleziona **Catalogo**.

Per creare una connessione tra un account Marketo e Platform, è necessario acquisire le credenziali di autenticazione. Per istruzioni dettagliate, consulta la [guida sull&#39;ottenimento delle credenziali di autenticazione del connettore di origine di Marketo](../sources/connectors/adobe-applications/marketo/marketo-auth.md).

Dopo aver acquisito le credenziali di autenticazione, l’addetto al marketing di Bodea crea una connessione tra l’account Marketo e la relativa organizzazione Platform. Consulta la documentazione per le istruzioni su [come connettere un account Marketo utilizzando l&#39;interfaccia utente di Platform](../sources/tutorials/ui/create/adobe-applications/marketo.md).

Il connettore di origine del Marketo Engage fornisce una funzione di mappatura automatica per semplificare il processo di mappatura di tutti i campi di dati a quelli degli schemi appena creati.

>[!NOTE]
> 
>Se hai creato gruppi di campi personalizzati negli schemi XDM, è possibile che in questa fase del processo siano presenti campi non collegati. Verifica tutti i valori che popolano i gruppi di campi personalizzati.

L’addetto al marketing di Bodea controlla che tutti i gruppi di campi siano mappati in modo appropriato e continua il processo di configurazione delle origini inizializzando un flusso di dati. Creando un flusso di dati per inserire dati Marketo, i dati in arrivo possono essere utilizzati dai servizi Platform a valle. Durante il processo di acquisizione iniziale, i dati vengono inseriti in Experience Platform come batch. Successivamente, i dati acquisiti successivi vengono quindi inviati in streaming al profilo con aggiornamenti in tempo quasi reale.

## Creare un pubblico per valutare i dati

La prossima attività consiste nel creare un pubblico per la nuova campagna di e-mail marketing di Bodea, basato su attributi specifici di entità correlate nei dati di origine. Nell&#39;interfaccia utente di Platform, l&#39;addetto al marketing di Bodea seleziona prima **[!UICONTROL Segmenti]** nell&#39;area di navigazione a sinistra, quindi **[!UICONTROL Crea segmento]**.

In questo esempio, il pubblico trova tutte le persone che lavorano nel reparto vendite e sono correlate a qualsiasi account che ha almeno un’opportunità aperta. Questo pubblico richiede un collegamento tra la classe Profilo individuale XDM, la classe Account aziendale XDM e la classe Opportunità aziendale XDM.

![Segmento del caso d&#39;uso](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Per istruzioni su come creare tipi di pubblico per valutare i dati, consulta la [Guida dell&#39;interfaccia utente di Segment Builder](../segmentation/ui/segment-builder.md). Per casi di utilizzo più specifici di segmentazione B2B, consulta la [panoramica sulla segmentazione per Real-Time CDP B2B edition](./segmentation/b2b.md).

Il Generatore di segmenti consente di creare un pubblico commerciabile dai dati del profilo cliente in tempo reale e di visualizzare stime del pubblico potenziale in base alla combinazione di attributi, eventi e pubblici esistenti definiti.

## Attivare i dati valutati in una destinazione

Una volta creato il pubblico, viene fornito un riepilogo nella sezione [!UICONTROL Dettagli] dell&#39;area di lavoro. Poiché non è attualmente attivata alcuna destinazione per la definizione del segmento, l’addetto marketing di Bodea deve esportare il pubblico in un set di dati in cui è possibile accedervi e su cui intervenire.

Nell&#39;area di lavoro [!UICONTROL Segmenti] dell&#39;interfaccia utente di Platform, l&#39;addetto al marketing di Bodea seleziona **[!UICONTROL Attiva nella destinazione]**.

![Attiva il pubblico in una destinazione](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>Consulta il tutorial su [attivazione di un pubblico in una destinazione](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) per i passaggi completi su come eseguire questa operazione.

L’addetto al marketing di Bodea attiva il pubblico nella destinazione Marketo, consentendo loro di inviare i dati del pubblico da Platform a Marketo Engage sotto forma di elenco statico. Per ulteriori informazioni, consulta la guida sulla [destinazione Marketo](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html).

## Passaggi successivi

Seguendo questa esercitazione, hai sfruttato correttamente i vari servizi Adobe Experience Platform utilizzati da Real-Time CDP B2B edition. Di conseguenza, hai imparato ad acquisire, segmentare, valutare ed esportare i tuoi dati B2B come tipi di pubblico utilizzabili che possono essere coinvolti su canali diversi.
