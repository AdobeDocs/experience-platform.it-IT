---
solution: Experience Platform
title: Guida all’interfaccia utente di Audiences
description: La funzione di composizione del pubblico nell’interfaccia utente di Adobe Experience Platform offre un’area di lavoro ricca che consente di interagire con gli elementi dati del profilo. L’area di lavoro fornisce controlli intuitivi per la creazione e la modifica dei tipi di pubblico per la tua organizzazione.
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 3852fc4eca8ea4b6b3fdcfb6aaa54315d83038b4
workflow-type: tm+mt
source-wordcount: '1913'
ht-degree: 0%

---

# Guida dell’interfaccia utente di Audience Composition

>[!NOTE]
>
>Questa guida spiega come creare tipi di pubblico utilizzando Composizione pubblico. Per scoprire come creare tipi di pubblico tramite le definizioni dei segmenti utilizzando il Generatore di segmenti, leggi [Guida dell’interfaccia utente di Segment Builder](./segment-builder.md).

La funzione Composizione pubblico fornisce un’area di lavoro per creare e modificare i tipi di pubblico, utilizzando blocchi che rappresentano azioni diverse.

![L’interfaccia utente di composizione del pubblico.](../images/ui/audience-composition/audience-composition.png)

Per modificare i dettagli della composizione, inclusi il titolo e la descrizione, selezionate ![cursori](../images/ui/audience-composition/sliders.png) pulsante.

Il **[!UICONTROL Proprietà composizione]** viene visualizzato popover. È possibile inserire i dettagli della composizione, inclusi il titolo e la descrizione qui.

![Viene visualizzata la finestra a comparsa Proprietà composizione.](../images/ui/audience-composition/composition-properties.png)

>[!NOTE]
>
>In caso affermativo **non** assegnate alla composizione un titolo, avrà un titolo &quot;Composizione&quot; seguito dalla data e dall&#39;ora di creazione per impostazione predefinita. Inoltre, ogni composizione **deve** hanno un proprio nome univoco.

Dopo aver aggiornato i dettagli della composizione, seleziona **[!UICONTROL Salva]** per confermare questi aggiornamenti. L’area di lavoro per la composizione del pubblico viene nuovamente visualizzata.

