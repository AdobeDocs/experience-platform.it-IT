---
solution: Experience Platform
title: Scopri come creare e condividere i tuoi playbook utilizzando l’Assistente AI.
description: Come creare e condividere i tuoi playbook per casi d’uso.
role: User
exl-id: 0bc49710-ad9e-4509-b7e6-55f9b9037aa9
source-git-commit: 401062fbea8845f16803edb72ccb14b75c3f8409
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 0%

---


# Creazione e condivisione di playbook (Beta)

[!DNL Playbook Authoring Framework], basato su AI Assistant in Adobe Experience Platform, consente di creare, gestire e condividere i playbook in modo efficiente in Adobe Experience Platform.

Il framework segue un processo in tre fasi:

1. **Acquisizione metadati**: utilizza l&#39;Assistente AI o il modulo Web per acquisire i metadati del playbook.

2. **Associazione tecnica**: aggiungi al playbook risorse tecniche specifiche, ad esempio percorsi o pubblico. Puoi mantenere il controllo completo sul processo di creazione del playbook nella sandbox di sviluppo, garantendo l’allineamento con gli schemi e altre strutture di dati univoche.

3. **Distribuzione playbook**: condividi playbook tra organizzazioni diverse. Ad esempio, il Martech Center of Excellence di ACME in Germania può creare un playbook &quot;d&#39;oro&quot; e distribuirlo a organizzazioni regionali in Thailandia, Australia, ecc. per contribuire a standardizzare il caso di utilizzo del marketing.

## Creare un playbook

Puoi creare un playbook in due modi: utilizzando l’Assistente AI o manualmente. Leggi le sezioni seguenti per scoprire come creare un playbook con AI Assistant.

### Panoramica playbook

Per creare un playbook con l’Assistente AI, segui la procedura riportata di seguito:

Nel pannello di navigazione a sinistra, seleziona **[!UICONTROL Playbook]**.

