---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;piattaforma dati cliente in tempo reale;cdp in tempo reale;b2b;cdp
solution: Experience Platform
title: Guida introduttiva ad Real-time Customer Data Platform B2B Edition
description: Utilizza questo scenario di esempio come esempio per configurare l’implementazione di Adobe Real-time Customer Data Platform B2B Edition.
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Guida introduttiva a Real-time Customer Data Platform B2B Edition

Questo documento fornisce un flusso di lavoro end-to-end di alto livello per iniziare a utilizzare Real-time Customer Data Platform (CDP) B2B Edition, utilizzando un esempio di caso d’uso per illustrare concetti chiave.

La società di tecnologia Bodea vuole combinare i dati delle persone e degli account provenienti da diverse fonti di dati in silos per indirizzare efficacemente i clienti con un&#39;e-mail e una campagna pubblicitaria LinkedIn per il suo nuovo prodotto. Bodea utilizza il Marketo Engage come piattaforma di automazione del marketing e deve segmentare un pubblico specifico per B2B da più CRM che contengono i dati dei clienti.

## Introduzione

Questo flusso di lavoro di esercitazione si basa su diversi servizi Adobe Experience Platform come parte della dimostrazione. Se desideri seguire questa procedura, è consigliabile avere una buona comprensione dei seguenti servizi:

- [Modale dati esperienza (XDM)](../xdm/home.md)
- [Origini](../sources/home.md)
- [Segmentazione](../segmentation/home.md)
- [Destinazioni](../destinations/home.md)

## Creare schemi per i dati

Come parte della configurazione iniziale, il reparto IT di Bodea deve creare uno schema XDM per garantire che i propri dati seguano un formato standard quando vengono inseriti in Platform ed è utilizzabile tra diversi servizi Platform e prodotti Adobe Experience Cloud (come Adobe Analytics e Adobe Target).

>[!WARNING]
>
>In questa esercitazione devi seguire i pattern di acquisizione descritti nella relativa documentazione di origine a . Non è garantito il funzionamento di altri metodi di mappatura dei campi.