L’area di lavoro per la composizione del pubblico è composta da quattro diversi tipi di blocchi: **[[!UICONTROL Pubblico]](#audience-block)**, **[[!UICONTROL Escludi]](#exclude-block)**, **[[!UICONTROL Classifica]](#rank-block)**, e **[[!UICONTROL Dividi]](#split-block)**.

## [!UICONTROL Pubblico] {#audience-block}

Il **[!UICONTROL Pubblico]** il tipo di blocco ti consente di aggiungere i sottogruppi di pubblico che desideri comporre il nuovo pubblico più grande. Per impostazione predefinita, un **[!UICONTROL Pubblico]** Il blocco è incluso nella parte superiore dell’area di lavoro della composizione.

Quando selezioni il **[!UICONTROL Pubblico]** blocco, nella barra a destra vengono visualizzati i controlli per etichettare il pubblico, aggiungere tipi di pubblico al blocco e creare regole personalizzate per il blocco di pubblico.

>[!NOTE]
>
>Puoi aggiungere tipi di pubblico **o** crea una regola personalizzata. Queste due funzionalità **non può** essere utilizzati insieme.

![Vengono visualizzati i dettagli del blocco Audience.](../images/ui/audience-composition/audience-block.png)

### [!UICONTROL Aggiungi pubblico] {#add-audience}

Aggiungere tipi di pubblico al blocco Pubblico. seleziona **[!UICONTROL Aggiungi pubblico]**.

![Viene evidenziato il pulsante Aggiungi pubblico.](../images/ui/audience-composition/add-audience.png)

>[!IMPORTANT]
>
>Tieni presente che **solo** verranno visualizzati i tipi di pubblico definiti utilizzando il criterio di unione predefinito.
>
>Inoltre, solo **pubblicato** Puoi utilizzare i tipi di pubblico creati con Segment Builder (Generatore di segmenti). I tipi di pubblico creati utilizzando la Composizione del pubblico e quelli generati esternamente sono **non** disponibile.

Viene visualizzato un elenco di tipi di pubblico. Seleziona i tipi di pubblico da includere, seguito da **[!UICONTROL Aggiungi]** per aggiungerli al blocco di pubblico.

![Viene visualizzato un elenco di tipi di pubblico. Da questa finestra di dialogo puoi selezionare il pubblico da aggiungere.](../images/ui/audience-composition/select-audience.png)

I tipi di pubblico selezionati vengono ora visualizzati nella barra a destra quando **[!UICONTROL Pubblico]** è selezionato. Da qui, puoi modificare il tipo di unione dei tipi di pubblico combinati.

![Vengono evidenziati i possibili tipi di unione per i tipi di pubblico.](../images/ui/audience-composition/merge-types.png)

| Tipo di unione | Descrizione |
| ---------- | ----------- |
| [!UICONTROL Union] | I tipi di pubblico vengono combinati in un unico pubblico. Equivale a un&#39;operazione OR. |
| [!UICONTROL Intersezione] | I tipi di pubblico vengono combinati, con solo quelli condivisi in **tutto** di quelli che vengono aggiunti. Equivale a un&#39;operazione AND. |
| [!UICONTROL Escludi sovrapposizione] | I tipi di pubblico vengono combinati, con solo quelli condivisi in **uno, ma non tutti** di quelli che vengono aggiunti. Equivale a un&#39;operazione XOR. |

### [!UICONTROL Genera regola] {#build-rule}

Per aggiungere una regola personalizzata al blocco Pubblico, seleziona **[!UICONTROL Genera regola]**.

![Il pulsante Genera regola è evidenziato.](../images/ui/audience-composition/build-rule.png)

Viene visualizzato il Generatore di segmenti. Puoi utilizzare il Generatore di segmenti per creare una regola personalizzata che il pubblico dovrà seguire. Ulteriori informazioni sull’utilizzo del Generatore di segmenti sono disponibili nella sezione [Guida al Generatore di segmenti](./segment-builder.md).

![Viene visualizzata l’interfaccia utente del Generatore di segmenti.](../images/ui/audience-composition/segment-builder.png)

Dopo aver aggiunto una regola personalizzata, seleziona **[!UICONTROL Salva]** per aggiungere la regola al pubblico.

![](../images/ui/audience-composition/custom-rule.png)

## [!UICONTROL Escludi] {#exclude-block}

Il **[!UICONTROL Escludi]** il tipo di blocco ti consente di escludere pubblici secondari o attributi specifici dal nuovo pubblico più ampio.

Per aggiungere una **[!UICONTROL Escludi]** blocco, seleziona il **+** , seguito da **[!UICONTROL Escludi]**.

![L&#39;opzione Escludi (Exclude) è selezionata.](../images/ui/audience-composition/add-exclude-block.png)

Il **[!UICONTROL Escludi]** viene aggiunto il blocco. Quando questo blocco è selezionato, i dettagli sull’esclusione vengono visualizzati nella barra a destra. Questo include l’etichetta del blocco e il tipo di esclusione. Puoi escludere [per pubblico](#exclude-audience) o [per attributo](#exclude-attribute).

![Il blocco Escludi, che evidenzia i due diversi tipi di esclusione disponibili.](../images/ui/audience-composition/exclude.png)

### Escludi per pubblico {#exclude-audience}

Se escludi per pubblico, puoi selezionare i tipi di pubblico da escludere selezionando **[!UICONTROL Aggiungi pubblico]**.

![Il [!UICONTROL Aggiungi pubblico] che consente di scegliere il pubblico da escludere.](../images/ui/audience-composition/add-excluded-audience.png)

>[!IMPORTANT]
>
>Solo **pubblicato** Puoi utilizzare i tipi di pubblico creati con Segment Builder (Generatore di segmenti). I tipi di pubblico creati utilizzando la Composizione del pubblico e quelli generati esternamente sono **non** disponibile.

Viene visualizzato un elenco di tipi di pubblico. Seleziona **[!UICONTROL Aggiungi]** per aggiungere i tipi di pubblico da escludere al blocco di esclusione.

![Viene visualizzato un elenco di tipi di pubblico. Da questa finestra di dialogo puoi selezionare il pubblico da aggiungere.](../images/ui/audience-composition/select-audience.png)

### Escludi per attributo {#exclude-attribute}

Se si esclude per attributo, è possibile selezionare gli attributi da escludere selezionando l&#39;opzione ![filter](../images/ui/audience-composition/filter-attribute.png) all&#39;interno del **[!UICONTROL Regola di esclusione]** sezione.

![Viene evidenziata la sezione degli attributi, che mostra dove selezionare l’attributo da escludere.](../images/ui/audience-composition/exclude-attribute.png)

Viene visualizzato un elenco di attributi di profilo. Seleziona il tipo di attributo da escludere, seguito da **[!UICONTROL Seleziona]** per aggiungerli al blocco di esclusione.

![Viene visualizzato un elenco di attributi.](../images/ui/audience-composition/select-attribute-exclude.png)

>[!IMPORTANT]
>
>Quando si esclude per attributo, è possibile specificare **uno** valore da escludere. L&#39;utilizzo di qualsiasi tipo di separatore, ad esempio una virgola o un punto e virgola, determina l&#39;esclusione del valore esatto. Ad esempio, impostando il valore come `red, blue` comporterà l’esclusione del termine `red, blue` dall&#39;attributo, ma **non** si traduce nell’esclusione di uno dei termini `red` o `blue`.

## [!UICONTROL Arricchire] {#enrich-block}

>[!IMPORTANT]
>
>A questo punto, gli attributi di arricchimento possono **solo** negli scenari Adobe Journey Optimizer a valle.

Il **[!UICONTROL Arricchire]** tipo di blocco consente di arricchire il pubblico con attributi aggiuntivi da un set di dati. Puoi utilizzare questi attributi nei casi di utilizzo di personalizzazione.

Per aggiungere una **[!UICONTROL Arricchire]** blocco, seleziona il **+** , seguito da **[!UICONTROL Arricchire]**.

![Il [!UICONTROL Arricchire] è selezionata.](../images/ui/audience-composition/add-enrich-block.png)

Il **[!UICONTROL Arricchire]** viene aggiunto il blocco. Quando questo blocco è selezionato, i dettagli sull’arricchimento vengono visualizzati nella barra a destra. Questo include l’etichetta del blocco e il set di dati di arricchimento.

Per selezionare il set di dati con cui arricchire il pubblico, seleziona la ![filter](../images/ui/audience-composition/filter-attribute.png) icona.

![Il pulsante Filtro viene evidenziato. Selezionando questa opzione si arriva al [!UICONTROL Seleziona set di dati] popover.](../images/ui/audience-composition/enrich-select-dataset.png)

Il **[!UICONTROL Seleziona set di dati]** viene visualizzato popover. Seleziona il set di dati da aggiungere per l’arricchimento, seguito da **[!UICONTROL Seleziona]** per aggiungere il set di dati per l’arricchimento.

![Il set di dati selezionato è selezionato.](../images/ui/audience-composition/enrich-dataset-selected.png)

>[!IMPORTANT]
>
>Il set di dati selezionato **deve** soddisfano i seguenti criteri:
>
>- Il set di dati **deve** essere di tipo record.
>   - Il set di dati **non può** essere di tipo evento, essere generato dal sistema o essere contrassegnato per il profilo.
>- Il set di dati **deve** almeno 1 GB.

Il **[!UICONTROL Criteri di arricchimento]** viene ora visualizzata nella barra a destra. In questa sezione, puoi selezionare **[!UICONTROL Chiave di unione sorgente]** e **[!UICONTROL Chiave di unione del set di dati di arricchimento]**, che consente di collegare il set di dati di arricchimento al pubblico che stai cercando di creare.

![Il [!UICONTROL Criteri di arricchimento] viene evidenziata.](../images/ui/audience-composition/enrichment-criteria.png)

Per selezionare **[!UICONTROL Chiave di unione sorgente]**, seleziona la ![filter](../images/ui/audience-composition/filter-attribute.png) icona.

![Icona del filtro per [!UICONTROL Chiave di unione sorgente] viene evidenziato.](../images/ui/audience-composition/enrich-select-source-join-key.png)

Il **[!UICONTROL Seleziona un attributo di profilo]** viene visualizzato popover. Seleziona l’attributo di profilo da utilizzare come chiave di join di origine, seguito da **[!UICONTROL Seleziona]** per scegliere tale attributo come chiave di join di origine.

![L&#39;attributo che si desidera utilizzare come chiave di join di origine viene evidenziato.](../images/ui/audience-composition/enrich-select-profile-attribute.png)

Per selezionare **[!UICONTROL Chiave di unione del set di dati di arricchimento]**, seleziona la ![filter](../images/ui/audience-composition/filter-attribute.png) icona.

![Icona del filtro per [!UICONTROL Chiave di unione del set di dati di arricchimento] viene evidenziato.](../images/ui/audience-composition/enrich-select-enrichment-dataset-join-key.png)

Il **[!UICONTROL Attributi di arricchimento]** viene visualizzato popover. Seleziona l’attributo da utilizzare come chiave di unione del set di dati di arricchimento, seguito da **[!UICONTROL Seleziona]** per scegliere tale attributo come chiave di unione del set di dati di arricchimento.

![L’attributo che desideri utilizzare come chiave di unione del set di dati di arricchimento è evidenziato.](../images/ui/audience-composition/enrich-select-enrichment-dataset-attribute.png)

Dopo aver aggiunto entrambe le chiavi di join, **[!UICONTROL Attributi di arricchimento]** viene visualizzata la sezione. Ora puoi aggiungere l’attributo con cui desideri migliorare il pubblico. Per aggiungere questi attributi, seleziona **[!UICONTROL Aggiungi attributo]**.

![Il [!UICONTROL Aggiungi attributo] viene evidenziato.](../images/ui/audience-composition/enrich-select-add-attribute.png)

Il **[!UICONTROL Attributi di arricchimento]** viene visualizzato popover. Puoi selezionare gli attributi dal set di dati per arricchire il pubblico con, seguito da **[!UICONTROL Seleziona]** per aggiungere gli attributi al pubblico.

![Vengono evidenziati gli attributi di arricchimento che si desidera aggiungere.](../images/ui/audience-composition/enrich-add-enrichment-attributes.png)

<!-- ## [!UICONTROL Join] {#join-block}

The **[!UICONTROL Join]** block type allows you to add in external audiences from datasets that have not yet been processed by Adobe Experience Platform.

To add a **[!UICONTROL Join]** block, select the **+** icon, followed by **[!UICONTROL Join]**.

![The Join option is selected.](../images/ui/audience-composition/add-join-block.png)

When you select the block, details about the join are shown in the right rail, including the block's label and the option to add audiences to the enrichment dataset.

![The join block is highlighted, including details about the join block.](../images/ui/audience-composition/join.png)

After selecting **[!UICONTROL Add Audience]**, a list of audiences appears. Select the audiences you want to include, followed by **[!UICONTROL Add]** to add them to your join block.

![A list of audiences appears. You can select which audience you want to add from this dialog.](../images/ui/audience-composition/select-audience.png)

Your selected audiences now appear within the right rail when the **[!UICONTROL Join]** block is selected. 

![The audiences that were added as part of the Join are shown.](../images/ui/audience-composition/selected-audiences.png) -->

## [!UICONTROL Classifica] {#rank-block}

Il **[!UICONTROL Classifica]** tipo di blocco consente di classificare e ordinare i profili in base a un attributo specificato e di includerli nella composizione.

Per aggiungere una **[!UICONTROL Classifica]** blocco, seleziona il **+** , seguito da **[!UICONTROL Classifica]**.

![L’opzione Classifica è selezionata.](../images/ui/audience-composition/add-rank-block.png)

Quando selezioni il blocco, i dettagli sulla classificazione vengono visualizzati nella barra a destra, tra cui l’etichetta del blocco, l’attributo in base al quale eseguire la classificazione, l’ordine di classificazione e un interruttore per limitare il numero di profili da classificare.

![Il blocco di classificazione viene evidenziato, così come i dettagli del blocco di classificazione.](../images/ui/audience-composition/rank.png)

Per selezionare l’attributo in base al quale classificare i tipi di pubblico, seleziona la ![filter](../images/ui/audience-composition/filter-attribute.png) icona.

![L’icona del filtro è evidenziata e mostra cosa selezionare per accedere alla schermata di selezione degli attributi del profilo.](../images/ui/audience-composition/select-rank-attribute.png)

Viene visualizzato un elenco di attributi di profilo. In questo popover, puoi selezionare il tipo di attributo in base al quale classificare il pubblico. Seleziona **[!UICONTROL Seleziona]** per aggiungerlo al blocco di classificazione. L&#39;attributo selezionato può **solo** essere numeri.

![Viene visualizzato un elenco di attributi.](../images/ui/audience-composition/select-attribute-rank.png)

Dopo aver selezionato l’attributo, puoi selezionare l’ordine in base al quale classificarlo. In ordine crescente (dal più basso al più alto) o decrescente (dal più alto al più basso).

Inoltre, puoi limitare il numero di profili restituiti abilitando la funzione **[!UICONTROL Aggiungi limite profilo]** attivare/disattivare. Quando questa opzione è abilitata, puoi impostare il numero massimo di profili restituiti all’interno del **[!UICONTROL Profili inclusi]** campo.

![Viene evidenziata l’opzione Aggiungi limite profilo, che consente di limitare il numero di profili restituiti.](../images/ui/audience-composition/add-profile-limit.png)

## [!UICONTROL Dividi] {#split-block}

Il **[!UICONTROL Dividi]** il tipo di blocco ti consente di suddividere il nuovo pubblico in vari tipi di pubblico secondario. Puoi suddividere questo pubblico in base alla percentuale o a un attributo. Quando suddividi il pubblico in sottogruppi, la suddivisione è **persistente**. Ciò significa che il profilo si troverà nello stesso pubblico secondario a ogni valutazione.

Per aggiungere una **[!UICONTROL Dividi]** blocco, seleziona il **+** , seguito da **[!UICONTROL Dividi]**.

![L&#39;opzione Dividi (Split) è selezionata.](../images/ui/audience-composition/add-split-block.png)

Quando dividi il pubblico, puoi dividerlo per percentuale o per attributo.

### Dividi per percentuale {#split-percentage}

Quando si suddivide in percentuale, il pubblico viene suddiviso in modo casuale, in base al numero di percorsi e alle percentuali fornite.

Ad esempio, puoi avere tre percorsi, ciascuno con una percentuale diversa di profili.

![Viene visualizzata la suddivisione in numero di tipi di pubblico e percentuali salvati.](../images/ui/audience-composition/percentages.png)

### Dividi per attributo {#split-attribute}

Quando si divide per attributo, il pubblico viene diviso in base agli attributi forniti. Per selezionare l&#39;attributo da dividere, selezionare **[!UICONTROL Dividi]** blocco, seguito da ![filter](../images/ui/audience-composition/filter-attribute.png) icona.

![Viene selezionato il pulsante di filtro, che mostra come filtrare per attributo.](../images/ui/audience-composition/select-split-attribute.png)

Viene visualizzato un elenco di attributi di profilo. Seleziona il tipo di attributo, seguito da **[!UICONTROL Seleziona]** per aggiungerlo al blocco diviso.

![Viene visualizzato un elenco di attributi.](../images/ui/audience-composition/select-attribute-exclude.png)

Dopo aver selezionato l’attributo, puoi scegliere quali profili apparterranno a quale pubblico secondario aggiungendo i valori all’interno del **[!UICONTROL Valori]** campo.

![Vengono aggiunti i valori per i quali si desidera dividere gli attributi.](../images/ui/audience-composition/attribute-split-values.png)

Inoltre, è possibile abilitare **[!UICONTROL Altri profili]** attiva per creare un pubblico secondario composto da tutti i profili non selezionati.

![Viene evidenziata l’opzione Altri profili.](../images/ui/audience-composition/split-other-profiles.png)

## Pubblicazione del pubblico

Dopo aver composto il pubblico, puoi salvarlo e pubblicarlo selezionando **[!UICONTROL Pubblica]**.

![Viene evidenziato il pulsante Pubblica, che mostra come salvare e pubblicare il pubblico.](../images/ui/audience-composition/publish.png)

In caso di errori nella creazione del pubblico, viene visualizzato un avviso che informa su come risolvere il problema.

![Viene evidenziato il pulsante Pubblica, che mostra come salvare e pubblicare il pubblico.](../images/ui/audience-composition/audience-alert.png)

## Passaggi successivi

La funzione Composizione pubblico offre un flusso di lavoro avanzato che consente di creare tipi di pubblico da diversi tipi di blocchi. Per ulteriori informazioni su altre parti dell’interfaccia utente del servizio di segmentazione, consulta [Guida utente al servizio di segmentazione](./overview.md).