![&quot;Playbook&quot; evidenziati nel riquadro di navigazione a sinistra nell&#39;interfaccia utente.](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

Seleziona **[!UICONTROL Nuovo playbook]**, quindi seleziona **Genera playbook con Assistente AI**.

![Interfaccia playbook con l&#39;opzione &quot;Genera playbook con Assistente AI&quot; selezionata.](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

Utilizza il campo prompt per descrivere il caso d’uso. Ad esempio:

&quot;Coinvolgi i clienti ACME che hanno navigato in scarpe da corsa ma non hanno completato l’acquisto.&quot;

![L&#39;interfaccia del playbook con l&#39;area del modulo Web evidenziata.](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

Seleziona **[!UICONTROL Genera]** per creare i metadati del playbook.

![L&#39;area di richiesta con il pulsante &quot;Genera&quot; playbook evidenziato.](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

Una volta generati, selezionare **[!UICONTROL Modifica]** per modificare il titolo, la descrizione e i metadati generati in base alle esigenze.

![Il playbook generato con il pulsante &quot;Modifica&quot; evidenziato.](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

Per garantire che i data engineer dispongano di tutti i dettagli necessari per impostare il caso d&#39;uso, compila la sezione **[!UICONTROL Dettagli playbook]**. Sebbene facoltativi, questi campi consentono di acquisire le informazioni chiave, semplificando il collegamento dei componenti tecnici corretti. Seleziona **[!UICONTROL Modifica]** per aggiungere valori ai campi seguenti:

* **Settore**
* **Pubblico target**
* **Canale di marketing**

![Sezione dei dettagli del playbook con il pulsante &quot;Modifica&quot; evidenziato.](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

Una volta generati i metadati, selezionare **[!UICONTROL Modifica mappa percorso]** per modificare i passaggi nella mappa percorso in base alle esigenze.

![Modifica il pulsante Mappa percorso.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![Modifica la mappa del percorso dopo aver acquisito i metadati del playbook.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

Quindi, procedi ad associare il playbook alle risorse tecniche. Per creare manualmente un playbook, selezionare **[!UICONTROL Crea playbook manualmente]**.

![Crea playbook manualmente](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

Viene visualizzato un modello di playbook vuoto. Compila dettagli come **Titolo** e **Descrizione**. Puoi anche modificare la mappa del percorso per aggiungere eventi e punti di contatto in base alle esigenze.

## Associa playbook a risorse tecniche

Indipendentemente dal fatto che si crei un playbook manualmente o con l&#39;Assistente AI, è necessario associarlo alle risorse tecniche richieste. Passa alla scheda **[!UICONTROL Assets tecnico]** e seleziona il prodotto richiesto. Selezionare **[!UICONTROL Journey Optimizer]**.

>[!NOTE]
>
> Il supporto per Real-Time CDP verrà aggiunto in una versione futura.

![La scheda &quot;Risorse tecniche&quot; e il pulsante &quot;Aggiungi prodotto richiesto&quot; sono evidenziati.](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

Scegli **[!UICONTROL Seleziona una risorsa]** per associare il playbook a un percorso, come illustrato nell&#39;immagine seguente. Quindi seleziona **Pubblica playbook** per finalizzare il playbook.

![ pulsante &quot;Seleziona risorse&quot; evidenziato nella scheda &quot;Risorse tecniche&quot;](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)

![Seleziona un percorso](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

Dopo la pubblicazione, il playbook estrae e associa automaticamente lo schema del percorso e i dettagli del pubblico.

![Playbook pubblicato](/help/use-case-playbooks/assets/playbooks/authoring/publish-playbook.png)

Tutti i playbook creati sono disponibili nella scheda **Playbook**.

![ scheda &quot;I tuoi playbook&quot;](/help/use-case-playbooks/assets/playbooks/authoring/your-playbooks-tab.png)

È possibile selezionare qualsiasi playbook dal catalogo per creare istanze da riutilizzare. Consulta la documentazione per [scoprire come creare istanze](/help/use-case-playbooks/playbooks/create-share-reuse.md).

![ Opzione &quot;Crea istanza&quot; evidenziata nella scheda &quot;Panoramica playbook&quot; dopo aver selezionato un playbook.](/help/use-case-playbooks/assets/playbooks/authoring/create-instance.png)

>[!NOTE]
>
> Una volta pubblicato un playbook, non è più possibile modificarlo. Per apportare modifiche, elimina il playbook e ricomincia.

## Esempi di prompt

L’Assistente AI può elaborare diverse strutture di prompt ed estrarre i dettagli chiave filtrando le informazioni non necessarie. Di seguito sono riportati alcuni esempi di prompt utente e della relativa interpretazione da parte del sistema:

**Esempio 1:**

&quot;Creare una campagna dal titolo &quot;Complete the Look&quot; (Completa l&#39;aspetto) per aumentare le vendite e la Customer Lifetime Value. La campagna incoraggia i clienti che hanno acquistato utensili per cucina o mobili a completare un acquisto complementare tramite consigli personalizzati e offerte correlate al loro acquisto. Inviare un messaggio ai clienti con le raccomandazioni sui prodotti. Se non effettua acquisti entro 7 giorni, riceve un secondo messaggio con consigli e offerte di prodotto. Utilizza le notifiche push e l’e-mail per contattare i clienti. Puoi rivolgerti ai clienti che hanno effettuato un acquisto negli ultimi 7 giorni nella categoria utensili da cucina o mobili e che non sono stati presi di mira negli ultimi 30 giorni. Come parte della campagna, vogliamo misurare i KPI come i clic (e-mail, app, sms, push), CTR, E-Wallet CTR, AOV Conversion.CLV Revenue, Total Purchase events (in-store, digital, call center).&quot;

![Esempio di visualizzazione di un prompt lungo nella casella di immissione testo](/help/use-case-playbooks/assets/playbooks/authoring/long-prompt.png)

**Esempio 2:**

&quot;Nome Progetto: Notiziario Moda
Sfondo: (proattivo o risoluzione del problema): un percorso progettato per inviare newsletter di moda ai clienti ACME che si sono abbonati per la comunicazione newsletter.
Obiettivo: invia e-mail newsletter moda ai clienti ACME che si sono abbonati per la comunicazione.
Dettagli promozionali: il cliente riceve notizie sulla moda nel canale e-mail settimanalmente. L’e-mail deve essere personalizzata e le varianti di contenuto devono essere basate su genere, lingua e mercato.
Canali del progetto/punti di contatto: e-mail
Pubblico di destinazione: clienti che si sono iscritti alle comunicazioni della newsletter di moda ACME.
KPI target/Metriche di coinvolgimento/ROI: 1. Aumentare i ricavi dai prodotti. 2. Incentivare la fedeltà dei clienti.&quot;

![Esempio di visualizzazione di un prompt organizzato nella casella di immissione testo](/help/use-case-playbooks/assets/playbooks/authoring/organized-list-prompt.png)

**Esempio 3:**

&quot;Spingi gli acquirenti a comprare i prodotti durante una campagna promozionale.
Coinvolgi gli acquirenti durante una promozione in corso inviando comunicazioni appropriate tramite e-mail, SMS o notifiche push per acquistare i prodotti. Invia loro un promemoria e-mail dopo 24 ore se non sono coinvolti nella promozione.&quot;

![Esempio di visualizzazione di un prompt conciso nella casella di immissione testo](/help/use-case-playbooks/assets/playbooks/authoring/concise-prompt.png)

**Esempio 4:**

&quot;Vendi scarpe ai giocatori delle scuole superiori.&quot;

![Esempio di richiesta di una riga](/help/use-case-playbooks/assets/playbooks/authoring/one-liner-prompt.png)

L’Assistente AI rimuove tutti i dettagli non necessari, ad esempio &quot;Nome progetto&quot; o &quot;Sfondo&quot;. Estrae gli elementi chiave come &quot;pubblico target&quot;, &quot;obiettivo della campagna&quot; e &quot;canale di marketing&quot; e funziona con qualsiasi stile di input.

Questi esempi mostrano come l’intelligenza artificiale può perfezionare ed estrarre dettagli essenziali dai prompt degli utenti.

>[!NOTE]
>
> Evita PII o parole esplicite mentre scrivi le tue richieste.

## Linee guida per i contenuti e moderazione

Quando crei i playbook, presta attenzione alla lingua e al contenuto che includi. I playbook sono visibili in tutta l’organizzazione e qualsiasi contenuto offensivo o inappropriato può essere segnalato dagli utenti.

### Segnalazione e processo di revisione

Se un playbook viene segnalato come contenuto inappropriato o offensivo, viene automaticamente segnalato ad Adobe per la revisione. Adobe esamina quindi il contenuto contrassegnato e, se ritenuto inappropriato, ne riceve una notifica al cliente e la playbook viene rimossa.

## Condivisione di playbook tra sandbox {#sharing-playbooks-sandboxes}

Se l’organizzazione contiene più sandbox, non è necessario condividere manualmente i playbook tra di esse. Una volta creato e pubblicato un playbook in una sandbox, questo diventa disponibile in tutte le sandbox all’interno di tale organizzazione. Puoi quindi creare istanze di quel playbook in una qualsiasi delle altre sandbox.

Se la playbook fa riferimento a campi non disponibili nello schema di unione della sandbox di destinazione o privi delle autorizzazioni necessarie, è possibile che venga visualizzato un messaggio di errore quando si tenta di creare l’istanza. Il messaggio richiama i campi mancanti e/o le autorizzazioni mancanti.

Se mancano campi nello schema di unione, una finestra di dialogo li evidenzia durante l’importazione.

![Campi mancanti nello schema di unione elencato durante il processo di importazione](/help/use-case-playbooks/assets/playbooks/authoring/missing-fields.png)

## Condivisione dei playbook in più organizzazioni {#sharing-playbooks-organizations}

Per condividere un playbook da un&#39;organizzazione all&#39;altra, eseguire la procedura seguente:

* **Accedi all&#39;organizzazione di origine**: accedi all&#39;organizzazione contenente il playbook creato e vuoi condividerlo dalla scheda **[!UICONTROL Playbook]**.
* **Pubblica il playbook**: se il playbook non è già pubblicato, è necessario pubblicarlo prima di condividerlo.

>[!NOTE]
>
>È necessario stabilire una partnership tra le organizzazioni di origine e di destinazione per consentire la condivisione dei playbook. Scopri come [creare una richiesta di partnership organizzazione](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/ui/sharing-packages-across-orgs).

* **Avvia la condivisione**: una volta pubblicato il playbook e stabilita una relazione, selezionare **[!UICONTROL Condividi playbook]**.
* **Selezionare l&#39;organizzazione di destinazione**: scegliere l&#39;organizzazione con cui si desidera condividere il playbook quando richiesto.
* **Conferma e condividi**: conferma la selezione. Riceverai messaggi di conferma che indicano che la condivisione è andata a buon fine.
* **Verifica l&#39;organizzazione di destinazione**: accedi all&#39;organizzazione di destinazione per verificare che il playbook sia disponibile.
* **Importa playbook**: seleziona **[!UICONTROL Importa]** per inserire il playbook nell&#39;organizzazione di destinazione. Puoi visualizzarlo nella scheda **Playbook**.

Se il playbook non viene visualizzato, assicurati che sia pubblicato e che la partnership con l’organizzazione sia attiva.

>[!IMPORTANT]
>
>La condivisione transitiva della playbook non è supportata. Se si condivide un playbook da un&#39;organizzazione a un&#39;altra e quindi lo si importa, non è possibile condividerlo nuovamente dall&#39;organizzazione ricevente a una terza organizzazione.

## Autorizzazioni richieste

Per accedere alla sandbox e utilizzare questa funzione, è necessario disporre delle seguenti autorizzazioni:

* **Autorizzazioni sandbox**:

Questi sono necessari per accedere all’ambiente sandbox in cui è presente la funzione:

* **Gestisci sandbox**
* **Visualizza sandbox**

* **Autorizzazioni di condivisione pacchetti**:

Queste autorizzazioni sono necessarie per la funzionalità di condivisione interna:

* [**Gestisci pacchetto**](/help/sandboxes/ui/sandbox-tooling.md)
* [**Condividi pacchetto**](/help/sandboxes/ui/sharing-packages-across-orgs.md)

Queste autorizzazioni ti consentiranno di:

* Inserisci l’ambiente sandbox
* Accedere alla funzione all’interno della sandbox
* Gestisci e condividi pacchetti secondo necessità

Queste autorizzazioni si trovano nella sezione **[!UICONTROL Sandbox]** dell&#39;elenco delle autorizzazioni.

![L&#39;elenco delle autorizzazioni con le autorizzazioni pertinenti evidenziate.](/help/use-case-playbooks/assets/playbooks/authoring/permissions.png)

### Percorsi e oggetti correlati - autorizzazioni

Durante la creazione di Percorsi che utilizzano i playbook, è probabile che si faccia riferimento ad altri oggetti come **Canali**, **Tipi di pubblico** e altre entità. Ognuno di questi ha un proprio set di autorizzazioni.

Queste sono le autorizzazioni chiave per le azioni relative al Percorso, ad esempio:

* **Visualizza percorso**
* **Gestisci percorso**
* Autorizzazioni relative a oggetti come tipi di pubblico e canali

Saranno inoltre necessarie le seguenti autorizzazioni per il pubblico:

* **Segmento letto**
* **Profilo letto**
* **Set di dati letto**

Poiché i Percorsi sono altamente flessibili e possono coinvolgere molti oggetti interconnessi, le relative [autorizzazioni complete](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/privacy/high-low-permissions) sono documentate separatamente e possono variare in base al caso d&#39;uso specifico.

## Passaggi successivi

Ora che sai come creare, pubblicare e condividere playbook utilizzando l&#39;Assistente AI, scopri come iniziare a utilizzare i playbook disponibili e scegli quello giusto per il tuo caso d&#39;uso da [Elenco playbook](/help/use-case-playbooks/playbooks/choose.md).