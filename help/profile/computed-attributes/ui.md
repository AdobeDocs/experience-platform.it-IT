---
title: Guida dell’interfaccia utente Attributi calcolati
description: Scopri come creare, visualizzare e aggiornare gli attributi calcolati utilizzando l’interfaccia utente di Adobe Experience Platform.
source-git-commit: 7ed473750b673eefd84b8d727043ad6ea35c3a8e
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 1%

---


# Guida dell’interfaccia utente attributi calcolati

In Adobe Experience Platform, gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate in segmentazione, attivazione e personalizzazione.

Questo documento fornisce una guida su come creare e aggiornare attributi calcolati utilizzando l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida dell’interfaccia utente richiede una comprensione dei vari [!DNL Experience Platform] servizi coinvolti nella gestione [!DNL Real-Time Customer Profiles]. Prima di leggere questa guida o di lavorare nell’interfaccia utente, consulta la documentazione dei seguenti servizi:

- [[!DNL Real-Time Customer Profile]](../home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.

## Visualizza attributi calcolati {#view}

Nell’interfaccia utente di Experienci Platform, seleziona **[!UICONTROL Profili]** nel menu di navigazione a sinistra, seguito da **[!UICONTROL Attributi calcolati]** per visualizzare un elenco degli attributi calcolati disponibili per la tua organizzazione. Ciò include informazioni sul nome, la descrizione, la data dell&#39;ultima valutazione e lo stato dell&#39;ultima valutazione dell&#39;attributo calcolato.

![Il [!UICONTROL Profilo] sezione e [!UICONTROL Attributi calcolati] Le schede sono evidenziate e mostrano agli utenti come accedere alla pagina di navigazione degli attributi calcolati.](./images/ui/browse.png)

Per selezionare i campi visibili, è possibile selezionare ![icona configura colonne](./images/ui/configure-icon.png) per aggiungere o rimuovere i campi da visualizzare.

| Campo | Descrizione |
| ----- | ----------- |
| [!UICONTROL Nome] | Nome visualizzato dell&#39;attributo calcolato. |
| [!UICONTROL Descrizione] | Descrizione dell&#39;attributo calcolato. |
| [!UICONTROL Metodo di valutazione] | Il metodo di valutazione per l&#39;attributo calcolato. In questo momento, solo **batch** è supportato. |
| [!UICONTROL Ultima valutazione eseguita] | Questo timestamp rappresenta l’ultima esecuzione di valutazione riuscita. Solo gli eventi che si sono verificati **prima di** questo timestamp viene considerato nell’ultima valutazione riuscita. |
| [!UICONTROL Stato ultima valutazione] | Lo stato che indica se l’attributo calcolato è stato calcolato correttamente o meno nell’ultima esecuzione della valutazione. I valori possibili includono **[!UICONTROL Completato]** o **[!UICONTROL Non riuscito]**. |
| [!UICONTROL Refresh frequency (Frequenza di aggiornamento)] | Indicazione della frequenza con cui si prevede di aggiornare l&#39;attributo calcolato. I valori possibili includono orario, giornaliero, settimanale o mensile. |
| [!UICONTROL Aggiornamento rapido] | Valore che indica se l&#39;aggiornamento rapido è abilitato o meno per questo attributo di calcolo. Se è abilitato l&#39;aggiornamento rapido, l&#39;attributo calcolato può essere aggiornato su base giornaliera anziché settimanale, bisettimanale o mensile. Questo valore è applicabile solo per gli attributi calcolati con un periodo di lookback superiore a una base settimanale. |
| [!UICONTROL Stato del ciclo di vita] | Stato corrente dell&#39;attributo calcolato. Esistono tre stati possibili: <ul><li>**[!UICONTROL Bozza]:** L’attributo calcolato **non** hai già creato un campo nello schema. In questo stato, l’attributo calcolato può essere modificato. </li><li>**[!UICONTROL Pubblicato]:** L’attributo calcolato ha un campo creato nello schema ed è pronto per essere utilizzato. In questo stato, l’attributo calcolato **non può** essere modificata.</li><li>**[!UICONTROL Inattivo]:** L’attributo calcolato è disabilitato. Per ulteriori informazioni sullo stato di inattività, leggere [Pagina Domande frequenti](./faq.md#inactive-status). </li> |
| [!UICONTROL Creato] | Timestamp che mostra la data e l’ora di creazione dell’attributo calcolato. |
| [!UICONTROL Ultima modifica] | Timestamp che mostra la data e l’ora dell’ultima modifica apportata all’attributo calcolato. |

Puoi anche filtrare gli attributi calcolati visualizzati in base allo stato del ciclo di vita. Seleziona la ![funnel](./images/ui/filter-icon.png) icona.

![L’icona del filtro viene evidenziata.](./images/ui/select-filter.png)

Ora puoi scegliere di filtrare gli attributi calcolati per stato ([!UICONTROL Bozza], [!UICONTROL Pubblicato], e [!UICONTROL Inattivo]).

![Vengono evidenziate le opzioni per le quali è possibile filtrare gli attributi calcolati. Queste opzioni includono [!UICONTROL Bozza], [!UICONTROL Pubblicato], e [!UICONTROL Inattivo].](./images/ui/view-filters.png)

Inoltre, puoi selezionare un attributo calcolato per visualizzare informazioni più dettagliate su di esso. Per ulteriori informazioni sulla pagina dei dettagli degli attributi calcolati, consulta [visualizzare la sezione dei dettagli di un attributo calcolato](#view-details).

## Creare un attributo calcolato {#create}

Per creare un nuovo attributo calcolato, seleziona **[!UICONTROL Crea attributo calcolato]** per inserire il nuovo flusso di lavoro attributo calcolato.

![Il [!UICONTROL Creare attributi calcolati] viene evidenziato, mostrando agli utenti come raggiungere la pagina di creazione di un attributo calcolato.](./images/ui/create.png)

Il **[!UICONTROL Crea attributo calcolato]** viene visualizzata. In questa pagina è possibile aggiungere le informazioni di base per l&#39;attributo calcolato che si desidera creare.

| Campo | Descrizione |
| ----- | ----------- |
| [!UICONTROL Nome visualizzato] | Il nome con cui sarà noto l’attributo calcolato. È necessario mantenere questo nome visualizzato univoco per ogni attributo calcolato. Come best practice, questo nome visualizzato deve contenere identificatori relativi all’attributo calcolato. Ad esempio, &quot;Somma degli acquisti di scarpe degli ultimi 7 giorni&quot;. |
| [!UICONTROL Nome campo] | Nome utilizzato per fare riferimento all&#39;attributo calcolato in altri servizi a valle. Questo nome deriva automaticamente dal nome visualizzato ed è scritto in camelCase. |
| [!UICONTROL Descrizione] | Descrizione dell&#39;attributo calcolato che si sta tentando di creare. |

![Il [!UICONTROL Informazioni di base] sezione del [!UICONTROL Crea attributo calcolato] pagina viene evidenziata.](./images/ui/basic-information.png)

Dopo aver aggiunto i dettagli dell’attributo calcolato, puoi iniziare a definire le regole.

### Specificare le condizioni di filtro degli eventi

Per creare una regola, seleziona innanzitutto gli attributi dalla **[!UICONTROL Eventi]** per filtrare gli eventi su cui desideri eseguire l’aggregazione. Attualmente, sono supportati solo attributi evento di tipo non array.

![Il [!UICONTROL Eventi] viene evidenziata.](./images/ui/events.png)

Dopo aver selezionato l’attributo da utilizzare nella definizione dell’attributo calcolato, puoi scegliere a cosa verrà confrontato questo valore.

![Vengono visualizzati i tipi di confronto disponibili.](./images/ui/select-comparison.png)

### Applica funzione di aggregazione

Ora puoi applicare una funzione al campo dall’output condizionale. Selezionare innanzitutto il tipo di funzione di aggregazione. Le opzioni disponibili includono [!UICONTROL Somma], [!UICONTROL Min], [!UICONTROL Max], [!UICONTROL Conteggio], e [!UICONTROL Più recente]. Ulteriori informazioni su queste funzioni sono disponibili nella [sezione delle funzioni](./overview.md#functions) della panoramica degli attributi calcolati.

![Vengono visualizzate le funzioni degli attributi calcolati.](./images/ui/select-function.png)

Dopo aver scelto una funzione, puoi scegliere il campo su cui eseguire l’aggregazione. I campi idonei da scegliere dipendono dalla funzione selezionata.

![Il campo evidenziato mostra l&#39;attributo su cui si sta scegliendo di aggregare la funzione.](./images/ui/select-eligible-field.png)

### Durata lookback

Dopo aver applicato la funzione di aggregazione, è necessario definire il periodo di lookback dell’attributo calcolato. Questo periodo di lookback specifica per quanto tempo desideri aggregare gli eventi. Questa durata del lookback può essere specificata in termini di ore, giorni, settimane o mesi.

![Viene evidenziata la durata del lookback.](./images/ui/select-lookback-duration.png)

### Aggiornamento rapido {#fast-refresh}

>[!CONTEXTUALHELP]
>id="platform_profile_computedAttributes_fastRefresh"
>title="Aggiornamento rapido"
>abstract="L’aggiornamento rapido consente di mantenere aggiornati gli attributi. L’abilitazione di questa opzione consente di aggiornare gli attributi calcolati su base giornaliera, anche per periodi di lookback più lunghi, per poter reagire rapidamente alle attività degli utenti. Questo valore è applicabile solo per gli attributi calcolati con un periodo di lookback superiore a una base settimanale."

Quando si applica la funzione di aggregazione, è possibile abilitare l’aggiornamento rapido se il periodo di lookback è superiore a una settimana.

![Il [!UICONTROL Aggiornamento rapido] la casella di controllo è evidenziata.](./images/ui/enable-fast-refresh.png)

L’aggiornamento rapido consente di mantenere aggiornati gli attributi. L’abilitazione di questa opzione consente di aggiornare gli attributi calcolati su base giornaliera, anche per periodi di lookback più lunghi, per poter reagire rapidamente alle attività degli utenti.

Per ulteriori informazioni sull&#39;aggiornamento rapido, leggere [sezione aggiornamento rapido](./overview.md#fast-refresh) della panoramica degli attributi calcolati.

Una volta completati questi passaggi, puoi scegliere se salvare l’attributo calcolato come bozza o pubblicarlo immediatamente.

![Il [!UICONTROL Salva come bozza] e [!UICONTROL Pubblica] vengono evidenziati.](./images/ui/draft-or-publish.png)

## Visualizzare i dettagli di un attributo calcolato {#view-details}

Per visualizzare i dettagli di un attributo calcolato, selezionare l&#39;attributo calcolato che si desidera visualizzare in [!UICONTROL **Sfoglia**] pagina.

![Viene evidenziato un attributo calcolato.](./images/ui/select.png)

Il contenuto della pagina varia, a seconda che l’attributo calcolato sia **[!UICONTROL Pubblicato]** o in **[!UICONTROL Bozza]**.

### Attributo calcolato pubblicato {#published}

Quando si seleziona un attributo calcolato pubblicato, viene visualizzata la pagina dei dettagli degli attributi calcolati.

![Viene visualizzata la pagina dei dettagli dell’attributo calcolato.](./images/ui/details.png)

In questa pagina viene visualizzato un riepilogo dei dettagli dell&#39;attributo calcolato, nonché un grafico che mostra la distribuzione del valore e i profili di esempio idonei per l&#39;attributo calcolato.

>[!NOTE]
>
>La distribuzione dei valori riflette la distribuzione dei valori degli attributi per i profili al momento del processo di campionamento. Il valore dell’attributo calcolato nel profilo di esempio riflette il valore del profilo unito più recente per alcuni profili di esempio.

### Attributo calcolato bozza {#draft}

Quando si seleziona una bozza di attributo calcolato, **[!UICONTROL Modifica attributi calcolati]** viene visualizzata. Questa pagina, in modo simile alla [!UICONTROL Creare attributi calcolati] , consente di modificare le informazioni di base e la definizione dell’attributo calcolato prima di aggiornare la bozza o pubblicarla.

![Il [!UICONTROL Modifica attributi calcolati] viene visualizzata.](./images/ui/edit.png)

## Utilizzo di attributi calcolati {#usage}

Dopo aver creato un attributo calcolato, puoi utilizzare **pubblicato** attributi calcolati in altri servizi a valle. Poiché gli attributi calcolati sono campi di attributi di profilo creati nello schema di unione profili, puoi cercare valori di attributi calcolati per un profilo cliente in tempo reale, utilizzarli in un pubblico, attivarli in una destinazione o utilizzarli per la personalizzazione nei percorsi in Adobe Journey Optimizer.

![Viene visualizzato il Generatore di segmenti, che mostra un attributo calcolato come parte della composizione di definizione del segmento.](./images/ui/use-ca.png)

## Passaggi successivi

Per ulteriori informazioni sugli attributi calcolati, consulta [panoramica degli attributi calcolati](./overview.md). Per informazioni sulla creazione e la configurazione di attributi calcolati tramite l’API, leggi la [guida per gli sviluppatori di attributi calcolati](./api.md).
