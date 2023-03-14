---
keywords: Experience Platform;home;argomenti popolari;servizio di segmentazione;segmentazione;servizio di segmentazione;guida utente;guida interfaccia utente;guida interfaccia utente tipi di pubblico;audience;audience;audiences;guida interfaccia utente;
solution: Experience Platform
title: Guida all’interfaccia utente di Audiences
description: Audience Builder nell’interfaccia utente di Adobe Experience Platform offre un’area di lavoro ricca che consente di interagire con gli elementi dati del profilo. L’area di lavoro fornisce controlli intuitivi per la creazione e la modifica dei tipi di pubblico per la tua organizzazione.
hide: true
hidefromtoc: true
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 1%

---

# Guida dell’interfaccia utente di Audience Builder

>[!IMPORTANT]
>
>Audience Builder è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Il Generatore di tipi di pubblico fornisce un’area di lavoro per creare e modificare i tipi di pubblico, utilizzando blocchi che vengono utilizzati per rappresentare azioni diverse.

![L’interfaccia utente di Audience Builder.](../images/ui/audience-builder/audience-builder.png)

L’area di lavoro per la composizione del pubblico è composta da cinque diversi tipi di blocchi: **[[!UICONTROL Pubblico]](#audience-block)**, **[[!UICONTROL Escludi]](#exclude-block)**, **[[!UICONTROL Iscriviti]](#join-block)**, **[[!UICONTROL Classifica]](#rank-block)**, e **[[!UICONTROL Dividi]](#split-block)**.

## [!UICONTROL Destinatari] {#audience-block}

Il **[!UICONTROL Pubblico]** il tipo di blocco ti consente di aggiungere i sottogruppi di pubblico che desideri comporre il nuovo pubblico più grande. Per impostazione predefinita, un **[!UICONTROL Pubblico]** Il blocco è incluso nella parte superiore dell’area di lavoro della composizione.

Quando selezioni il **[!UICONTROL Pubblico]** , nella barra a destra vengono visualizzati i controlli per l’etichettatura e l’aggiunta di tipi di pubblico al blocco.

![Vengono visualizzati i dettagli del blocco Audience.](../images/ui/audience-builder/select-audience.png)

Dopo aver selezionato **[!UICONTROL Aggiungi pubblico]**, viene visualizzato un elenco di tipi di pubblico. Seleziona i tipi di pubblico da includere, seguito da **[!UICONTROL Aggiungi]** per aggiungerli al blocco di pubblico.

![Viene visualizzato un elenco di tipi di pubblico. Da questa finestra di dialogo puoi selezionare il pubblico da aggiungere.](../images/ui/audience-builder/select-audience.png)

I tipi di pubblico selezionati vengono ora visualizzati nella barra a destra quando **[!UICONTROL Pubblico]** è selezionato. Da qui, puoi modificare il tipo di unione dei tipi di pubblico combinati.

![Vengono evidenziati i possibili tipi di unione per i tipi di pubblico.](../images/ui/audience-builder/merge-types.png)

| Tipo di unione | Descrizione |
| ---------- | ----------- |
| [!UICONTROL Unione] | I tipi di pubblico vengono combinati in un unico pubblico. Equivale a un&#39;operazione OR. |
| [!UICONTROL Intersection] | I tipi di pubblico vengono combinati, con solo quelli condivisi in **tutto** di quelli che vengono aggiunti. Equivale a un&#39;operazione AND. |
| [!UICONTROL Escludi sovrapposizione] | I tipi di pubblico vengono combinati, con solo quelli condivisi in **uno, ma non tutti** di quelli che vengono aggiunti. Equivale a un&#39;operazione XOR. |

## [!UICONTROL Escludi] {#exclude-block}

Il **[!UICONTROL Escludi]** il tipo di blocco ti consente di escludere pubblici secondari o attributi specifici dal nuovo pubblico più ampio.

Per aggiungere una **[!UICONTROL Escludi]** blocco, seleziona il **+** , seguito da **[!UICONTROL Escludi]**.

![L&#39;opzione Escludi (Exclude) è selezionata.](../images/ui/audience-builder/add-exclude-block.png)

Il **[!UICONTROL Escludi]** viene aggiunto il blocco. Quando questo blocco è selezionato, i dettagli sull’esclusione vengono visualizzati nella barra a destra. Questo include l’etichetta del blocco e il tipo di esclusione. Puoi escludere [per pubblico](#exclude-audience) o [per attributo](#exclude-attribute).

![Il blocco Escludi, che evidenzia i due diversi tipi di esclusione disponibili.](../images/ui/audience-builder/exclude.png)

### Escludi per pubblico {#exclude-audience}

Se escludi per pubblico, puoi selezionare i tipi di pubblico da escludere selezionando **[!UICONTROL Aggiungi pubblico]**.

![Viene selezionato il pulsante Aggiungi pubblico, che consente di scegliere quale pubblico escludere.](../images/ui/audience-builder/add-excluded-audience.png)

Viene visualizzato un elenco di tipi di pubblico. Seleziona **[!UICONTROL Aggiungi]** per aggiungere i tipi di pubblico da escludere al blocco di esclusione.

![Viene visualizzato un elenco di tipi di pubblico. Da questa finestra di dialogo puoi selezionare il pubblico da aggiungere.](../images/ui/audience-builder/select-audience.png)

### Escludi per attributo {#exclude-attribute}

Se si esclude per attributo, è possibile selezionare gli attributi da escludere selezionando l&#39;opzione ![filter](../images/ui/audience-builder/filter-attribute.png) all&#39;interno del **[!UICONTROL Regola di esclusione]** sezione.

![Viene evidenziata la sezione degli attributi, che mostra dove selezionare l’attributo da escludere.](../images/ui/audience-builder/exclude-attribute.png)

Viene visualizzato un elenco di attributi di profilo. Seleziona il tipo di attributo da escludere, seguito da **[!UICONTROL Seleziona]** per aggiungerli al blocco di esclusione.

![Viene visualizzato un elenco di attributi.](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL Iscriversi] {#join-block}

Il **[!UICONTROL Iscriviti]** tipo di blocco consente di aggiungere tipi di pubblico esterni da set di dati non ancora elaborati da Adobe Experience Platform.

Per aggiungere una **[!UICONTROL Iscriviti]** blocco, seleziona il **+** , seguito da **[!UICONTROL Iscriviti]**.

![L’opzione Unisci è selezionata.](../images/ui/audience-builder/add-join-block.png)

Quando selezioni il blocco, i dettagli sul join vengono visualizzati nella barra a destra, inclusa l’etichetta del blocco e l’opzione per aggiungere tipi di pubblico al set di dati di arricchimento.

![Il blocco di join viene evidenziato, inclusi i dettagli sul blocco di join.](../images/ui/audience-builder/join.png)

Dopo aver selezionato **[!UICONTROL Aggiungi pubblico]**, viene visualizzato un elenco di tipi di pubblico. Seleziona i tipi di pubblico da includere, seguito da **[!UICONTROL Aggiungi]** per aggiungerli al blocco di join.

![Viene visualizzato un elenco di tipi di pubblico. Da questa finestra di dialogo puoi selezionare il pubblico da aggiungere.](../images/ui/audience-builder/select-audience.png)

I tipi di pubblico selezionati vengono ora visualizzati nella barra a destra quando **[!UICONTROL Iscriviti]** è selezionato.

![Vengono visualizzati i tipi di pubblico aggiunti come parte dell’unione.](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL Classifica] {#rank-block}

Il **[!UICONTROL Classifica]** il tipo di blocco ti consente di classificare e ordinare i tipi di pubblico prima che venga pubblicato il nuovo pubblico.

Per aggiungere una **[!UICONTROL Classifica]** blocco, seleziona il **+** , seguito da **[!UICONTROL Classifica]**.

![L’opzione Classifica è selezionata.](../images/ui/audience-builder/add-rank-block.png)

Quando selezioni il blocco, i dettagli sulla classificazione vengono visualizzati nella barra a destra, tra cui l’etichetta del blocco, l’attributo in base al quale eseguire la classificazione, l’ordine di classificazione e un interruttore per limitare il numero di profili da classificare.

![Il blocco di classificazione viene evidenziato, così come i dettagli del blocco di classificazione.](../images/ui/audience-builder/rank.png)

Per selezionare l’attributo in base al quale classificare i tipi di pubblico, seleziona la ![filter](../images/ui/audience-builder/filter-attribute.png) icona.

![L’icona del filtro è evidenziata e mostra cosa selezionare per accedere alla schermata di selezione degli attributi del profilo.](../images/ui/audience-builder/select-rank-attribute.png)

Viene visualizzato un elenco di attributi di profilo. In questo popover, puoi selezionare il tipo di attributo in base al quale classificare il pubblico. Seleziona **[!UICONTROL Seleziona]** per aggiungerlo al blocco di classificazione. L&#39;attributo selezionato può **solo** essere di tipo `int`.

![Viene visualizzato un elenco di attributi.](../images/ui/audience-builder/select-attribute.png)

Dopo aver selezionato l’attributo, puoi selezionare l’ordine in base al quale classificarlo. In ordine crescente (dal più basso al più alto) o decrescente (dal più alto al più basso).

Inoltre, puoi limitare il numero di tipi di pubblico restituiti abilitando la funzione **[!UICONTROL Aggiungi limite profilo]** attivare/disattivare. Quando questa opzione è abilitata, puoi impostare il numero massimo di tipi di pubblico restituiti all’interno del **[!UICONTROL Profili inclusi]** campo.

![Viene evidenziata l’opzione Aggiungi limite profilo, che consente di limitare il numero di tipi di pubblico restituiti.](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL Dividere] {#split-block}

Il **[!UICONTROL Dividi]** il tipo di blocco ti consente di suddividere il nuovo pubblico in vari tipi di pubblico secondario. Puoi suddividere questo pubblico in base alla percentuale o a un attributo.

Per aggiungere una **[!UICONTROL Dividi]** blocco, seleziona il **+** , seguito da **[!UICONTROL Dividi]**.

![L&#39;opzione Dividi (Split) è selezionata.](../images/ui/audience-builder/add-split-block.png)

### Dividi per percentuale {#split-percentage}

Quando si suddivide in percentuale, il pubblico viene suddiviso in modo casuale, in base al numero di percorsi e alle percentuali fornite.

Ad esempio, puoi avere tre percorsi, ciascuno con una percentuale diversa di profili.

![Viene visualizzata la suddivisione in numero di tipi di pubblico e percentuali salvati.](../images/ui/audience-builder/percentages.png)

Inoltre, puoi contrassegnare uno dei tipi di pubblico suddivisi come gruppo di controllo.

![Attivazione/disattivazione del gruppo di controllo. Questo consente di contrassegnare uno dei tipi di pubblico suddivisi come gruppo di controllo.](../images/ui/audience-builder/control-group.png)

### Dividi per attributo {#split-attribute}

Quando si divide per attributo, il pubblico viene diviso in base agli attributi forniti. Per selezionare l&#39;attributo da dividere, selezionare **[!UICONTROL Dividi]** blocco, seguito da ![filter](../images/ui/audience-builder/filter-attribute.png) icona.

![Viene selezionato il pulsante di filtro, che mostra come filtrare per attributo.](../images/ui/audience-builder/select-attribute-split.png)

Viene visualizzato un elenco di attributi di profilo. Seleziona il tipo di attributo, seguito da **[!UICONTROL Seleziona]** per aggiungerlo al blocco diviso.

![Viene visualizzato un elenco di attributi.](../images/ui/audience-builder/select-attribute.png)

Dopo aver selezionato l’attributo, puoi scegliere quali profili apparterranno a quale pubblico secondario aggiungendo i valori all’interno del **[!UICONTROL Valori]** campo.

![Vengono aggiunti i valori per i quali si desidera dividere gli attributi.](../images/ui/audience-builder/attribute-split-values.png)

Inoltre, è possibile abilitare **[!UICONTROL Altri profili]** attiva per creare un pubblico secondario composto da tutti i profili non selezionati.

![Viene evidenziata l’opzione Altri profili.](../images/ui/audience-builder/attribute-split-other-profiles.png)

## Pubblicazione del pubblico

Dopo aver composto il pubblico, puoi salvarlo e pubblicarlo selezionando **[!UICONTROL Pubblica]**.

![Viene evidenziato il pulsante Pubblica, che mostra come salvare e pubblicare il pubblico.](../images/ui/audience-builder/publish-audience.png)

In caso di errori nella creazione del pubblico, viene visualizzato un avviso che informa su come risolvere il problema.

![Viene evidenziato il pulsante Pubblica, che mostra come salvare e pubblicare il pubblico.](../images/ui/audience-builder/audience-alert.png)

## Passaggi successivi

Audience Builder offre un flusso di lavoro avanzato che consente di creare tipi di pubblico da diversi tipi di blocchi. Per ulteriori informazioni su altre parti dell’interfaccia utente del servizio di segmentazione, consulta [Guida utente al servizio di segmentazione](./overview.md).
