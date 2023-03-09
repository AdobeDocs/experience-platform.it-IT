---
keywords: Experience Platform;home;argomenti popolari;Applicazione dei criteri;Applicazione automatica;Imposizione basata su API;governance dei dati
solution: Experience Platform
title: Applicazione automatica dei criteri
description: Questo documento illustra come i criteri di utilizzo dei dati vengono applicati automaticamente quando si attivano i segmenti nelle destinazioni in Experience Platform.
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: 30d8cc73128cff444ce06a8ab913aeb8fa816ed1
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 0%

---

# Applicazione automatica dei criteri

>[!IMPORTANT]
>
>L’applicazione automatica dei criteri è disponibile solo per le organizzazioni che hanno acquistato **Schermo sanitario Adobe** o **Adobe Privacy &amp; Security Shield**.

Una volta etichettati i dati e definiti i criteri di utilizzo dei dati, puoi applicare la conformità dell’utilizzo dei dati ai criteri. Quando si attivano i segmenti di pubblico nelle destinazioni, Adobe Experience Platform applica automaticamente i criteri di utilizzo in caso di violazioni.

>[!NOTE]
>
>Questo documento si concentra sull’applicazione della governance dei dati e dei criteri di consenso. Per informazioni sui criteri di controllo degli accessi, consulta la documentazione su [controllo degli accessi basato su attributi](../../access-control/abac/overview.md).

## Prerequisiti

Questa guida richiede una buona conoscenza dei servizi Platform coinvolti nell’applicazione automatica. Per ulteriori informazioni, consulta la seguente documentazione prima di continuare con questa guida:

* [Governance dei dati Adobe Experience Platform](../home.md): framework tramite il quale Platform applica la conformità dell’utilizzo dei dati tramite l’utilizzo di etichette e criteri.
* [Profilo cliente in tempo reale](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio di segmentazione di Adobe Experience Platform](../../segmentation/home.md): il motore di segmentazione in [!DNL Platform] utilizzato per creare segmenti di pubblico dai profili dei clienti in base ai comportamenti e agli attributi dei clienti.
* [Destinazioni](../../destinations/home.md): le destinazioni sono integrazioni predefinite con applicazioni di uso comune che consentono l’attivazione diretta dei dati da Platform per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e altro ancora.

## Flusso di applicazione {#flow}

Il diagramma seguente illustra come l’applicazione dei criteri viene integrata nel flusso di dati dell’attivazione dei segmenti:

![](../images/enforcement/enforcement-flow.png)

Quando un segmento viene attivato per la prima volta, [!DNL Policy Service] verifica delle politiche applicabili sulla base dei seguenti fattori:

* Le etichette di utilizzo dei dati applicate ai campi e ai set di dati all’interno del segmento da attivare.
* Lo scopo di marketing della destinazione.
* I profili che hanno acconsentito a essere inclusi nell’attivazione del segmento, in base ai criteri di consenso configurati.

>[!NOTE]
>
>Se esistono etichette di utilizzo dei dati che sono state applicate solo a determinati campi all’interno di un set di dati (anziché all’intero set di dati), l’applicazione di tali etichette a livello di campo all’attivazione avviene solo nelle seguenti condizioni:
>
>* I campi vengono utilizzati nella definizione del segmento.
>* I campi sono configurati come attributi previsti per la destinazione target.


## Derivazione dei dati {#lineage}

La derivazione dei dati svolge un ruolo chiave nel modo in cui i criteri vengono applicati in Platform. In termini generali, la derivazione dei dati si riferisce all’origine di un set di dati e a cosa gli accade (o dove si sposta) nel tempo.

Nel contesto della governance dei dati, la derivazione consente alle etichette di utilizzo dei dati di propagarsi dai set di dati ai servizi a valle che utilizzano i loro dati, come Profilo cliente in tempo reale e destinazioni. Questo consente di valutare e applicare i criteri in diversi punti chiave del percorso dei dati tramite Platform e fornisce ai consumatori di dati il contesto necessario per capire perché si è verificata una violazione dei criteri.

