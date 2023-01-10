---
keywords: Experience Platform;home;argomenti popolari;servizio di segmentazione;segmentazione;servizio di segmentazione;guida utente;guida utente;guida utente;guida utente di Audiences;guida utente di Audiences;audience builder;audience;audiences;guida interfaccia utente di Audiences;
solution: Experience Platform
title: Guida all'interfaccia utente di Audiences
description: Audience Builder nell’interfaccia utente di Adobe Experience Platform offre un’area di lavoro ricca che consente di interagire con gli elementi dati di profilo. L’area di lavoro offre controlli intuitivi per la creazione e la modifica di tipi di pubblico per la tua organizzazione.
hide: true
hidefromtoc: true
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 1%

---

# Guida all’interfaccia utente di Audience Builder

>[!IMPORTANT]
>
>Audience Builder è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Audience Builder fornisce un’area di lavoro per creare e modificare i tipi di pubblico, utilizzando i blocchi utilizzati per rappresentare azioni diverse.

![Interfaccia utente di Audience Builder.](../images/ui/audience-builder/audience-builder.png)

L’area di lavoro della composizione del pubblico è composta da cinque diversi tipi di blocchi: **[[!UICONTROL Pubblico]](#audience-block)**, **[[!UICONTROL Escludi]](#exclude-block)**, **[[!UICONTROL Iscriviti]](#join-block)**, **[[!UICONTROL Classificazione]](#rank-block)** e **[[!UICONTROL Divisione]](#split-block)**.

## [!UICONTROL Destinatari] {#audience-block}

La **[!UICONTROL Pubblico]** il tipo di blocco ti consente di aggiungere i tipi di pubblico secondari che desideri comporre per il nuovo pubblico più grande. Per impostazione predefinita, un **[!UICONTROL Pubblico]** il blocco è incluso nella parte superiore dell&#39;area di composizione.

Quando selezioni la **[!UICONTROL Pubblico]** nella barra a destra sono visualizzati i controlli per l’etichettatura e l’aggiunta di tipi di pubblico al blocco .

![Vengono visualizzati i dettagli del blocco Pubblico .](../images/ui/audience-builder/select-audience.png)

Dopo aver selezionato **[!UICONTROL Aggiungi pubblico]**, viene visualizzato un elenco di tipi di pubblico. Seleziona il pubblico da includere, seguito da **[!UICONTROL Aggiungi]** per aggiungerli al blocco del pubblico.

![Viene visualizzato un elenco di tipi di pubblico. Puoi selezionare il pubblico da aggiungere da questa finestra di dialogo.](../images/ui/audience-builder/select-audience.png)

I tipi di pubblico selezionati vengono ora visualizzati nella barra a destra quando **[!UICONTROL Pubblico]** blocco selezionato. Da qui puoi modificare il tipo di unione dei tipi di pubblico combinati.

![Vengono evidenziati i possibili tipi di unione per i tipi di pubblico.](../images/ui/audience-builder/merge-types.png)

| Tipo di unione | Descrizione |
| ---------- | ----------- |
| [!UICONTROL Unione] | I tipi di pubblico vengono combinati in un unico pubblico. Equivale a un&#39;operazione OR. |
| [!UICONTROL Intersection] | I tipi di pubblico vengono combinati, con solo i tipi di pubblico condivisi in **tutto** di essere aggiunti. Equivale a un&#39;operazione AND. |
| [!UICONTROL Escludi sovrapposizione] | I tipi di pubblico vengono combinati, con solo i tipi di pubblico condivisi in **uno, ma non tutti** di essere aggiunti. Equivale a un&#39;operazione XOR. |

## [!UICONTROL Escludi] {#exclude-block}

La **[!UICONTROL Escludi]** il tipo di blocco ti consente di escludere tipi di pubblico o attributi specifici dal nuovo pubblico più grande.

Per aggiungere un **[!UICONTROL Escludi]** blocco, seleziona **+** , seguita da **[!UICONTROL Escludi]**.

![L’opzione Escludi è selezionata.](../images/ui/audience-builder/add-exclude-block.png)

La **[!UICONTROL Escludi]** viene aggiunto il blocco . Quando questo blocco è selezionato, i dettagli relativi all’esclusione vengono visualizzati nella barra a destra. Questo include l’etichetta e il tipo di esclusione del blocco. Puoi escludere [per pubblico](#exclude-audience) o [per attributo](#exclude-attribute).

![Il blocco Escludi , evidenziando i due diversi tipi di esclusione disponibili.](../images/ui/audience-builder/exclude.png)

### Escludi per pubblico {#exclude-audience}

Se escludi per pubblico, puoi selezionare i tipi di pubblico da escludere selezionando **[!UICONTROL Aggiungi pubblico]**.

![Il pulsante Aggiungi pubblico è selezionato e consente di scegliere il pubblico da escludere.](../images/ui/audience-builder/add-excluded-audience.png)

Viene visualizzato un elenco di tipi di pubblico. Seleziona **[!UICONTROL Aggiungi]** per aggiungere i tipi di pubblico da escludere al blocco exclude.

![Viene visualizzato un elenco di tipi di pubblico. Puoi selezionare il pubblico da aggiungere da questa finestra di dialogo.](../images/ui/audience-builder/select-audience.png)

### Escludi per attributo {#exclude-attribute}

Se escludi per attributo, puoi selezionare gli attributi da escludere selezionando la ![filter](../images/ui/audience-builder/filter-attribute.png) all’interno dell’icona **[!UICONTROL Regola di esclusione]** sezione .

![La sezione attributo è evidenziata e mostra dove selezionare per scegliere l’attributo da escludere.](../images/ui/audience-builder/exclude-attribute.png)

Viene visualizzato un elenco di attributi di profilo. Seleziona il tipo di attributo da escludere, seguito da **[!UICONTROL Seleziona]** per aggiungerli al blocco di esclusione.

![Viene visualizzato un elenco di attributi.](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL Iscriversi] {#join-block}

La **[!UICONTROL Iscriviti]** il tipo di blocco consente di aggiungere tipi di pubblico esterni da set di dati non ancora elaborati da Adobe Experience Platform.

Per aggiungere una **[!UICONTROL Iscriviti]** blocco, seleziona **+** , seguita da **[!UICONTROL Iscriviti]**.

![L’opzione Unisci è selezionata.](../images/ui/audience-builder/add-join-block.png)

Quando selezioni il blocco , i dettagli sul join vengono visualizzati nella barra a destra, inclusa l’etichetta del blocco e l’opzione per aggiungere tipi di pubblico al set di dati di arricchimento.

![Il blocco di join viene evidenziato, inclusi i dettagli sul blocco di join.](../images/ui/audience-builder/join.png)

Dopo aver selezionato **[!UICONTROL Aggiungi pubblico]**, viene visualizzato un elenco di tipi di pubblico. Seleziona il pubblico da includere, seguito da **[!UICONTROL Aggiungi]** per aggiungerli al blocco di join.

![Viene visualizzato un elenco di tipi di pubblico. Puoi selezionare il pubblico da aggiungere da questa finestra di dialogo.](../images/ui/audience-builder/select-audience.png)

I tipi di pubblico selezionati vengono ora visualizzati nella barra a destra quando **[!UICONTROL Iscriviti]** blocco selezionato.

![Vengono visualizzati i tipi di pubblico aggiunti come parte del join.](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL Classificazione] {#rank-block}

La **[!UICONTROL Classificazione]** il tipo di blocco ti consente di classificare e ordinare i tipi di pubblico prima che il nuovo pubblico venga pubblicato.

Per aggiungere una **[!UICONTROL Classificazione]** blocco, seleziona **+** , seguita da **[!UICONTROL Classificazione]**.

![L’opzione Classifica è selezionata.](../images/ui/audience-builder/add-rank-block.png)

Quando selezioni il blocco , i dettagli sulla classificazione vengono visualizzati nella barra a destra, inclusa l’etichetta del blocco, l’attributo da classificare, l’ordine di classificazione e un interruttore per limitare il numero di profili alla classificazione.

![Viene evidenziato il blocco di classificazione e i dettagli del blocco di classificazione.](../images/ui/audience-builder/rank.png)

Per selezionare l&#39;attributo per cui classificare i tipi di pubblico, seleziona la ![filter](../images/ui/audience-builder/filter-attribute.png) icona.

![L’icona del filtro viene evidenziata e mostra cosa selezionare per accedere alla schermata di selezione dell’attributo del profilo.](../images/ui/audience-builder/select-rank-attribute.png)

Viene visualizzato un elenco di attributi di profilo. Su questo pover, puoi selezionare il tipo di attributo per il quale vuoi classificare il pubblico. Seleziona **[!UICONTROL Seleziona]** per aggiungerlo al blocco di rango. L&#39;attributo selezionato può essere **only** essere di tipo `int`.

![Viene visualizzato un elenco di attributi.](../images/ui/audience-builder/select-attribute.png)

Dopo aver selezionato l’attributo, puoi selezionare l’ordine in cui classificarlo. In ordine crescente (dal più basso al più alto) o decrescente (dal più alto al più basso).

Inoltre, puoi limitare il numero di tipi di pubblico restituiti abilitando il **[!UICONTROL Aggiungi limite profilo]** alternare. Quando questa opzione è attivata, puoi impostare il numero massimo di tipi di pubblico restituiti all’interno della **[!UICONTROL Profili inclusi]** campo .

![L’opzione Aggiungi limite profilo è evidenziata e consente di limitare il numero di tipi di pubblico restituiti.](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL Dividere] {#split-block}

La **[!UICONTROL Divisione]** il tipo di blocco ti consente di suddividere il nuovo pubblico in vari sottotipi di pubblico. Puoi suddividere questo pubblico in base alla percentuale o a un attributo.

Per aggiungere una **[!UICONTROL Divisione]** blocco, seleziona **+** , seguita da **[!UICONTROL Divisione]**.

![L’opzione Dividi è selezionata.](../images/ui/audience-builder/add-split-block.png)

### Suddivisione per percentuale {#split-percentage}

Quando si suddivide in percentuale, i tipi di pubblico vengono suddivisi in modo casuale, in base al numero di percorsi e alle percentuali fornite.

Ad esempio, puoi avere tre percorsi, ciascuno con una percentuale diversa di profili.

![Viene visualizzata la suddivisione del numero di tipi di pubblico e percentuali salvati.](../images/ui/audience-builder/percentages.png)

Inoltre, puoi contrassegnare uno dei tipi di pubblico suddivisi come gruppo di controllo.

![L’interruttore del gruppo di controllo è attivato. Questo consente di contrassegnare uno dei tipi di pubblico suddivisi come gruppo di controllo.](../images/ui/audience-builder/control-group.png)

### Divisione per attributo {#split-attribute}

Quando si suddivide per attributo, i tipi di pubblico vengono suddivisi in base agli attributi forniti. Per selezionare l&#39;attributo per il quale eseguire la suddivisione, selezionare la **[!UICONTROL Divisione]** blocco, seguito dal ![filter](../images/ui/audience-builder/filter-attribute.png) icona.

![Il pulsante filtro è selezionato e mostra come filtrare per attributo.](../images/ui/audience-builder/select-attribute-split.png)

Viene visualizzato un elenco di attributi di profilo. Seleziona il tipo di attributo, seguito da **[!UICONTROL Seleziona]** per aggiungerlo al blocco di divisione.

![Viene visualizzato un elenco di attributi.](../images/ui/audience-builder/select-attribute.png)

Dopo aver selezionato l’attributo , puoi scegliere i profili a cui appartiene il sottopubblico aggiungendo i valori all’interno del **[!UICONTROL Valori]** campo .

![Vengono aggiunti i valori per i quali si desidera dividere gli attributi.](../images/ui/audience-builder/attribute-split-values.png)

Inoltre, puoi abilitare il **[!UICONTROL Altri profili]** per creare un pubblico secondario composto da tutti i profili non selezionati.

![L’opzione Altri profili viene evidenziata.](../images/ui/audience-builder/attribute-split-other-profiles.png)

## Pubblicazione del pubblico

Dopo aver creato il pubblico, puoi salvarlo e pubblicarlo selezionando **[!UICONTROL Pubblica]**.

![Il pulsante Pubblica è evidenziato e illustra come salvare e pubblicare il pubblico.](../images/ui/audience-builder/publish-audience.png)

In caso di errori durante la creazione del pubblico, viene visualizzato un avviso che ti informa su come risolvere il problema.

![Il pulsante Pubblica è evidenziato e illustra come salvare e pubblicare il pubblico.](../images/ui/audience-builder/audience-alert.png)

## Passaggi successivi

Audience Builder fornisce un flusso di lavoro ricco che consente di creare tipi di pubblico dai diversi tipi di blocchi. Per ulteriori informazioni su altre parti dell’interfaccia utente del servizio di segmentazione, consulta la sezione [Guida utente al servizio di segmentazione](./overview.md).
