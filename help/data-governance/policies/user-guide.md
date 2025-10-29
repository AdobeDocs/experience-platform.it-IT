---
keywords: Experience Platform;home;argomenti popolari;governance dei dati;guida utente sui criteri di utilizzo dei dati
solution: Experience Platform
title: Gestire i criteri di utilizzo dei dati nell’interfaccia utente
description: La governance dei dati di Adobe Experience Platform fornisce un’interfaccia utente che consente di creare e gestire i criteri di utilizzo dei dati. Questo documento fornisce una panoramica delle azioni che possono essere eseguite nell’area di lavoro Criteri nell’interfaccia utente di Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: 364a92bde1a1629d2811e7ff16bd6a4fb5287249
workflow-type: tm+mt
source-wordcount: '2380'
ht-degree: 11%

---

# Gestire i criteri di utilizzo dei dati nell’interfaccia utente {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_description"
>title="Integrare e applicare il consenso dei clienti nei dati di profilo"
>abstract="<h2>Descrizione</h2><p>Con Experience Platform è possibile integrare i dati di consenso raccolti dalla clientela nei rispettivi profili. Puoi quindi impostare i criteri di consenso per determinare se tali dati possono essere inclusi nei segmenti attivati per determinate destinazioni.</p>"

Questo documento illustra come utilizzare l&#39;area di lavoro **[!UICONTROL Policies]** nell&#39;interfaccia utente di Adobe Experience Platform per creare e gestire i criteri di utilizzo dei dati.

>[!NOTE]
>
>Per informazioni su come gestire i criteri di controllo di accesso nell&#39;interfaccia utente, fare riferimento alla [guida dell&#39;interfaccia utente di controllo di accesso basata su attributi](../../access-control/abac/ui/policies.md).