Adobe Experience Platform consente di generare automaticamente gli schemi e i namespace richiesti per le origini dati B2B. Questo strumento assicura che gli schemi creati descrivano i dati in modo strutturato e riutilizzabile. Segui [Documentazione dell&#39;utilità di generazione automatica di spazi dei nomi B2B e schemi](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) per un riferimento completo al processo di configurazione.

Nell’interfaccia utente di Adobe Experience Platform, l’addetto al marketing Bodea seleziona **[!UICONTROL Schemi]** nella barra a sinistra, seguita dalla **[!UICONTROL Sfoglia]** scheda . Poiché hanno utilizzato l&#39;utilità di generazione automatica del Marketo Engage, i nuovi schemi vuoti appaiono nell&#39;elenco e tutti hanno il prefisso &quot;B2B&quot;.

![Scheda Sfoglia dell’area di lavoro schema](./assets/b2b-tutorial/empty-b2b-schemas.png)

L&#39;utility di generazione automatica ha definito la struttura del modello dati per gli schemi utilizzando le classi standard XDM B2B (ad esempio [Account aziendale XDM](../xdm/classes/b2b/business-account.md) e [Opportunità aziendali XDM](../xdm/classes/b2b/business-opportunity.md)) che acquisiscono entità dati B2B fondamentali. Inoltre, gli schemi B2B generati automaticamente basati su queste classi hanno relazioni prestabilite che consentono casi d’uso avanzati di segmentazione. L’interfaccia utente consente di creare facilmente tutti i gruppi di campi aggiuntivi necessari per la struttura dei dati. Consulta la sezione [Guida all’interfaccia utente XDM, aggiunta di gruppi di campi a una sezione dello schema](../xdm/ui/resources/schemas.md#add-field-groups) per ulteriori informazioni.

>[!NOTE]
> 
>Se non utilizzi l&#39;utilità di generazione automatica o se è necessario creare una nuova relazione, consulta l&#39;esercitazione su [creazione di relazioni tra schemi B2B](../xdm/tutorials/relationship-b2b.md).

Profilo cliente in tempo reale unisce i dati provenienti da fonti diverse per creare profili consolidati di entità B2B chiave. Poiché i profili vengono generati in base a una singola classe, l’utility di generazione automatica imposta le relazioni tra schemi in base a casi d’uso aziendali comuni. Di conseguenza, il team Bodea è ora pronto per acquisire i dati in base ai loro schemi B2B.

>[!NOTE]
> 
>Nell’area di lavoro Schema è possibile individuare facilmente spazi dei nomi di identità predefiniti, chiavi primarie e relazioni create per gli schemi dall’utility di generazione automatica.
>
>![visualizzazione dell&#39;interfaccia utente di identità e relazione dello schema predefinita](./assets/b2b-tutorial/schema-identity-relationship.png)

## Inserire i dati in Experience Platform

Successivamente, l&#39;addetto al marketing di Bodea utilizza il [Connettore Marketo Engage](../sources/connectors/adobe-applications/marketo/marketo.md) acquisire dati in Platform da utilizzare nei servizi a valle. Puoi anche acquisire i dati utilizzando una delle origini approvate per Real-Time CDP B2B Edition.

>[!NOTE]
> 
>Per scoprire quali connettori sorgente sono disponibili per la tua organizzazione, puoi visualizzare il catalogo origini nell’interfaccia utente di Platform. Per accedere al catalogo, seleziona **Origini** nel menu di navigazione a sinistra, seleziona **Catalogo**.

Per creare una connessione tra un account Marketo e Platform, è necessario acquisire le credenziali di autenticazione. Consulta la sezione [guida al raggiungimento delle credenziali di autenticazione del connettore di origine Marketo](../sources/connectors/adobe-applications/marketo/marketo-auth.md) per istruzioni dettagliate.

Dopo aver acquisito le credenziali di autenticazione, l’addetto al marketing Bodea crea una connessione tra l’account Marketo e la relativa organizzazione IMS della piattaforma. Consulta la documentazione per le istruzioni su [come collegare un account Marketo tramite l’interfaccia utente della piattaforma](../sources/tutorials/ui/create/adobe-applications/marketo.md).

Il connettore di origine del Marketo Engage fornisce una funzione di mappatura automatica che facilita il processo di mappatura di tutti i campi dati su quelli degli schemi appena creati.

>[!NOTE]
> 
>Se hai creato gruppi di campi personalizzati negli schemi XDM, in questa fase del processo potresti avere campi non connessi. Assicurati di controllare tutti i valori che popolano i gruppi di campi personalizzati.

L’addetto al marketing Bodea verifica che tutti i gruppi di campi siano mappati in modo appropriato e continua il processo di configurazione delle sorgenti inizializzando un flusso di dati. Creando un flusso di dati per l’inserimento di dati Marketo, i dati in arrivo possono essere utilizzati dai servizi Platform a valle. Durante il processo di acquisizione iniziale, i dati vengono inseriti in Experience Platform come batch. In seguito, i dati acquisiti successivi vengono quindi trasmessi in streaming a Profilo con aggiornamenti in tempo reale.

## Creare un segmento per valutare i dati

L’attività successiva consiste nel creare un pubblico per la nuova campagna di marketing e-mail di Bodea basata su attributi specifici delle entità correlate nei dati di origine. Nell’interfaccia utente di Platform, l’addetto al marketing Bodea seleziona per la prima volta **[!UICONTROL Segmenti]** nella navigazione a sinistra, quindi **[!UICONTROL Creare un segmento]**.

In questo esempio, il segmento trova tutte le persone che lavorano nel reparto vendite e sono correlate a qualsiasi account che ha almeno una opportunità aperta. Questo segmento richiede un collegamento tra la classe Profilo individuale XDM, la classe Account aziendale XDM e la classe Opportunità aziendale XDM.

![Segmento del caso d’uso](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Per istruzioni su come creare segmenti per valutare i dati, consulta la sezione [Guida all’interfaccia utente di Generatore di segmenti](../segmentation/ui/segment-builder.md). Per casi d’uso di segmentazione B2B più specifici, consulta [panoramica sulla segmentazione per Real-Time CDP B2B Edition](./segmentation/b2b.md).

Il Generatore di segmenti consente di creare un pubblico commerciabile dai dati del Profilo cliente in tempo reale e di visualizzare le stime del pubblico potenziale in base alla combinazione di attributi, eventi e tipi di pubblico esistenti definiti.

## Attiva i dati valutati in una destinazione

Una volta creato correttamente il segmento, viene fornito un riepilogo nel [!UICONTROL Dettagli] dell&#39;area di lavoro. Poiché non sono attualmente attivate destinazioni per il segmento, l’addetto al marketing Bodea deve esportare il pubblico in un set di dati a cui è possibile accedere e su cui agisce.

All&#39;interno di [!UICONTROL Segmenti] nell’area di lavoro dell’interfaccia utente di Platform, l’addetto al marketing di Bodea seleziona **[!UICONTROL Attiva a destinazione]**.

![Attiva il segmento a una destinazione](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>Guarda l’esercitazione su [attivazione di un segmento a una destinazione](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) per passaggi completi su come eseguire questa operazione.

L’addetto al marketing Bodea attiva il segmento alla destinazione Marketo, consentendo loro di inviare in push i dati dei segmenti da Platform a Marketo Engage sotto forma di elenco statico. Consulta la guida [Destinazione Marketo](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html) per ulteriori informazioni.

## Passaggi successivi

Seguendo questa esercitazione, hai sfruttato con successo i vari servizi Adobe Experience Platform utilizzati da Real-Time CDP B2B Edition. Di conseguenza, hai imparato a acquisire, segmentare, valutare ed esportare i tuoi dati B2B come tipi di pubblico utilizzabili che possono essere coinvolti in diversi canali.
