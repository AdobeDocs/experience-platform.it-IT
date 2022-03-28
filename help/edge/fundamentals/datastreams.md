---
title: Configurare il Datastream per l'SDK Web di Experience Platform
description: 'Scopri come configurare i Datastreams. '
keywords: configurazione;datastreams;datastreamId;edge;datastream id;Impostazioni ambiente;edgeConfigId;identità;sincronizzazione id abilitata;ID contenitore di sincronizzazione ID;Sandbox;ingresso streaming;set di dati evento;target;codice client;token di proprietà;ID ambiente di Target;destinazioni cookie;destinazioni url;impostazioni Analytics Blockreport id suite;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 7fc62099ef7561595d260a5507fb2094f58b6016
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 1%

---

# Configurare un datastream

Un datastream rappresenta la configurazione lato server quando si implementano gli SDK per web e dispositivi mobili di Adobe Experience Platform. Mentre il [configura, comando](configuring-the-sdk.md) nell&#39;SDK controlla gli elementi che devono essere gestiti sul client (come il `edgeDomain`), i datastreams gestiscono tutte le altre configurazioni per l&#39;SDK. Quando viene inviata una richiesta a Adobe Experience Platform Edge Network, la `edgeConfigId` viene utilizzato per fare riferimento al datastream. Questo consente di aggiornare la configurazione lato server senza dover apportare modifiche al codice sul sito web.

Questo documento descrive i passaggi per la configurazione di un datastream nell’interfaccia utente di raccolta dati.