>[!IMPORTANT]
>
>Tutti i criteri di utilizzo dei dati (inclusi i criteri core forniti da Adobe) sono disabilitati per impostazione predefinita. Affinché un singolo criterio possa essere preso in considerazione per l’applicazione, è necessario abilitarlo manualmente. Consulta la sezione su [abilitazione dei criteri](#enable) per i passaggi su come eseguire questa operazione nell&#39;interfaccia utente.

## Prerequisiti

Questa guida richiede una buona conoscenza dei seguenti concetti di [!DNL Experience Platform]:

* [Governance dei dati](../home.md)
* [Criteri di utilizzo dei dati](./overview.md)

## Visualizza criteri esistenti {#view-policies}

Nell&#39;interfaccia utente [!DNL Experience Platform], selezionare **[!UICONTROL Policies]** per aprire l&#39;area di lavoro **[!UICONTROL Policies]**. Nella scheda **[!UICONTROL Browse]** è disponibile un elenco dei criteri disponibili, incluse le etichette, le azioni di marketing e lo stato associati.

![](../images/policies/browse-policies.png)

Se hai accesso ai criteri di consenso, seleziona l&#39;opzione **[!UICONTROL Consent policies]** per visualizzarli nella scheda [!UICONTROL Browse].

![](../images/policies/consent-policy-toggle.png)

Selezionare un criterio elencato per visualizzarne la descrizione e il tipo. Se è selezionato un criterio personalizzato, vengono visualizzati controlli aggiuntivi per modificare, eliminare o [abilitare/disabilitare il criterio](#enable).

![](../images/policies/policy-details.png)

## Creare un criterio personalizzato {#create-policy}

Per creare un nuovo criterio di utilizzo dati personalizzato, selezionare **[!UICONTROL Create policy]** nell&#39;angolo superiore destro della scheda **[!UICONTROL Browse]** nell&#39;area di lavoro **[!UICONTROL Policies]**.

![](../images/policies/create-policy-button.png)

Viene visualizzata la finestra di dialogo [!UICONTROL Choose type of policy]. Seleziona un [criterio di consenso](#consent-policy) o un [criterio di governance dei dati](#create-governance-policy).

![Finestra di dialogo Scegli il tipo di criterio.](../images/policies/choose-policy-type.png)

### Utilizzare insieme la governance dei dati e i criteri di consenso {#combine-policies}

>[!NOTE]
>
>I criteri di consenso sono attualmente disponibili solo per le organizzazioni che hanno acquistato Adobe Healthcare Shield o Adobe Privacy &amp; Security Shield.

I criteri di governance e di consenso possono essere utilizzati insieme per creare regole solide per la gestione dei tipi di pubblico mappati su una destinazione. I criteri di consenso sono di natura inclusiva, il che significa che determinano quali profili possono essere inclusi in ogni esperienza di marketing. Al contrario, i criteri di governance escludono l’utilizzo di attributi con etichetta specifici dalla configurazione per l’attivazione.

Utilizzando questo comportamento, puoi impostare una combinazione di criteri e regole di consenso che includono i profili corretti, ma impedisce di includere dati in contrasto con le regole organizzative impostate. Uno scenario esemplificativo potrebbe essere quello di escludere i dati sensibili dall’inclusione, ma comunque in grado di eseguire il targeting degli utenti autorizzati per il marketing tramite social media. I passaggi necessari per questo scenario sono descritti nell’infografica seguente.

![Un&#39;infografica che illustra i passaggi necessari per utilizzare insieme i criteri di governance e di consenso al fine di creare solide regole per i tipi di pubblico che gestiscono.](../images/policies/governance-and-consent-policies-infographic.png)

### Creare criteri di governance dei dati {#create-governance-policy}

Verrà visualizzato il flusso di lavoro **[!UICONTROL Create policy]**. Per iniziare, specifica un nome e una descrizione per il nuovo criterio.

![](../images/policies/create-policy-description.png)

Quindi, seleziona le etichette di utilizzo dei dati su cui basare il criterio. Quando selezioni più etichette, puoi scegliere se i dati devono contenere tutte le etichette o solo una di esse affinché il criterio venga applicato. Al termine, fai clic su **[!UICONTROL Next]**.

![](../images/policies/add-labels.png)

Viene visualizzato il passaggio **[!UICONTROL Select marketing actions]**. Scegliere le azioni di marketing appropriate dall&#39;elenco fornito, quindi selezionare **[!UICONTROL Next]** per continuare.

>[!NOTE]
>
>Quando si selezionano più azioni di marketing, il criterio le interpreta come una regola &quot;OR&quot;. In altre parole, il criterio si applica se vengono eseguite **qualsiasi** delle azioni di marketing selezionate.

![](../images/policies/add-marketing-actions.png)

Viene visualizzato il passaggio **[!UICONTROL Review]**, che consente di rivedere i dettagli del nuovo criterio prima di crearlo. Una volta che sei soddisfatto, seleziona **[!UICONTROL Finish]** per creare il criterio.

![](../images/policies/policy-review.png)

Viene visualizzata di nuovo la scheda **[!UICONTROL Browse]**, in cui ora i criteri appena creati sono elencati nello stato &quot;Bozza&quot;. Per abilitare il criterio, vedere la sezione successiva.

![](../images/policies/created-policy.png)

### Creare un criterio di consenso {#consent-policy}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_instructions"
>title="Istruzioni"
>abstract="<ul><li>Assicurati di acquisire i dati delle preferenze negli schemi di unione tramite il connettore di origine OneTrust o lo schema XDM standard per il consenso.</li><li>Seleziona <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=it">Criteri</a> nella barra di navigazione a sinistra, quindi seleziona <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=it#create-governance-policy">Crea criterio</a>.</li><li>Nella sezione <b>Se</b>, descrivi le condizioni o le azioni che attiveranno il controllo dei criteri.</li><li>Nella sezione <b>Allora</b>, inserisci gli attributi di consenso che devono essere presenti affinché un profilo sia incluso nell’azione che ha attivato il criterio.</li><li>Seleziona <b>Salva</b> per creare il criterio. Per abilitare il criterio, seleziona il pulsante di attivazione <b>Stato</b> nella barra a destra.</li><li>Experience Platform applica automaticamente i criteri di consenso abilitati quando attivi i segmenti sulle destinazioni e fornisce dettagli su come ogni criterio influisce sulle dimensioni del pubblico.</li><li>Per ulteriori informazioni su questa funzione, consulta la guida su come <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=it#consent-policy">creare i criteri di consenso</a>, in Experience League.</li></ul>"

>[!IMPORTANT]
>
>I criteri di consenso sono disponibili solo per le organizzazioni che hanno acquistato **Adobe Healthcare Shield** o **Adobe Privacy &amp; Security Shield**.

Se hai scelto di creare un criterio di consenso, viene visualizzata una nuova schermata che ti consente di configurare il nuovo criterio.

![](../images/policies/consent-policy-dialog.png)

Per utilizzare i criteri di consenso, devi disporre di attributi di consenso presenti nei dati del profilo. Consulta la guida sull&#39;elaborazione del [consenso in Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md) per i passaggi dettagliati su come includere gli attributi richiesti nello schema di unione.

I criteri di consenso sono composti da due componenti logici:

* **[!UICONTROL If]**: la condizione che attiverà il controllo dei criteri. Ciò può essere basato sull’esecuzione di una determinata azione di marketing, sulla presenza di determinate etichette di utilizzo dei dati o su una combinazione delle due.
* **[!UICONTROL Then]**: gli attributi di consenso che devono essere presenti affinché un profilo sia incluso nell&#39;azione che ha attivato il criterio.

>[!NOTE]
>
>I criteri di consenso supportano la creazione di regole avanzate con vari tipi di campi e operatori. Per un riferimento completo ai tipi di campo, agli operatori e agli esempi di creazione di regole supportati, vedere [Riferimento alle regole dei criteri di consenso](./consent-policy-rule-building-reference.md).

#### Configurare le condizioni {#consent-conditions}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentif"
>title="Condizione “Se”"
>abstract="Inizia definendo le condizioni che attiveranno il controllo dei criteri. Le condizioni possono includere l’esecuzione di determinate azioni di marketing, la presenza di determinate etichette di governance dei dati o una combinazione di entrambe. Utilizza la logica AND/OR per creare relazioni condizionali complesse tra più condizioni."

Nella sezione **[!UICONTROL If]**, seleziona le azioni di marketing e/o le etichette di utilizzo dei dati che devono attivare questo criterio. Selezionare **[!UICONTROL View all]** e **[!UICONTROL Select labels]** per visualizzare l&#39;elenco completo delle azioni di marketing e delle etichette disponibili, rispettivamente.

Dopo aver aggiunto almeno una condizione, è possibile selezionare **[!UICONTROL Add condition]** per continuare ad aggiungere altre condizioni in base alle esigenze, scegliendo il tipo di condizione appropriato dal menu a discesa.

![](../images/policies/add-condition.png)

Se selezioni più di una condizione, puoi utilizzare l’icona che appare tra di esse per cambiare la relazione condizionale tra &quot;AND&quot; e &quot;OR&quot;.

![](../images/policies/and-or-selection.png)

#### Selezionare attributi di consenso {#consent-attributes}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentthen"
>title="Condizione “Allora”"
>abstract="Una volta definita la condizione “Se”, utilizza la sezione “Allora” per selezionare almeno un attributo di consenso dallo schema di unione. È necessario spostarsi tra i campi contenitore (Oggetto, Mappa, Array) per raggiungere i campi primitivi (Stringa, Numero, Booleano ecc.) per la creazione di regole. Questo campo primitivo è l’attributo che deve essere presente affinché i profili possano essere inclusi nell’azione disciplinata da questo criterio."

Nella sezione **[!UICONTROL Then]**, seleziona almeno un attributo di consenso dallo schema di unione. Questo è l’attributo che deve essere presente affinché i profili possano essere inclusi nell’azione disciplinata da questo criterio. Puoi scegliere una delle opzioni suggerite oppure selezionare **[!UICONTROL View all]** per scegliere l&#39;attributo direttamente dallo schema di unione.

>[!NOTE]
>
>I criteri di consenso supportano tipi di campi primitivi (stringa, numero, booleano, data) e tipi di contenitori (oggetto, mappa, array). Puoi passare ai contenitori per selezionare attributi specifici e applicare la logica AND/OR per combinare le regole. Per un riferimento completo ai tipi di campo, agli operatori e agli esempi di creazione di regole supportati, vedi il [riferimento per la creazione di regole dei criteri di consenso](./consent-policy-rule-building-reference.md).

![L&#39;interfaccia utente del generatore di criteri di consenso mostra le sezioni If e Then, con Visualizza tutto evidenziato.](../images/policies/view-all.png)

Se si seleziona **[!UICONTROL View all]**, viene visualizzata la finestra di dialogo **[!UICONTROL Select consent attribute]**. Seleziona gli attributi di consenso da verificare per questo criterio. In alternativa, in questa finestra di dialogo è possibile selezionare **[!UICONTROL Advanced Schema search]** per scegliere un campo primitivo nidificato da valutare come parte del criterio. Seleziona **[!UICONTROL Done]** per confermare le impostazioni.

![La finestra di dialogo Seleziona attributo di consenso con un attributo è stata evidenziata ed è stata completata.](../images/policies/select-consent-attribute.png)

### Ricerca avanzata dello schema {#advanced-schema-search}

Nella finestra di dialogo **[!UICONTROL Select consent attribute]**, seleziona **[!UICONTROL Advanced Schema search]** per aprire la finestra di dialogo **[!UICONTROL Select union schema field]**. Da questa vista, selezionare attributi a livello di radice o attributi nidificati di tipi di campi primitivi come stringa, numero, booleano e data, nonché tipi di contenitori come oggetto, mappa e matrice.

![Percorso di clic per spostarsi nella ricerca avanzata dello schema.](../images/policies/consent-advanced-schema-search.gif)

#### Campi a valore fisso per una condizione criterio {#fixed-value-fields}

Quando selezioni un campo a valore fisso come condizione dei criteri, nel pannello [!UICONTROL Selected attributes] vengono visualizzati i valori predefiniti definiti nello schema di dati.

>[!NOTE]
>
>Se un campo è configurato con un set fisso di valori (ad esempio, come enum o altro vocabolario controllato), il generatore di criteri applica tale vincolo per garantire che le condizioni vengano valutate solo in base a dati validi e standardizzati.

Per mantenere la qualità e la coerenza dei dati, l’interfaccia utente riproduce questi valori come caselle di controllo selezionabili anziché come campi di testo libero. Questo approccio riduce la convalida manuale e aiuta i criteri di consenso a valutare i dati in modo affidabile.

Per definire la condizione, selezionare le caselle di controllo relative ai valori che si desidera vengano valutati dal criterio.

![Finestra di dialogo &#39;Seleziona campo schema di unione&#39; con un campo del diagramma schema e le caselle di controllo disponibili a valore fisso evidenziate.](../images/policies/select-schema-field.png)

#### Mappare i campi del tipo di dati per una condizione di criterio {#map-data-type-fields}

Quando selezioni un campo primitivo contenuto in un tipo di dati Mappa, nel pannello **[!UICONTROL Selected attributes]** vengono visualizzate opzioni di configurazione aggiuntive. Utilizza queste opzioni per configurare i controlli del consenso tra più chiavi senza la necessità di un criterio separato per ciascuna chiave. Questo metodo di configurazione semplifica la gestione dei criteri riducendo il numero di criteri da creare.

![La sezione relativa alla mappatura dei criteri di consenso è evidenziata nel pannello degli attributi.](../images/policies/consent-policies-map.png)

##### Configurare gli attributi del tipo di dati mappa {#configure-map-attributes}

Per configurare un attributo di tipo mappa, effettua le seguenti operazioni:

Nel diagramma schema di unione selezionare un campo primitivo, ad esempio una stringa o un numero, contenuto in un tipo di dati Mappa. Il pannello **[!UICONTROL Selected attributes]** viene aggiornato per visualizzare ulteriori opzioni di configurazione per tale campo.

![Sono state aggiornate le opzioni di attributo per un campo primitivo contenuto in un tipo di dati Mappa.](../images/policies/select-union-schema-field.png)

Nel pannello **[!UICONTROL Selected attributes]** configurare il modo in cui i criteri valutano i tasti mappa selezionando o deselezionando la casella di controllo **[!UICONTROL Find any matching item]**.

| Opzione | Azione | Comportamento dei criteri |
| --- | --- | --- |
| La casella di controllo **[!UICONTROL Find any matching item]** è **selezionata** | Il campo di testo **[!UICONTROL within]** è disabilitato. | Il criterio controlla **ogni chiave** all&#39;interno della mappa. Qualsiasi chiave in cui il campo nidificato soddisfa la condizione del valore viene considerata una corrispondenza per il criterio. Ciò è utile per applicare la conformità globale tra gli attributi con chiave dinamica. |
| La casella di controllo **[!UICONTROL Find any matching item]** è **deselezionata** | Immettere un nome chiave specifico nel campo di testo **[!UICONTROL within]**. | Il criterio controlla solo la chiave di mappa specificata nel campo **[!UICONTROL within]**. Vengono associati solo i profili in cui il campo nidificato per una chiave specifica soddisfa il valore definito. Questo è utile per i criteri che si riferiscono a un programma specifico o a una chiave di frequenza (ad esempio, `frequencyMap.m1`). |

Immettere il valore per il campo primitivo selezionato che il criterio deve valutare. Ad esempio, se il tipo di campo è `Integer`, immettere un valore numerico.

![Barra laterale attributi selezionati con le opzioni di configurazione della mappa evidenziate.](../images/policies/within-option.png)

Seleziona **[!UICONTROL Select]** per confermare la configurazione e tornare al generatore di criteri.

Dopo aver selezionato almeno un attributo di consenso, il pannello **[!UICONTROL Policy properties]** viene aggiornato per mostrare il numero stimato di profili inclusi in questo criterio, insieme alla percentuale di profili interessati nell&#39;archivio profili. Il conteggio stimato dei profili viene aggiornato automaticamente quando si modifica la configurazione dei criteri.

![L&#39;interfaccia utente del generatore di criteri mostra una condizione Then configurata con la barra a destra delle proprietà dei criteri che mostra il conteggio dei profili qualificati stimati.](../images/policies/audience-preview.png)

Per aggiungere altri attributi di consenso, selezionare **[!UICONTROL Add result]**. In questo modo viene creata un’altra regola per l’inclusione di profili basati su tali attributi.

![L&#39;interfaccia utente del generatore dei criteri di consenso con l&#39;opzione Aggiungi risultato evidenziata.](../images/policies/add-result.png)

>[!NOTE]
>
>Per modificare un attributo esistente, selezionare il nome dell&#39;attributo e quindi l&#39;icona della matita (![Un&#39;icona della matita.](/help/images/icons/edit.png)). Viene visualizzata la finestra di dialogo **[!UICONTROL Select union schema field]** in cui è possibile apportare modifiche.
>
>![L&#39;interfaccia utente di Generatore criteri di consenso con l&#39;attributo di consenso e l&#39;icona di modifica evidenziati.](../images/policies/edit-then-attributes.png)

Continua ad aggiungere o modificare le condizioni e gli attributi di consenso fino a quando il criterio non soddisfa i tuoi requisiti. Al termine, immettere un nome e una descrizione (facoltativa), quindi selezionare **[!UICONTROL Save]** per creare il criterio.

![](../images/policies/name-and-save.png)

Il criterio di consenso è stato creato e il relativo stato è impostato su [!UICONTROL Disabled] per impostazione predefinita. Per abilitare subito il criterio, seleziona l&#39;opzione **[!UICONTROL Status]** nella barra a destra.

![](../images/policies/enable-consent-policy.png)


#### Verificare l’applicazione dei criteri

Dopo aver creato e abilitato un criterio di consenso, puoi visualizzare in anteprima come questo influisce sui tipi di pubblico consentiti quando attivi i segmenti nelle destinazioni. Per ulteriori informazioni, consulta la sezione sulla [valutazione dei criteri di consenso](../enforcement/auto-enforcement.md#consent-policy-evaluation).

## Abilitare o disabilitare un criterio {#enable}

Tutti i criteri di utilizzo dei dati (inclusi i criteri core forniti da Adobe) sono disabilitati per impostazione predefinita. Affinché un singolo criterio possa essere preso in considerazione per l’applicazione, devi abilitarlo manualmente tramite l’API o l’interfaccia utente.

È possibile abilitare o disabilitare i criteri dalla scheda **[!UICONTROL Browse]** nell&#39;area di lavoro **[!UICONTROL Policies]**. Seleziona un criterio personalizzato dall’elenco per visualizzarne i dettagli a destra. In **[!UICONTROL Status]** selezionare il pulsante di attivazione/disattivazione per attivare o disattivare il criterio.

![](../images/policies/enable-policy.png)

## Visualizzare le azioni di marketing {#view-marketing-actions}

Nell&#39;area di lavoro **[!UICONTROL Policies]**, seleziona la scheda **[!UICONTROL Marketing actions]** per visualizzare un elenco delle azioni di marketing disponibili definite da Adobe e dalla tua organizzazione.

![](../images/policies/marketing-actions.png)

## Creare un’azione di marketing {#create-marketing-action}

Per creare una nuova azione di marketing personalizzata, selezionare **[!UICONTROL Create marketing action]** nell&#39;angolo superiore destro della scheda **[!UICONTROL Marketing actions]** nell&#39;area di lavoro **[!UICONTROL Policies]**.

![](../images/policies/create-marketing-action.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Create marketing action]**. Immettere un nome e una descrizione per l&#39;azione di marketing, quindi selezionare **[!UICONTROL Create]**.

![](../images/policies/create-marketing-action-details.png)

L&#39;azione appena creata viene visualizzata nella scheda **[!UICONTROL Marketing actions]**. È ora possibile utilizzare l&#39;azione di marketing durante [la creazione di nuovi criteri di utilizzo dei dati](#create-policy).

![](../images/policies/created-marketing-action.png)

## Modificare o eliminare un’azione di marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>È possibile modificare solo le azioni di marketing personalizzate definite dall’organizzazione. Le azioni di marketing definite da Adobe non possono essere modificate o eliminate.

Nell&#39;area di lavoro **[!UICONTROL Policies]**, seleziona la scheda **[!UICONTROL Marketing actions]** per visualizzare un elenco delle azioni di marketing disponibili definite da Adobe e dalla tua organizzazione. Seleziona un’azione di marketing personalizzata dall’elenco, quindi utilizza i campi forniti nella sezione di destra per modificarne i dettagli.

![](../images/policies/edit-marketing-action.png)

Se l&#39;azione di marketing non è utilizzata da criteri di utilizzo esistenti, è possibile eliminarla selezionando **[!UICONTROL Delete marketing action]**.

>[!NOTE]
>
>Se si tenta di eliminare un’azione di marketing utilizzata da un criterio esistente, viene visualizzato un messaggio di errore a indicare che il tentativo di eliminazione non è riuscito.

![](../images/policies/delete-marketing-action.png)

## Passaggi successivi

Questo documento fornisce una panoramica su come gestire i criteri di utilizzo dei dati nell&#39;interfaccia utente [!DNL Experience Platform]. Per i passaggi su come gestire i criteri utilizzando [!DNL Policy Service API], consulta la [guida per gli sviluppatori](../api/getting-started.md). Per informazioni su come applicare i criteri di utilizzo dei dati, vedere la [panoramica sull&#39;applicazione dei criteri](../enforcement/overview.md).

Il seguente video fornisce una dimostrazione di come utilizzare i criteri di utilizzo nell&#39;interfaccia utente [!DNL Experience Platform]:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
