---
title: Guida dell’interfaccia utente Attributi calcolati
description: Scopri come creare, visualizzare e aggiornare gli attributi calcolati utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: bc621167-6dba-473e-90e4-aac7ceb6579a
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 6%

---

# Guida dell’interfaccia utente attributi calcolati

>[!NOTE]
>
>Per accedere agli attributi calcolati, devi disporre delle autorizzazioni appropriate (**Visualizza attributi calcolati** e **Gestisci attributi calcolati**). Per ulteriori informazioni sulle autorizzazioni richieste, leggere la [documentazione sul controllo degli accessi](../../access-control/home.md). Per informazioni su come applicare queste autorizzazioni, leggere la [guida alla gestione delle autorizzazioni](../../access-control/ui/permissions.md).

In Adobe Experience Platform, gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate in segmentazione, attivazione e personalizzazione.

Questo documento fornisce una guida su come creare e aggiornare attributi calcolati utilizzando l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida dell&#39;interfaccia utente richiede una conoscenza dei vari servizi [!DNL Experience Platform] coinvolti nella gestione di [!DNL Real-Time Customer Profiles]. Prima di leggere questa guida o di lavorare nell’interfaccia utente, consulta la documentazione dei seguenti servizi:

- [[!DNL Real-Time Customer Profile]](../home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.

## Visualizza attributi calcolati {#view}

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Profili]** nell&#39;area di navigazione a sinistra, seguito da **[!UICONTROL Attributi calcolati]** per visualizzare un elenco degli attributi calcolati disponibili per la tua organizzazione. Ciò include informazioni sul nome, la descrizione, la data dell&#39;ultima valutazione e lo stato dell&#39;ultima valutazione dell&#39;attributo calcolato.

![La sezione [!UICONTROL Profilo] e le schede [!UICONTROL Attributi calcolati] sono evidenziate e mostrano agli utenti come accedere alla pagina Sfoglia attributi calcolati.](./images/ui/browse.png)