Ad Experience Platform, l’applicazione delle policy riguarda la seguente derivazione:

1. I dati vengono acquisiti in Platform e memorizzati in **set di dati**.
1. I profili dei clienti sono identificati e costruiti da tali set di dati unendo i frammenti di dati in base al **criterio di unione**.
1. I gruppi di profili sono suddivisi in **segmenti** in base agli attributi comuni.
1. I segmenti vengono attivati a valle **destinazioni**.

Ciascuna fase del calendario di cui sopra rappresenta un’entità che può contribuire all’applicazione delle politiche, come indicato nella tabella seguente:

| Fase di derivazione dei dati | Ruolo nell’applicazione dei criteri |
| --- | --- |
| Set di dati | I set di dati contengono etichette di utilizzo dei dati (applicate a livello di set di dati o di campo) che definiscono i casi di utilizzo per i quali è possibile utilizzare l’intero set di dati o campi specifici. Se un set di dati o un campo contenente determinate etichette viene utilizzato per uno scopo limitato da un criterio, si verificheranno violazioni dei criteri.<br><br>Nei set di dati vengono memorizzati anche tutti gli attributi di consenso raccolti dai clienti. Se hai accesso ai criteri di consenso, tutti i profili che non soddisfano i requisiti di attributo del consenso dei tuoi criteri verranno esclusi dai segmenti attivati per una destinazione. |
| Criterio di unione | I criteri di unione sono le regole utilizzate da Platform per determinare il modo in cui assegnare la priorità ai dati quando si uniscono frammenti da più set di dati. Se i criteri di unione sono configurati in modo che i set di dati con etichette con restrizioni vengano attivati in una destinazione, si verificheranno violazioni dei criteri. Consulta la [panoramica dei criteri di unione](../../profile/merge-policies/overview.md) per ulteriori informazioni. |
| Segmento | Le regole del segmento definiscono quali attributi devono essere inclusi dai profili cliente. A seconda dei campi inclusi in una definizione di segmento, il segmento erediterà tutte le etichette di utilizzo applicate per tali campi. Se attivi un segmento le cui etichette ereditate sono limitate dai criteri applicabili della destinazione target, in base al caso di utilizzo di marketing, si verificheranno violazioni dei criteri. |
| Destinazione | Durante la configurazione di una destinazione, è possibile definire un’azione di marketing (talvolta denominata caso di utilizzo di marketing). Questo caso d’uso è correlato a un’azione di marketing definita in un criterio. In altre parole, l’azione di marketing che definisci per una destinazione determina quali criteri di utilizzo dei dati e criteri di consenso sono applicabili a tale destinazione.<br><br>Le violazioni dei criteri di utilizzo dei dati si verificano se si attiva un segmento le cui etichette di utilizzo sono limitate per l’azione di marketing della destinazione target.<br><br>(Beta) Quando un segmento viene attivato, tutti i profili che non contengono gli attributi di consenso richiesti per l’azione di marketing (come definiti dai criteri di consenso) vengono esclusi dal pubblico attivato. |

>[!IMPORTANT]
>
>Alcuni criteri di utilizzo dati possono specificare due o più etichette con una relazione AND. Ad esempio, un criterio potrebbe limitare un’azione di marketing se le etichette `C1` E `C2` sono entrambi presenti, ma non limita la stessa azione se è presente solo una di tali etichette.
>
>Per quanto riguarda l’applicazione automatica, il framework di governance dei dati non considera l’attivazione di segmenti separati a una destinazione come una combinazione di dati. Pertanto, l’esempio `C1 AND C2` il criterio è **NOT** applicato se queste etichette sono incluse in segmenti separati. Questo criterio viene invece applicato solo quando entrambe le etichette sono presenti nello stesso segmento al momento dell’attivazione.

Quando si verificano violazioni dei criteri, i messaggi risultanti visualizzati nell’interfaccia utente forniscono utili strumenti per esplorare la derivazione dei dati che contribuiscono alla violazione e contribuire alla risoluzione del problema. Maggiori dettagli sono forniti nella sezione successiva.

