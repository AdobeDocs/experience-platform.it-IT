---
solution: Experience Platform
title: Guida all’interfaccia utente di Audiences
description: La funzione di composizione del pubblico nell’interfaccia utente di Adobe Experience Platform offre un’area di lavoro ricca che consente di interagire con gli elementi dati del profilo. L’area di lavoro fornisce controlli intuitivi per la creazione e la modifica dei tipi di pubblico per la tua organizzazione.
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: e17403f0529c5b94869d3bd4e860c798db620d31
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 0%

---

# Guida dell’interfaccia utente di Audience Composition

>[!NOTE]
>
>Questa guida spiega come creare tipi di pubblico utilizzando Composizione pubblico. Per informazioni su come creare tipi di pubblico tramite le definizioni dei segmenti utilizzando il Generatore di segmenti, consulta la [guida dell&#39;interfaccia utente del Generatore di segmenti](./segment-builder.md).

La funzione Composizione pubblico fornisce un’area di lavoro per creare e modificare i tipi di pubblico, utilizzando blocchi che rappresentano azioni diverse.

![Interfaccia utente per la composizione del pubblico.](../images/ui/audience-composition/audience-composition.png)

Per modificare i dettagli della composizione, inclusi il titolo e la descrizione, selezionare il pulsante ![cursori](/help/images/icons/properties.png).

Viene visualizzato il popover **[!UICONTROL Proprietà composizione]**. È possibile inserire i dettagli della composizione, inclusi il titolo e la descrizione qui.

![Viene visualizzato il popover delle proprietà di composizione.](../images/ui/audience-composition/composition-properties.png)

>[!NOTE]
>
>Se **non** assegna un titolo alla composizione, per impostazione predefinita il titolo sarà &quot;Composizione&quot; seguito dalla data e dall&#39;ora di creazione. Inoltre, ogni composizione **deve** avere un proprio nome univoco.

Dopo aver aggiornato i dettagli della composizione, seleziona **[!UICONTROL Salva]** per confermare questi aggiornamenti. L’area di lavoro per la composizione del pubblico viene nuovamente visualizzata.

L&#39;area di lavoro per la composizione del pubblico è composta da quattro diversi tipi di blocchi: **[[!UICONTROL Pubblico]](#audience-block)**, **[[!UICONTROL Escludi]](#exclude-block)**, **[[!UICONTROL Classifica]](#rank-block)** e **[[!UICONTROL Dividi]](#split-block)**.

## [!UICONTROL Pubblico] {#audience-block}

Il tipo di blocco **[!UICONTROL Pubblico]** ti consente di aggiungere i sottogruppi di pubblico che desideri comporre il nuovo pubblico più grande. Per impostazione predefinita, un blocco **[!UICONTROL Pubblico]** è incluso nella parte superiore dell&#39;area di lavoro della composizione.

Quando selezioni il blocco **[!UICONTROL Pubblico]**, nella barra a destra vengono visualizzati i controlli per etichettare il pubblico, aggiungere tipi di pubblico al blocco e creare regole personalizzate per il blocco di pubblico.

>[!NOTE]
>
>Puoi aggiungere tipi di pubblico **o** per creare una regola personalizzata. Queste due funzionalità **non possono** essere utilizzate insieme.

![Vengono visualizzati i dettagli del blocco del pubblico.](../images/ui/audience-composition/audience-block.png)

### [!UICONTROL Aggiungi pubblico] {#add-audience}

Aggiungere tipi di pubblico al blocco Pubblico. selezionare **[!UICONTROL Aggiungi pubblico]**.

![Il pulsante Aggiungi pubblico è evidenziato.](../images/ui/audience-composition/add-audience.png)

>[!IMPORTANT]
>
>Tieni presente che verranno visualizzati **solo** tipi di pubblico definiti utilizzando il criterio di unione predefinito.
>
>Inoltre, è possibile utilizzare solo i tipi di pubblico **pubblicati** creati con Segment Builder. I tipi di pubblico creati mediante Composizione pubblico e quelli generati esternamente sono **non** disponibili.

Viene visualizzato un elenco di tipi di pubblico. Seleziona i tipi di pubblico da includere, seguito da **[!UICONTROL Aggiungi]** per aggiungerli al blocco di pubblico.

![Viene visualizzato un elenco di tipi di pubblico. È possibile selezionare il pubblico da aggiungere da questa finestra di dialogo.](../images/ui/audience-composition/select-audience.png)

I tipi di pubblico selezionati vengono ora visualizzati nella barra a destra quando è selezionato il blocco **[!UICONTROL Pubblico]**. Da qui, puoi modificare il tipo di unione dei tipi di pubblico combinati.

![I possibili tipi di unione per i tipi di pubblico sono evidenziati.](../images/ui/audience-composition/merge-types.png)

| Tipo di unione | Descrizione |
| ---------- | ----------- |
| [!UICONTROL Union] | I tipi di pubblico vengono combinati in un unico pubblico. Equivale a un&#39;operazione OR. |
| [!UICONTROL Intersection] | I tipi di pubblico vengono combinati e vengono aggiunti solo quelli condivisi in **tutti**. Equivale a un&#39;operazione AND. |
| [!UICONTROL Escludi sovrapposizione] | I tipi di pubblico vengono combinati, con solo quelli condivisi in **uno, ma non tutti**. Equivale a un&#39;operazione XOR. |

### [!UICONTROL Genera regola] {#build-rule}

Per aggiungere una regola personalizzata al blocco Pubblico, seleziona **[!UICONTROL Genera regola]**.

![Il pulsante Genera regola è evidenziato.](../images/ui/audience-composition/build-rule.png)

Viene visualizzato il Generatore di segmenti. Puoi utilizzare il Generatore di segmenti per creare una regola personalizzata che il pubblico dovrà seguire. Ulteriori informazioni sull&#39;utilizzo del Generatore di segmenti sono disponibili nella [guida del Generatore di segmenti](./segment-builder.md).

![Viene visualizzata l&#39;interfaccia utente del Generatore di segmenti.](../images/ui/audience-composition/segment-builder.png)

Dopo aver aggiunto una regola personalizzata, seleziona **[!UICONTROL Salva]** per aggiungere la regola al pubblico.

![](../images/ui/audience-composition/custom-rule.png)

## [!UICONTROL Escludi] {#exclude-block}

Il tipo di blocco **[!UICONTROL Escludi]** ti consente di escludere pubblici secondari o attributi specifici dal tuo nuovo pubblico più grande.

Per aggiungere un blocco **[!UICONTROL Escludi]**, seleziona l&#39;icona **+**, seguita da **[!UICONTROL Escludi]**.

![L&#39;opzione Escludi è selezionata.](../images/ui/audience-composition/add-exclude-block.png)

Il blocco **[!UICONTROL Escludi]** è stato aggiunto. Quando questo blocco è selezionato, i dettagli sull’esclusione vengono visualizzati nella barra a destra. Questo include l’etichetta del blocco e il tipo di esclusione. È possibile escludere [per pubblico](#exclude-audience) o [per attributo](#exclude-attribute).

![Il blocco Exclude, che evidenzia i due diversi tipi di esclusione disponibili.](../images/ui/audience-composition/exclude.png)

### Escludi per pubblico {#exclude-audience}

Se escludi per pubblico, puoi selezionare i tipi di pubblico da escludere selezionando **[!UICONTROL Aggiungi pubblico]**.

![È selezionato il pulsante [!UICONTROL Aggiungi pubblico], che consente di scegliere il pubblico da escludere.](../images/ui/audience-composition/add-excluded-audience.png)

>[!IMPORTANT]
>
>È possibile utilizzare solo i tipi di pubblico **pubblicati** creati con Segment Builder. I tipi di pubblico creati mediante Composizione pubblico e quelli generati esternamente sono **non** disponibili.

Viene visualizzato un elenco di tipi di pubblico. Seleziona **[!UICONTROL Aggiungi]** per aggiungere i tipi di pubblico da escludere al blocco di esclusione.

![Viene visualizzato un elenco di tipi di pubblico. È possibile selezionare il pubblico da aggiungere da questa finestra di dialogo.](../images/ui/audience-composition/select-audience.png)

### Escludi per attributo {#exclude-attribute}

Se escludi per attributo, puoi selezionare gli attributi da escludere selezionando l&#39;icona ![filtro](/help/images/icons/project-edit.png) nella sezione **[!UICONTROL Regola di esclusione]**.

![La sezione degli attributi è evidenziata e mostra dove scegliere l&#39;attributo da escludere.](../images/ui/audience-composition/exclude-attribute.png)

Viene visualizzato un elenco di attributi di profilo. Seleziona il tipo di attributo da escludere, seguito da **[!UICONTROL Seleziona]** per aggiungerlo al blocco di esclusione.

![Viene visualizzato un elenco di attributi.](../images/ui/audience-composition/select-attribute-exclude.png)

>[!IMPORTANT]
>
>Quando si esclude per attributo, è possibile specificare solo **un** valore da escludere. L&#39;utilizzo di qualsiasi tipo di separatore, ad esempio una virgola o un punto e virgola, determina l&#39;esclusione del valore esatto. Se ad esempio si imposta il valore come `red, blue`, il termine `red, blue` verrà escluso dall&#39;attributo, ma **non** comporterà l&#39;esclusione del termine `red` o `blue`.

## [!UICONTROL Arricchisci] {#enrich-block}

>[!IMPORTANT]
>
>Al momento, gli attributi di arricchimento possono **solo** essere utilizzati in scenari Adobe Journey Optimizer a valle.

Il tipo di blocco **[!UICONTROL Arricchisci]** ti consente di arricchire il pubblico con attributi aggiuntivi da un set di dati. Puoi utilizzare questi attributi nei casi di utilizzo di personalizzazione.

Per aggiungere un blocco **[!UICONTROL Arricchisci]**, seleziona l&#39;icona **+**, seguita da **[!UICONTROL Arricchisci]**.

![L&#39;opzione [!UICONTROL Arricchisci] è selezionata.](../images/ui/audience-composition/add-enrich-block.png)

Blocco **[!UICONTROL Arricchisci]** aggiunto. Quando questo blocco è selezionato, i dettagli sull’arricchimento vengono visualizzati nella barra a destra. Questo include l’etichetta del blocco e il set di dati di arricchimento.

Per selezionare il set di dati con cui arricchire il pubblico, seleziona l&#39;icona ![filtro](/help/images/icons/project-edit.png).

![Il pulsante del filtro è evidenziato. Selezionando questa opzione si accede al popover [!UICONTROL Seleziona set di dati].](../images/ui/audience-composition/enrich-select-dataset.png)

Viene visualizzato il popover **[!UICONTROL Seleziona set di dati]**. Seleziona il set di dati da aggiungere per l&#39;arricchimento, seguito da **[!UICONTROL Seleziona]** per aggiungere il set di dati per l&#39;arricchimento.

![Il set di dati scelto è selezionato.](../images/ui/audience-composition/enrich-dataset-selected.png)

>[!IMPORTANT]
>
>Il set di dati selezionato **deve** soddisfare i seguenti criteri:
>
>- Il set di dati **deve** essere di tipo record.
>   - Il set di dati **non può** essere di tipo evento, generato dal sistema o contrassegnato per il profilo.
>- Il set di dati **deve** essere di almeno 1 GB.

La sezione **[!UICONTROL Criteri di arricchimento]** è ora visualizzata nella barra a destra. In questa sezione è possibile selezionare la **[!UICONTROL chiave di join di Source]** e la **[!UICONTROL chiave di join del set di dati di arricchimento]**, che consente di collegare il set di dati di arricchimento al pubblico che si sta tentando di creare.

![L&#39;area [!UICONTROL Criteri di arricchimento] è evidenziata.](../images/ui/audience-composition/enrichment-criteria.png)

Per selezionare la **[!UICONTROL chiave di join di Source]**, selezionare l&#39;icona ![filter](/help/images/icons/project-edit.png).

![L&#39;icona del filtro per la [!UICONTROL chiave di join di Source] è evidenziata.](../images/ui/audience-composition/enrich-select-source-join-key.png)

Viene visualizzato il popover **[!UICONTROL Seleziona un attributo di profilo]**. Seleziona l&#39;attributo di profilo che desideri utilizzare come chiave di join di origine, seguito da **[!UICONTROL Seleziona]** per scegliere tale attributo come chiave di join di origine.

![L&#39;attributo che si desidera utilizzare come chiave di join di origine è evidenziato.](../images/ui/audience-composition/enrich-select-profile-attribute.png)

Per selezionare la chiave di join del set di dati **[!UICONTROL Enrichment]**, selezionare l&#39;icona ![filter](/help/images/icons/project-edit.png).

![L&#39;icona del filtro per la chiave di aggiunta al set di dati di arricchimento  è evidenziata.](../images/ui/audience-composition/enrich-select-enrichment-dataset-join-key.png)

Viene visualizzato il popover **[!UICONTROL Attributi di arricchimento]**. Seleziona l&#39;attributo da utilizzare come chiave di join del set di dati di arricchimento, seguito da **[!UICONTROL Seleziona]** per scegliere tale attributo come chiave di join del set di dati di arricchimento.

![L&#39;attributo che si desidera utilizzare come chiave di join del set di dati di arricchimento è evidenziato.](../images/ui/audience-composition/enrich-select-enrichment-dataset-attribute.png)

Dopo aver aggiunto entrambe le chiavi di join, viene visualizzata la sezione **[!UICONTROL Attributi di arricchimento]**. Ora puoi aggiungere l’attributo con cui desideri migliorare il pubblico. Per aggiungere questi attributi, selezionare **[!UICONTROL Aggiungi attributo]**.

![Il pulsante [!UICONTROL Aggiungi attributo] è evidenziato.](../images/ui/audience-composition/enrich-select-add-attribute.png)

Viene visualizzato il popover **[!UICONTROL Attributi di arricchimento]**. Puoi selezionare gli attributi dal set di dati con cui arricchire il pubblico, seguito da **[!UICONTROL Seleziona]** per aggiungere gli attributi al pubblico.

![Gli attributi di arricchimento che desideri aggiungere sono evidenziati.](../images/ui/audience-composition/enrich-add-enrichment-attributes.png)

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

Il tipo di blocco **[!UICONTROL Classifica]** consente di classificare e ordinare i profili in base a un attributo specificato e di includerli nella composizione.

Per aggiungere un blocco **[!UICONTROL Classifica]**, seleziona l&#39;icona **+**, seguita da **[!UICONTROL Classifica]**.

![L&#39;opzione di classificazione è selezionata.](../images/ui/audience-composition/add-rank-block.png)

Quando selezioni il blocco, i dettagli sulla classificazione vengono visualizzati nella barra a destra, tra cui l’etichetta del blocco, l’attributo in base al quale eseguire la classificazione, l’ordine di classificazione e un interruttore per limitare il numero di profili da classificare.

![Il blocco di classificazione è evidenziato, così come i dettagli del blocco di classificazione.](../images/ui/audience-composition/rank.png)

Per selezionare l&#39;attributo in base al quale classificare i tipi di pubblico, seleziona l&#39;icona ![filtro](/help/images/icons/project-edit.png).

![L&#39;icona del filtro è evidenziata e mostra cosa selezionare per accedere alla schermata di selezione degli attributi del profilo.](../images/ui/audience-composition/select-rank-attribute.png)

Viene visualizzato un elenco di attributi di profilo. In questo popover, puoi selezionare il tipo di attributo in base al quale classificare il pubblico. Seleziona **[!UICONTROL Seleziona]** per aggiungerlo al tuo blocco di classificazione. Tieni presente che l&#39;attributo selezionato può essere **solo** numeri.

![Viene visualizzato un elenco di attributi.](../images/ui/audience-composition/select-attribute-rank.png)

Dopo aver selezionato l’attributo, puoi selezionare l’ordine in base al quale classificarlo. In ordine crescente (dal più basso al più alto) o decrescente (dal più alto al più basso).

Inoltre, puoi limitare il numero di profili restituiti abilitando l&#39;interruttore **[!UICONTROL Aggiungi limite profilo]**. Quando questa opzione è abilitata, puoi impostare il numero massimo di profili restituiti all&#39;interno del campo **[!UICONTROL Profili inclusi]**.

![L&#39;opzione Aggiungi limite profilo è evidenziata e consente di limitare il numero di profili restituiti.](../images/ui/audience-composition/add-profile-limit.png)

## [!UICONTROL Divisione] {#split-block}

Il tipo di blocco **[!UICONTROL Dividi]** ti consente di suddividere il nuovo pubblico in vari sottogruppi. Puoi suddividere questo pubblico in base alla percentuale o a un attributo. Durante la suddivisione del pubblico in sottotargeting, la suddivisione è **non** persistente. Ciò significa che i profili possono trovarsi in diversi sottotipi di pubblico per ogni valutazione.

Per aggiungere un blocco **[!UICONTROL Split]**, seleziona l&#39;icona **+**, seguita da **[!UICONTROL Split]**.

![L&#39;opzione Dividi è selezionata.](../images/ui/audience-composition/add-split-block.png)

Quando dividi il pubblico, puoi dividerlo per percentuale o per attributo.

### Dividi per percentuale {#split-percentage}

Quando si suddivide in percentuale, il pubblico viene suddiviso in modo casuale, in base al numero di percorsi e alle percentuali fornite.

Ad esempio, puoi avere tre percorsi, ciascuno con una percentuale diversa di profili.

![Viene visualizzata la suddivisione in numero di tipi di pubblico e percentuali salvati.](../images/ui/audience-composition/percentages.png)

### Dividi per attributo {#split-attribute}

Quando si divide per attributo, il pubblico viene diviso in base agli attributi forniti. Per selezionare l&#39;attributo da dividere, selezionare il blocco **[!UICONTROL Dividi]**, seguito dall&#39;icona ![filtro](/help/images/icons/project-edit.png).

![Il pulsante di filtro è selezionato e mostra come filtrare per attributo.](../images/ui/audience-composition/select-split-attribute.png)

Viene visualizzato un elenco di attributi di profilo. Seleziona il tipo di attributo, seguito da **[!UICONTROL Seleziona]** per aggiungerlo al blocco di suddivisione.

![Viene visualizzato un elenco di attributi.](../images/ui/audience-composition/select-attribute-exclude.png)

Dopo aver selezionato l&#39;attributo, puoi scegliere quali profili apparterranno a quale pubblico secondario aggiungendo i valori all&#39;interno del campo **[!UICONTROL Valori]**.

![Vengono aggiunti i valori per i quali si desidera dividere gli attributi.](../images/ui/audience-composition/attribute-split-values.png)

Inoltre, puoi abilitare l&#39;interruttore **[!UICONTROL Altri profili]** per creare un pubblico secondario composto da tutti i profili non selezionati.

![L&#39;opzione Altri profili è evidenziata.](../images/ui/audience-composition/split-other-profiles.png)

## Pubblicazione del pubblico

>[!IMPORTANT]
>
>Quando pubblichi la composizione del pubblico, tieni presente che potrebbero essere necessarie fino a 48 ore per valutarla e attivarla per l’utilizzo in servizi a valle come una destinazione Real-Time CDP o un canale Adobe Journey Optimizer.

Dopo aver creato la composizione, puoi salvarla e pubblicarla selezionando **[!UICONTROL Publish]**.

![Il pulsante Publish è evidenziato e mostra come salvare e pubblicare la composizione.](../images/ui/audience-composition/publish.png)

In caso di errori nella creazione del pubblico, viene visualizzato un avviso che informa su come risolvere il problema.

![Il pulsante Publish è evidenziato e mostra come salvare e pubblicare la composizione.](../images/ui/audience-composition/audience-alert.png)

## Passaggi successivi

La funzione Composizione pubblico offre un flusso di lavoro avanzato che consente di creare composizioni da diversi tipi di blocchi. Per ulteriori informazioni su altre parti dell&#39;interfaccia utente di Segmentation Service, consulta la [Guida utente di Segmentation Service](./overview.md).