>[!NOTE]
>
>Per poter accedere a questa funzione nell’interfaccia utente, è necessario eseguire il provisioning della tua organizzazione. Se non hai accesso, compila quanto segue [modulo](http://adobe.ly/websdkaccess) e vi concederemo l&#39;accesso necessario.

## Accedere al [!UICONTROL Datastreams] workspace

Puoi creare e gestire i datastreams nell’interfaccia utente Raccolta dati selezionando **[!UICONTROL Datastreams]** nella navigazione a sinistra.

![Scheda Datastreams nell’interfaccia utente di raccolta dati](../images/datastreams/datastreams-tab.png)

>[!NOTE]
>
>Mentre puoi accedere al [!UICONTROL Datastreams] indipendentemente dal fatto che si utilizzino le funzionalità di gestione tag di Platform, è necessario disporre delle autorizzazioni per gli sviluppatori per gestire direttamente i datastreams. Consulta la sezione [autorizzazioni utente](../../tags/ui/administration/user-permissions.md) per ulteriori informazioni, consulta la documentazione sui tag .

La [!UICONTROL Datastreams] visualizza un elenco dei datastreams esistenti, con il relativo nome descrittivo, ID e data dell’ultima modifica. Selezionare il nome di un datastream in [visualizzare i dettagli e configurare i servizi](#view-details).

Seleziona l’icona &quot;Altro&quot; (**...**) per un particolare datastream per rivelare più opzioni. Seleziona **[!UICONTROL Modifica]** per aggiornare [configurazione di base](#configure) per il datastream, oppure seleziona **[!UICONTROL Elimina]** per rimuovere il datastream.

![Opzioni di modifica o eliminazione e del datastream esistente](../images/datastreams/edit-datastream.png)

## Crea un nuovo datastream {#create}

Per creare un datastream, inizia selezionando **[!UICONTROL Nuovo Datastream]**.

![Seleziona nuovo archivio dati](../images/datastreams/new-datastream-button.png)

### [!UICONTROL Configurare gli] {#configure}

Viene visualizzato il flusso di lavoro di creazione del datastream, a partire dal passaggio di configurazione. Da qui, devi fornire un nome e una descrizione facoltativa per il datastream.

Se stai configurando questo datastream per l’utilizzo in Experience Platform e stai utilizzando l’SDK per web di Platform, devi anche selezionare un [schema Experience Data Model (XDM) basato su eventi](../../xdm/classes/experienceevent.md) per rappresentare i dati che intendi acquisire.

![Configurazione di base per un datastream](../images/datastreams/configure.png)

Seleziona **[!UICONTROL Opzioni avanzate]** per visualizzare controlli aggiuntivi per configurare il datastream.

![Opzioni di configurazione avanzate](../images/datastreams/advanced-options.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Posizione geografica] | Determina se si verificano ricerche GPS in base all&#39;indirizzo IP dell&#39;utente. Impostazione predefinita **[!UICONTROL Nessuno]** disabilita le ricerche GPS, mentre il **[!UICONTROL Città]** fornisce le coordinate GPS a due posizioni decimali. |
| [!UICONTROL Cookie ID di prime parti] | Quando questa impostazione è abilitata, indica alla rete Edge di fare riferimento a un cookie specificato durante la ricerca di un [ID dispositivo di prime parti](../identity/first-party-device-ids.md), anziché cercare questo valore nella mappa identità.<br><br>Quando abiliti questa impostazione, devi fornire il nome del cookie in cui deve essere memorizzato l’ID. |
| [!UICONTROL Sincronizzazione ID di terze parti] | Le sincronizzazioni ID possono essere raggruppate in contenitori per consentire l’esecuzione di sincronizzazioni ID diverse in momenti diversi. Quando abilitata, questa impostazione consente di specificare quale contenitore di sincronizzazioni ID viene eseguito per questo datastream. |

Il resto di questa sezione si concentra sui passaggi per eseguire il mapping dei dati a uno schema evento Platform selezionato. Se utilizzi Mobile SDK o non stai configurando il datastream per Platform, seleziona **[!UICONTROL Salva]** prima di passare alla sezione successiva del [aggiunta di servizi al datastream](#add-services).

### Preparazione per la raccolta dei dati {#data-prep}

>[!IMPORTANT]
>
>La preparazione dei dati per la raccolta dei dati non è attualmente supportata per le implementazioni SDK di Mobile.

Data Prep è un servizio di Experience Platform che consente di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM). Quando configuri un datastream abilitato per Platform, puoi utilizzare le funzionalità di preparazione dei dati per mappare i dati di origine su XDM durante l’invio a Platform Edge Network.

Le sottosezioni seguenti descrivono i passaggi di base per la mappatura dei dati all’interno dell’interfaccia utente di raccolta dati. Per una guida completa su tutte le funzionalità di preparazione dei dati, comprese le funzioni di trasformazione per i campi calcolati, consulta la seguente documentazione:

* [Panoramica sulla preparazione dei dati](../../data-prep/home.md)
* [Funzioni di mappatura della preparazione dei dati](../../data-prep/functions.md)
* [Gestione dei formati di dati con Data Prep](../../data-prep/data-handling.md)

#### [!UICONTROL Seleziona dati]

Seleziona **[!UICONTROL Salvare e aggiungere mappature]** dopo aver completato [passaggio di configurazione di base](#configure)e **[!UICONTROL Seleziona dati]** viene visualizzato il passaggio . Da qui, devi fornire un oggetto JSON di esempio che rappresenti la struttura dei dati che intendi inviare a Platform. È possibile selezionare l’opzione per caricare l’oggetto come file oppure incollare l’oggetto non elaborato nella casella di testo fornita.

>[!IMPORTANT]
>
>L&#39;oggetto JSON deve avere un singolo nodo principale `data` per passare la convalida.

Se il JSON è valido, nel pannello di destra viene visualizzato uno schema di anteprima. Seleziona **[!UICONTROL Next]** (Avanti) per continuare.

![Esempio JSON di dati in arrivo previsti](../images/datastreams/select-data.png)

#### [!UICONTROL Mappatura]

La **[!UICONTROL Mappatura]** viene visualizzato un passaggio che ti consente di mappare i campi nei dati di origine a quelli dello schema dell’evento di destinazione in Platform. Per iniziare, seleziona **[!UICONTROL Aggiungi nuova mappatura]** per creare una nuova riga di mappatura.

![Aggiunta di una nuova mappatura](../images/datastreams/add-new-mapping.png)

Seleziona l’icona sorgente (![Icona Sorgente](../images/datastreams/source-icon.png)) e nella finestra di dialogo visualizzata seleziona il campo sorgente da mappare nell’area di lavoro fornita. Dopo aver scelto un campo, utilizza le **[!UICONTROL Seleziona]** per continuare.

![Selezione del campo da mappare nello schema di origine](../images/datastreams/source-mapping.png)

Quindi, seleziona l’icona dello schema (![Icona Schema](../images/datastreams/schema-icon.png)) per aprire una finestra di dialogo simile per lo schema dell’evento di destinazione. Scegli il campo a cui desideri mappare i dati prima di confermare con **[!UICONTROL Seleziona]**.

![Selezione del campo da mappare nello schema di destinazione](../images/datastreams/target-mapping.png)

Viene visualizzata nuovamente la pagina di mappatura con la mappatura del campo completata. La **[!UICONTROL Avanzamento mappatura]** aggiornamenti della sezione per riflettere il numero totale di campi mappati correttamente.

![Campo mappato con avanzamento riflesso](../images/datastreams/field-mapped.png)

Continua seguendo i passaggi precedenti per mappare il resto dei campi allo schema di destinazione. Anche se non è necessario mappare tutti i campi di origine disponibili, per completare questo passaggio è necessario mappare tutti i campi dello schema di destinazione impostati come necessario. La **[!UICONTROL Campi obbligatori]** contatore indica quanti campi obbligatori non sono ancora stati mappati nella configurazione corrente.

Una volta che il conteggio dei campi obbligatori raggiunge lo zero e si è soddisfatti della mappatura, selezionare **[!UICONTROL Salva]** per finalizzare le modifiche.

![Mapping completato](../images/datastreams/mapping-complete.png)

## Visualizza i dettagli del datastream {#view-details}

Dopo aver configurato un nuovo datastream o selezionato uno esistente da visualizzare, viene visualizzata la pagina dei dettagli per quel datastream. Qui puoi trovare ulteriori informazioni sul datastream, compreso il relativo ID.

![Pagina dei dettagli per un datastream creato](../images/datastreams/view-details.png)

Dalla schermata dei dettagli del datastream, puoi [aggiungi servizi](#add-services) per abilitare le funzionalità dei prodotti Adobe Experience Cloud a cui hai accesso.

## Aggiungere servizi a un datastream {#add-services}

Nella pagina dei dettagli di un datastream, seleziona **[!UICONTROL Aggiungi servizio]** per iniziare ad aggiungere i servizi disponibili per quel datastream.

![Seleziona Aggiungi servizio per continuare](../images/datastreams/add-service.png)

Nella schermata successiva, utilizza il menu a discesa per selezionare un servizio da configurare per questo datastream. In questo elenco verranno visualizzati solo i servizi a cui hai accesso.

![Selezionare un servizio dall&#39;elenco](../images/datastreams/service-selection.png)

Seleziona il servizio desiderato, compila le opzioni di configurazione visualizzate, quindi seleziona **[!UICONTROL Salva]** per aggiungere il servizio al datastream. Tutti i servizi aggiunti vengono visualizzati nella visualizzazione dei dettagli del datastream.

![Servizi aggiunti a un datastream](../images/datastreams/services-added.png)

Le sottosezioni seguenti descrivono le opzioni di configurazione per ogni servizio.

>[!NOTE]
>
>Ogni configurazione del servizio contiene un **[!UICONTROL Abilitato]** attiva automaticamente quando il servizio è selezionato. Per disabilitare il servizio selezionato per questo datastream, seleziona il **[!UICONTROL Abilitato]** scattare di nuovo.

### Impostazioni di Adobe Analytics

Questo servizio controlla se e come i dati vengono inviati ad Adobe Analytics. Ulteriori dettagli sono disponibili nella guida all&#39;indirizzo [invio di dati ad Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Blocco impostazioni Adobe Analytics](../images/datastreams/analytics-config.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL ID suite di rapporti] | **(Obbligatorio)** ID della suite di rapporti di Analytics a cui desideri inviare i dati. Questo ID si trova nell&#39;interfaccia utente di Adobe Analytics in [!UICONTROL Amministratore] > [!UICONTROL ReportSuites]. Se sono specificate più suite di rapporti, i dati vengono copiati in ciascuna suite di rapporti. |

### Impostazioni Adobe Audience Manager

Questo servizio controlla se e come i dati vengono inviati a Adobe Audience Manager. Tutto ciò che è necessario per inviare dati ad Audience Manager è quello di abilitare questa sezione. Le altre impostazioni sono facoltative ma incoraggiate.

![Adobe Blocco delle impostazioni di Gestione dell&#39;audience](../images/datastreams/audience-manager-config.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Destinazioni cookie abilitate] | Consente all’SDK di condividere le informazioni sui segmenti tramite [destinazioni cookie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) da [!DNL Audience Manager]. |
| [!UICONTROL Destinazioni URL abilitate] | Consente all’SDK di condividere le informazioni sui segmenti tramite [Destinazioni URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) da [!DNL Audience Manager]. |

### Impostazioni Adobe Experience Platform

>[!IMPORTANT]
>
>Quando abiliti un datastream per Platform, prendi nota della sandbox di Platform che stai utilizzando, come visualizzata nella barra multifunzione superiore dell’interfaccia utente di Raccolta dati.
>
>![Sandbox selezionato](../images/datastreams/platform-sandbox.png)
>
>Le sandbox sono partizioni virtuali in Adobe Experience Platform che ti consentono di isolare i dati e le implementazioni da altre parti della tua organizzazione. Una volta creato un datastream, la relativa sandbox non può essere modificata. Per ulteriori dettagli sul ruolo delle sandbox in Experience Platform, consulta la sezione [documentazione sandbox](../../sandboxes/home.md).

Questo servizio controlla se e come i dati vengono inviati a Adobe Experience Platform.

![Blocco delle impostazioni Adobe Experience Platform](../images/datastreams/platform-config.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Set di dati evento] | **(Obbligatorio)** Seleziona il set di dati della piattaforma a cui verranno inviati i dati evento cliente. Questo schema deve utilizzare [Classe ExperienceEvent XDM](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Set di dati del profilo] | Seleziona il set di dati della piattaforma a cui verranno inviati i dati degli attributi del cliente. Questo schema deve utilizzare [Classe di profilo individuale XDM](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Seleziona questa casella di controllo per abilitare l’Offer decisioning per un’implementazione Platform Web SDK. Consulta la guida su [utilizzo di Offer Decisioning con Platform Web SDK](../personalization/offer-decisioning/offer-decisioning-overview.md) per ulteriori dettagli sull’implementazione. Per ulteriori informazioni sulle funzionalità di Offer Decisioning, consulta la [Documentazione di Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=it). |
| [!UICONTROL Segmentazione Edge] | Seleziona questa casella di controllo per abilitare [segmentazione dei bordi](../../segmentation/ui/edge-segmentation.md) per questo datastream. Quando l’SDK invia i dati tramite un datastream abilitato per la segmentazione edge, nella risposta vengono restituite tutte le appartenenze di segmenti aggiornate per il profilo in questione.<br><br>Questa opzione può essere utilizzata in combinazione con [!UICONTROL Destinazioni personalizzazione] per [casi d’uso per la personalizzazione di pagine successive](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Destinazioni personalizzazione] | Se utilizzato in combinazione con il [!UICONTROL Segmentazione Edge] questa opzione consente al datastream di connettersi a motori di personalizzazione come Adobe Target. Fai riferimento alla documentazione sulle destinazioni per i passaggi specifici su [configurazione delle destinazioni di personalizzazione](../../destinations/ui/configure-personalization-destinations.md). |

### Impostazioni di Adobe Target

Questo servizio controlla se e come i dati vengono inviati ad Adobe Target.

![Blocco delle impostazioni di Adobe Target](../images/datastreams/target-config.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Token di proprietà] | [!DNL Target] consente ai clienti di controllare le autorizzazioni tramite l’uso delle proprietà. Per ulteriori informazioni sulle proprietà, consulta la guida su [configurazione delle autorizzazioni Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) in [!DNL Target] documentazione.<br><br>Il token di proprietà si trova nell’interfaccia utente di Adobe Target in [!UICONTROL Configurazione] > [!UICONTROL Proprietà]. |
| [!UICONTROL ID ambiente di destinazione] | [Ambienti in Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) ti aiuta a gestire la tua implementazione in tutte le fasi di sviluppo. Questa impostazione specifica l&#39;ambiente da utilizzare con questo datastream.<br><br>Si consiglia di impostare questo valore in modo diverso per ogni `dev`, `stage`e `prod` ambienti datastream per semplificare le operazioni. Tuttavia, se hai già definito ambienti Adobe Target, puoi utilizzarli. |
| [!UICONTROL Spazio dei nomi ID di terze parti di Target] | Spazio dei nomi di identità per `mbox3rdPartyId` si desidera utilizzare per questo datastream. Consulta la guida su [implementazione `mbox3rdPartyId` con l’SDK per web](../personalization/adobe-target/using-mbox-3rdpartyid.md) per ulteriori informazioni. |

### [!UICONTROL Inoltro eventi] impostazioni

Questo servizio controlla se e come i dati vengono inviati a [inoltro eventi](../../tags/ui/event-forwarding/overview.md).

![Sezione Inoltro eventi dell’interfaccia utente di configurazione](../images/datastreams/event-forwarding-config.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Launch, proprietà] | **(Obbligatorio)** Proprietà di inoltro eventi a cui si desidera inviare i dati. |
| [!UICONTROL Ambiente Launch] | **(Obbligatorio)** Ambiente all’interno della proprietà selezionata a cui si desidera inviare i dati. |

>[!NOTE]
>
>È possibile selezionare **[!UICONTROL Immetti manualmente gli ID]** digitare i nomi delle proprietà e dell’ambiente anziché utilizzare i menu a discesa.

## Passaggi successivi

Questa guida illustra come configurare un datastream nell’interfaccia utente di raccolta dati. Per ulteriori informazioni su come installare e configurare l’SDK web dopo aver configurato un datastream, consulta la [Guida alla raccolta dati E2E](../../collection/e2e.md#install).