## Messaggi di applicazione dei criteri {#enforcement}

Le sezioni seguenti descrivono i diversi messaggi di applicazione dei criteri visualizzati nell’interfaccia utente di Platform:

* [Violazione dei criteri di utilizzo dei dati](#data-usage-violation)
* [Valutazione dei criteri di consenso](#consent-policy-evaluation)

### Violazione dei criteri di utilizzo dei dati {#data-usage-violation}

Se si verifica una violazione dei criteri dal tentativo di attivare un segmento (o [apportare modifiche a un segmento già attivato](#policy-enforcement-for-activated-segments)) l&#39;azione è impedita e viene visualizzato un messaggio a comparsa che indica che uno o più criteri sono stati violati. Una volta attivata la violazione, **[!UICONTROL Salva]** il pulsante è disattivato per l’entità da modificare finché i componenti appropriati non vengono aggiornati per conformarsi ai criteri di utilizzo dei dati.

Selezionare una violazione dei criteri nella colonna sinistra del popover per visualizzare i dettagli relativi a tale violazione.

![](../images/enforcement/violation-policy-select.png)

Il messaggio di violazione fornisce un riepilogo del criterio violato, incluse le condizioni che il criterio è configurato per verificare, l’azione specifica che ha attivato la violazione e un elenco delle possibili risoluzioni del problema.

![](../images/enforcement/violation-summary.png)

Sotto il riepilogo delle violazioni viene visualizzato un grafico di derivazione dei dati che consente di visualizzare i set di dati, i criteri di unione, i segmenti e le destinazioni coinvolti nella violazione dei criteri. L’entità che stai modificando viene evidenziata nel grafico, indicando quale punto del flusso sta causando la violazione. Puoi selezionare un nome di entità all’interno del grafico per aprire la pagina dei dettagli dell’entità in questione.

![](../images/enforcement/data-lineage.png)

È inoltre possibile utilizzare **[!UICONTROL Filtro]** icona (![](../images/enforcement/filter.png)) per filtrare le entità visualizzate per categoria. È necessario selezionare almeno due categorie per visualizzare i dati.

![](../images/enforcement/lineage-filter.png)

Seleziona **[!UICONTROL Vista a elenco]** per visualizzare la derivazione dati come elenco. Per tornare al grafico visivo, seleziona **[!UICONTROL Vista percorso]**.

![](../images/enforcement/list-view.png)

### Valutazione dei criteri di consenso {#consent-policy-evaluation}

Se è stato [criteri di consenso creati](../policies/user-guide.md#consent-policy) e quando attivi un segmento in una destinazione, puoi vedere in che modo i tuoi criteri di consenso influiscono sulla percentuale di profili inclusi nell’attivazione.

#### Miglioramento dei criteri di consenso per gli elementi multimediali a pagamento {#consent-policy-enhancement}

È stato apportato un miglioramento all’applicazione dei criteri di consenso sulle destinazioni batch e di streaming, comprese le attivazioni di file multimediali a pagamento. Questo miglioramento è disponibile per i clienti di Privacy and Security Shield o Healthcare Shield e rimuove in modo proattivo i profili da destinazioni batch e streaming quando lo stato del consenso cambia. Inoltre, assicura che le modifiche del consenso vengano propagate immediatamente in modo che il pubblico giusto sia sempre mirato.

Questi miglioramenti consentono una maggiore fiducia nella strategia di marketing, in quanto eliminano la necessità per gli addetti al marketing di aggiungere manualmente attributi di consenso alla propria espressione di segmento. In questo modo, nessun profilo viene inavvertitamente sottoposto a targeting per alcuna esperienza di marketing dopo il ritiro del consenso o la cessazione degli stessi per un criterio di consenso. I criteri di consenso marketing che impostano regole per la gestione dei dati di consenso o preferenze nei vari flussi di lavoro di marketing vengono ora applicati automaticamente nei flussi di lavoro di attivazione nelle soluzioni a valle.

>[!NOTE]
>
>Questo miglioramento non comporta modifiche all’interfaccia utente.

#### Valutazione pre-attivazione

Una volta raggiunta la **[!UICONTROL Revisione]** passaggio quando [attivazione di una destinazione](../../destinations/ui/activation-overview.md), seleziona **[!UICONTROL Visualizza criteri applicati]**.

![Pulsante Visualizza criteri applicati nel flusso di lavoro di attivazione della destinazione](../images/enforcement/view-applied-policies.png)

Viene visualizzata una finestra di dialogo di verifica dei criteri, con un’anteprima di come i criteri di consenso influiscono sul pubblico autorizzato dei segmenti attivati.

![Finestra di dialogo di controllo dei criteri di consenso nell’interfaccia utente di Platform](../images/enforcement/consent-policy-check.png)

La finestra di dialogo mostra il pubblico autorizzato per un segmento alla volta. Per visualizzare la valutazione dei criteri per un segmento diverso, utilizza il menu a discesa sopra il diagramma per selezionarne uno dall’elenco.

![Selettore di segmenti nella finestra di dialogo di controllo dei criteri](../images/enforcement/segment-switcher.png)

Utilizza la barra a sinistra per passare dai criteri di consenso applicabili per il segmento selezionato a quelli applicabili. I criteri non selezionati sono rappresentati nella sezione &quot;[!UICONTROL Altre politiche]&quot; del diagramma.

![Selettore criteri nella finestra di dialogo di controllo criteri](../images/enforcement/policy-switcher.png)

Il diagramma mostra la sovrapposizione tra tre gruppi di profili:

1. Profili idonei per il segmento selezionato
1. Profili idonei per il criterio di consenso selezionato
1. Profili idonei per gli altri criteri di consenso applicabili per il segmento (denominati &quot;[!UICONTROL Altre politiche]&quot;).

I profili idonei per tutti e tre i gruppi di cui sopra rappresentano il pubblico autorizzato per il segmento selezionato, riepilogato nella barra a destra.

![Sezione Riepilogo nella finestra di dialogo di controllo dei criteri](../images/enforcement/summary.png)

Passa il puntatore del mouse su uno dei tipi di pubblico nel diagramma per visualizzare il numero di profili in esso contenuti.

![Evidenziazione di una sezione di diagramma nella finestra di dialogo di controllo dei criteri](../images/enforcement/highlight-segment.png)

Il pubblico autorizzato è rappresentato dalla sovrapposizione centrale del diagramma e può essere evidenziato come le altre sezioni.

![Evidenziazione del pubblico autorizzato nel diagramma](../images/enforcement/consented-audience.png)

#### Applicazione esecuzione flusso

Quando i dati vengono attivati su una destinazione, i dettagli di esecuzione del flusso mostrano il numero di identità escluse a causa di criteri di consenso attivi.

![Metriche delle identità escluse per un’esecuzione di flusso di dati](../images/enforcement/dataflow-run-enforcement.png)

## Applicazione dei criteri per i segmenti attivati {#policy-enforcement-for-activated-segments}

L’applicazione dei criteri si applica comunque ai segmenti dopo la loro attivazione, limitando eventuali modifiche a un segmento o alla sua destinazione che potrebbero causare una violazione dei criteri. Per come [derivazione dati](#lineage) funziona nell’applicazione dei criteri e una qualsiasi delle seguenti azioni può potenzialmente attivare una violazione:

* Aggiornamento delle etichette di utilizzo dei dati
* Modifica dei set di dati per un segmento
* Modifica dei predicati dei segmenti
* Modifica delle configurazioni di destinazione

Se una delle azioni di cui sopra attiva una violazione, tale azione non può essere salvata e viene visualizzato un messaggio di violazione dei criteri, per garantire che i segmenti attivati continuino a essere conformi ai criteri di utilizzo dei dati durante la modifica.

## Passaggi successivi

In questo documento viene illustrato il funzionamento dell’applicazione automatica delle policy in Experience Platform. Per i passaggi su come integrare in modo programmatico l’applicazione dei criteri nelle applicazioni utilizzando le chiamate API, consulta la guida su [Imposizione basata su API](./api-enforcement.md).