Per selezionare i campi visibili, è possibile selezionare ![l&#39;icona Configura colonne](/help/images/icons/column-settings.png) per aggiungere o rimuovere i campi da visualizzare.

| Campo | Descrizione |
| ----- | ----------- |
| [!UICONTROL Nome] | Nome visualizzato dell&#39;attributo calcolato. |
| [!UICONTROL Descrizione] | Descrizione dell&#39;attributo calcolato. |
| [!UICONTROL Metodo di valutazione] | Il metodo di valutazione per l&#39;attributo calcolato. Al momento, è supportato solo il **batch**. |
| [!UICONTROL Ultima valutazione] | Questo timestamp rappresenta l’ultima esecuzione di valutazione riuscita. Solo gli eventi che si sono verificati **prima** di questa marca temporale vengono considerati nell&#39;ultima valutazione riuscita. |
| [!UICONTROL Ultimo stato di valutazione] | Lo stato che indica se l’attributo calcolato è stato calcolato correttamente o meno nell’ultima esecuzione della valutazione. I valori possibili includono **[!UICONTROL Operazione riuscita]** o **[!UICONTROL Operazione non riuscita]**. |
| [!UICONTROL Frequenza di aggiornamento] | Indicazione della frequenza con cui si prevede di aggiornare l&#39;attributo calcolato. I valori possibili includono orario, giornaliero, settimanale o mensile. |
| [!UICONTROL Aggiornamento rapido] | Valore che indica se l&#39;aggiornamento rapido è abilitato o meno per questo attributo di calcolo. Se è abilitato l&#39;aggiornamento rapido, l&#39;attributo calcolato può essere aggiornato su base giornaliera anziché settimanale, bisettimanale o mensile. Questo valore è applicabile solo per attributi calcolati con un periodo di lookback superiore a una base settimanale. |
| [!UICONTROL Stato del ciclo di vita] | Stato corrente dell&#39;attributo calcolato. Esistono tre stati possibili: <ul><li>**[!UICONTROL Bozza]:** L&#39;attributo calcolato **non** ha ancora un campo creato nello schema. In questo stato, l’attributo calcolato può essere modificato. </li><li>**[!UICONTROL Pubblicato]:** L&#39;attributo calcolato ha un campo creato nello schema ed è pronto per essere utilizzato. In questo stato, l&#39;attributo calcolato **non può** essere modificato.</li><li>**[!UICONTROL Inattivo]:** L&#39;attributo calcolato è disabilitato. Per ulteriori informazioni sullo stato inattivo, leggere la [pagina delle domande frequenti](./faq.md#inactive-status). </li> |
| [!UICONTROL Creato] | Timestamp che mostra la data e l’ora di creazione dell’attributo calcolato. |
| [!UICONTROL Ultima modifica] | Timestamp che mostra la data e l’ora dell’ultima modifica apportata all’attributo calcolato. |

Puoi anche filtrare gli attributi calcolati visualizzati in base allo stato del ciclo di vita. Seleziona l&#39;icona ![funnel](/help/images/icons/filter.png).

![L&#39;icona del filtro è evidenziata.](./images/ui/select-filter.png)

Ora puoi scegliere di filtrare gli attributi calcolati per stato ([!UICONTROL Bozza], [!UICONTROL Pubblicato] e [!UICONTROL Inattivo]).

![Le opzioni per le quali è possibile filtrare gli attributi calcolati sono evidenziate. Queste opzioni includono [!UICONTROL Bozza], [!UICONTROL Pubblicato] e [!UICONTROL Inattivo].](./images/ui/view-filters.png)

Inoltre, puoi selezionare un attributo calcolato per visualizzare informazioni più dettagliate su di esso. Per ulteriori informazioni sulla pagina dei dettagli degli attributi calcolati, leggere la [sezione dei dettagli di un attributo calcolato](#view-details).

## Creare un attributo calcolato {#create}

Per creare un nuovo attributo calcolato, selezionare **[!UICONTROL Crea attributo calcolato]** per immettere il nuovo flusso di lavoro dell&#39;attributo calcolato.

![Il pulsante [!UICONTROL Crea attributi calcolati] è evidenziato e mostra agli utenti come raggiungere la pagina di creazione di attributi calcolati.](./images/ui/create.png)

Viene visualizzata la pagina **[!UICONTROL Crea attributo calcolato]**. In questa pagina è possibile aggiungere le informazioni di base per l&#39;attributo calcolato che si desidera creare.

| Campo | Descrizione |
| ----- | ----------- |
| [!UICONTROL Nome visualizzato] | Il nome con cui sarà noto l’attributo calcolato. È necessario mantenere questo nome visualizzato univoco per ogni attributo calcolato. Come best practice, questo nome visualizzato deve contenere identificatori relativi all’attributo calcolato. Ad esempio, &quot;Somma degli acquisti di scarpe degli ultimi 7 giorni&quot;. |
| [!UICONTROL Nome campo] | Nome utilizzato per fare riferimento all&#39;attributo calcolato in altri servizi a valle. Questo nome deriva automaticamente dal nome visualizzato ed è scritto in camelCase. |
| [!UICONTROL Descrizione] | Descrizione dell&#39;attributo calcolato che si sta tentando di creare. |

![La sezione [!UICONTROL Informazioni di base] della pagina [!UICONTROL Crea attributo calcolato] è evidenziata.](./images/ui/basic-information.png)

Dopo aver aggiunto i dettagli dell’attributo calcolato, puoi iniziare a definire le regole.

### Specificare le condizioni di filtro degli eventi

Per creare una regola, seleziona innanzitutto gli attributi dalla sezione **[!UICONTROL Eventi]** per filtrare gli eventi su cui desideri aggregare. Attualmente, sono supportati solo attributi evento di tipo non array.

![La sezione [!UICONTROL Events] è evidenziata.](./images/ui/events.png)

Dopo aver selezionato l’attributo da utilizzare nella definizione dell’attributo calcolato, puoi scegliere a cosa verrà confrontato questo valore.

![Vengono visualizzati i tipi di confronto disponibili.](./images/ui/select-comparison.png)

### Applica funzione di aggregazione

Ora puoi applicare una funzione al campo dall’output condizionale. Selezionare innanzitutto il tipo di funzione di aggregazione. Le opzioni disponibili includono [!UICONTROL Somma], [!UICONTROL Min], [!UICONTROL Max], [!UICONTROL Conteggio] e [!UICONTROL Più recente]. Ulteriori informazioni su queste funzioni sono disponibili nella [sezione funzioni](./overview.md#functions) della panoramica degli attributi calcolati.

![Vengono visualizzate le funzioni degli attributi calcolati.](./images/ui/select-function.png)

Dopo aver scelto una funzione, puoi scegliere il campo su cui eseguire l’aggregazione. I campi idonei da scegliere dipendono dalla funzione selezionata.

![Nel campo evidenziato è visualizzato l&#39;attributo che si sta scegliendo di aggregare la funzione.](./images/ui/select-eligible-field.png)

### Durata lookback

Dopo aver applicato la funzione di aggregazione, è necessario definire il periodo di lookback dell’attributo calcolato. Questo periodo di lookback specifica per quanto tempo desideri aggregare gli eventi. Questa durata del lookback può essere specificata in termini di ore, giorni, settimane o mesi.

![La durata del lookback è evidenziata.](./images/ui/select-lookback-duration.png)

### Aggiornamento rapido {#fast-refresh}

>[!CONTEXTUALHELP]
>id="platform_profile_computedAttributes_fastRefresh"
>title="Aggiornamento rapido"
>abstract="L’aggiornamento rapido consente di mantenere aggiornati gli attributi. L’abilitazione di questa opzione consente di aggiornare gli attributi calcolati su base giornaliera, anche per periodi di lookback più lunghi, per poter reagire rapidamente alle attività degli utenti. Questo valore è applicabile solo per attributi calcolati con un periodo di lookback superiore a una base settimanale."

Quando si applica la funzione di aggregazione, è possibile abilitare l’aggiornamento rapido se il periodo di lookback è superiore a una settimana.

![La casella di controllo [!UICONTROL Aggiornamento rapido] è evidenziata.](./images/ui/enable-fast-refresh.png)

L’aggiornamento rapido consente di mantenere aggiornati gli attributi. L’abilitazione di questa opzione consente di aggiornare gli attributi calcolati su base giornaliera, anche per periodi di lookback più lunghi, per poter reagire rapidamente alle attività degli utenti.

Per ulteriori informazioni sull&#39;aggiornamento rapido, leggere la [sezione sull&#39;aggiornamento rapido](./overview.md#fast-refresh) della panoramica degli attributi calcolati.

Una volta completati questi passaggi, puoi scegliere se salvare l’attributo calcolato come bozza o pubblicarlo immediatamente.

![I pulsanti [!UICONTROL Salva come bozza] e [!UICONTROL Publish] sono evidenziati.](./images/ui/draft-or-publish.png)

## Visualizzare i dettagli di un attributo calcolato {#view-details}

Per visualizzare i dettagli di un attributo calcolato, selezionare l&#39;attributo calcolato che si desidera visualizzare nella pagina [!UICONTROL **Sfoglia**].

![Un attributo calcolato è evidenziato.](./images/ui/select.png)

Il contenuto della pagina varia a seconda che l&#39;attributo calcolato sia **[!UICONTROL Pubblicato]** o in **[!UICONTROL Bozza]**.

### Attributo calcolato pubblicato {#published}

Quando si seleziona un attributo calcolato pubblicato, viene visualizzata la pagina dei dettagli degli attributi calcolati.

![Viene visualizzata la pagina dei dettagli dell&#39;attributo calcolato.](./images/ui/details.png)

In questa pagina viene visualizzato un riepilogo dei dettagli dell&#39;attributo calcolato, nonché un grafico che mostra la distribuzione del valore e i profili di esempio idonei per l&#39;attributo calcolato.

>[!NOTE]
>
>La distribuzione dei valori riflette la distribuzione dei valori degli attributi per i profili al momento del processo di campionamento. Il valore dell’attributo calcolato nel profilo di esempio riflette il valore del profilo unito più recente per alcuni profili di esempio.

### Attributo calcolato bozza {#draft}

Quando si seleziona una bozza di attributo calcolato, viene visualizzata la pagina **[!UICONTROL Modifica attributi calcolati]**. Questa pagina, simile alla pagina [!UICONTROL Crea attributi calcolati], consente di modificare le informazioni di base dell&#39;attributo calcolato e la relativa definizione prima di aggiornare la bozza o pubblicarla.

![Viene visualizzata la pagina [!UICONTROL Modifica attributi calcolati].](./images/ui/edit.png)

## Utilizzo di attributi calcolati {#usage}

>[!IMPORTANT]
>
>Se utilizzi un attributo calcolato con la funzione **Most Recent** in una definizione di segmento, **devi** includere **entrambi** il valore e il valore timestamp nell&#39;oggetto attributo calcolato.
>
>Ad esempio, se stai creando una definizione di segmento che sta cercando &quot;Tutti i profili con un indirizzo e-mail valido&quot; in cui il campo dell&#39;indirizzo e-mail è compilato da un attributo calcolato con la funzione più recente, **devi** includere sia il valore dell&#39;indirizzo e-mail che il **e** timestamp dell&#39;indirizzo e-mail esistente.

Dopo aver creato un attributo calcolato, puoi utilizzare gli attributi calcolati **published** in altri servizi a valle. Poiché gli attributi calcolati sono campi di attributi di profilo creati nello schema di unione profili, puoi cercare valori di attributi calcolati per un profilo cliente in tempo reale, utilizzarli in un pubblico, attivarli in una destinazione o utilizzarli per la personalizzazione nei percorsi in Adobe Journey Optimizer.

>[!NOTE]
>
>Gli attributi calcolati **non possono** essere utilizzati nelle **composizioni** del pubblico.

![Viene visualizzato il Generatore di segmenti, che mostra un attributo calcolato come parte della composizione della definizione del segmento.](./images/ui/use-ca.png)

## Passaggi successivi

Per ulteriori informazioni sugli attributi calcolati, leggere la [panoramica sugli attributi calcolati](./overview.md). Per informazioni sulla creazione e la configurazione di attributi calcolati tramite l&#39;API, leggere la [guida per gli sviluppatori di attributi calcolati](./api.md).
