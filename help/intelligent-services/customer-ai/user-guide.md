---
keywords: Experience Platform;user guide;customer ai;popular topics
solution: Experience Platform
title: Guida utente AI del cliente
topic: User guide
translation-type: tm+mt
source-git-commit: 7987cec12c22e9b48ddc9fdc263d7cd28bd172f2

---


# Guida utente AI del cliente

L&#39;AI del cliente, come parte di Intelligent Services consente di generare punteggi personalizzati di propensione senza doversi preoccupare dell&#39;apprendimento automatico.

Questa guida descrive i passaggi per lavorare con l&#39;AI del cliente. Sono disponibili dei passaggi per i seguenti argomenti:

* [Configurare un&#39;istanza](#configure-an-instance)
* [Creazione di segmenti di clienti con punteggi previsti](#create-customer-segments-with-predicted-scores)

Inoltre, l&#39;appendice di questa esercitazione fornisce informazioni sull&#39; [output dell&#39;AI](#customer-ai-output-data)cliente.

## Configurare un&#39;istanza

I servizi intelligenti forniscono ai clienti un servizio Adobe Sensei semplice da usare che può essere configurato per diversi casi di utilizzo. Le sezioni seguenti forniscono i passaggi per configurare un&#39;istanza dell&#39;API cliente.

### Configurare l’istanza

Nell’interfaccia utente della piattaforma, fai clic su **Servizi** nella barra di navigazione a sinistra. Viene visualizzato il browser **Servizi** , che visualizza tutti i servizi disponibili. Nel contenitore per l&#39;API cliente, fate clic su **Apri**.

![](./images/user-guide/navigate-to-service.png)

Nella schermata *Customer AI* (AI cliente) sono visualizzate tutte le istanze AI del cliente esistenti. Fate clic su **Crea istanza**.

![](./images/user-guide/dashboard.png)

Viene visualizzato il flusso di lavoro per la creazione dell’istanza, a partire dal passaggio *Configurazione* .

Di seguito sono riportate informazioni importanti sui valori che è necessario fornire all’istanza con:

* Il nome dell&#39;istanza viene utilizzato in tutti i punti in cui viene visualizzato il punteggio AI del cliente. I nomi dovrebbero quindi descrivere ciò che i punteggi di previsione rappresentano, ad esempio, &quot;Probabilità di annullare l&#39;iscrizione alla rivista&quot;.

* Il tipo di propensione determina l&#39;intento del punteggio e la polarità della metrica. È possibile scegliere **Churn** o **Conversion**. Per ulteriori informazioni su come il tipo di propensione influisce sull’istanza, vedere la nota sotto il riepilogo [del](./discover-insights.md#scoring-summary) punteggio nel documento di approfondimento.

* Origine dati è la posizione in cui si trovano i dati. Set di dati è il set di dati di input utilizzato per prevedere i punteggi. Per impostazione predefinita, l&#39;AI del cliente utilizza i dati Evento esperienza cliente per calcolare i punteggi di propensione. Quando si seleziona un dataset dal selettore a discesa, vengono elencati solo quelli compatibili con l&#39;API del cliente.

* Per impostazione predefinita, i punteggi di propensione vengono generati per tutti i profili, a meno che non sia specificata una popolazione idonea. Potete specificare una popolazione idonea definendo le condizioni per includere o escludere i profili in base agli eventi.

Immettete i valori richiesti e fate clic su **Avanti**.

![](./images/user-guide/setup.png)

### Definire un obiettivo

Viene visualizzato il passaggio *Definisci obiettivo* , che fornisce un ambiente interattivo per definire visivamente un obiettivo. Un obiettivo è composto da uno o più eventi, in cui ogni occorrenza dell&#39;evento è basata sulla condizione in cui si trova. L&#39;obiettivo di un&#39;istanza AI del cliente è determinare la probabilità di raggiungere il suo obiettivo entro un determinato intervallo di tempo.

Fare clic su **Inserisci nome** campo e selezionare un campo dall&#39;elenco a discesa. Fate clic sul secondo input e selezionate una clausola per la condizione dell&#39;evento, quindi fornite il valore target per completare l&#39;evento. È possibile configurare altri eventi facendo clic su **Aggiungi evento**. Infine, completare l&#39;obiettivo applicando un periodo di tempo di previsione in numero di giorni, quindi fare clic su **Avanti**.

![](./images/user-guide/goal.png)

### Configurare una pianificazione *(facoltativo)*

Viene visualizzato il passaggio *avanzato* . Questo passaggio facoltativo consente di configurare una pianificazione per l&#39;automazione delle esecuzioni di previsione, definire esclusioni di previsione per filtrare determinati eventi, oppure fare clic su **Fine** se non è necessario nulla.

Imposta una pianificazione del punteggio configurando la Frequenza ** punteggio. Le esecuzioni di previsione automatizzate possono essere pianificate per essere eseguite su base settimanale o mensile.

![](./images/user-guide/schedule.png)

Sotto la configurazione della pianificazione, potete definire esclusioni di previsione per evitare che gli eventi che soddisfano determinate condizioni vengano valutati al momento della generazione dei punteggi. Questa funzione può essere utilizzata per filtrare gli input di dati irrilevanti.

Per escludere determinati eventi, fate clic su **Aggiungi esclusione** e definite l&#39;evento nello stesso modo in cui è definito l&#39;obiettivo. Per rimuovere un&#39;esclusione, fate clic sulle ellissi (**...**) in alto a destra del contenitore dell&#39;evento, quindi fate clic su **Rimuovi contenitore**.

![](./images/user-guide/exclusion.png)

Escludete gli eventi in base alle esigenze, quindi fate clic su **Fine** per creare l&#39;istanza.

![](./images/user-guide/advanced.png)

Se l&#39;istanza viene creata correttamente, viene attivata immediatamente un&#39;esecuzione della previsione ed eseguita in base alla pianificazione definita.

>[!NOTE] A seconda della dimensione dei dati di input, l&#39;esecuzione della previsione può richiedere fino a 24 ore per essere completata.

Seguendo questa sezione, hai configurato un&#39;istanza dell&#39;AI cliente ed è stata eseguita un&#39;esecuzione di previsione. Al completamento dell&#39;esecuzione, le informazioni con punteggio popolano automaticamente i profili con punteggi previsti. Attendere fino a 24 ore prima di continuare con la sezione successiva dell&#39;esercitazione.

## Creazione di segmenti di clienti con punteggi previsti

Al termine di un&#39;esecuzione della previsione, i punteggi di propensione previsti vengono automaticamente utilizzati da Profili. L&#39;arricchimento dei profili con i punteggi AI dei clienti consente di creare segmenti di clienti per trovare audience in base ai loro punteggi di propensione. Questa sezione descrive i passaggi per la creazione di segmenti con Segment Builder (Generatore di segmenti). Per un’esercitazione più affidabile sulla creazione di segmenti, consulta la guida [utente di](../../segmentation/tutorials/create-a-segment.md)Segment Builder (Generatore di segmenti).

>[!IMPORTANT] Per utilizzare questo metodo, è necessario abilitare il profilo cliente in tempo reale per il set di dati.

Nell’interfaccia utente della piattaforma, fai clic su **Segmenti** nella barra di navigazione a sinistra, quindi fai clic su **Crea segmento**.

![](./images/user-guide/segments.png)

Viene visualizzato *Segment Builder (Generatore* di segmenti). Dalla colonna *Campi* a sinistra e nella scheda *Attributi* , fare clic sulla cartella denominata **XDM Individuale Profile** , quindi fare clic sulla cartella contenente lo spazio dei nomi dell&#39;organizzazione. La cartella denominata **Customer AI** contiene i risultati delle esecuzioni di previsione e prende il nome dall’istanza a cui appartengono i punteggi. Fate clic su una cartella di istanza per accedere ai risultati dell’istanza desiderata.

![](./images/user-guide/results.png)

Situato al centro di Segment Builder (Generatore di segmenti), trascina l’attributo **Score** nell’area di lavoro del generatore di *regole* per definire una regola.

Nella colonna delle proprietà *del* segmento a destra, specifica un nome per il segmento.

![](./images/user-guide/properties.png)

Sopra la colonna *Campi* a sinistra, fate clic sull’icona a forma di **ingranaggio** e selezionate un criterio **di** unione. Fai clic su **Salva** per creare il segmento.

![](./images/user-guide/merge_policy.png)

## Passaggi successivi

Seguendo questa esercitazione, hai configurato con successo un&#39;istanza di AI cliente, generato punteggi di propensione e individuato audience in base ai loro punteggi di propensione utilizzando il Generatore di segmenti. Ora potete eseguire il targeting delle audience attivandole nelle destinazioni. Per ulteriori informazioni, consulta [la panoramica](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) delle destinazioni.

## Appendice

La sezione seguente fornisce informazioni aggiuntive sull&#39;output dell&#39;AI cliente.

### Dati di output AI del cliente

L&#39;AI del cliente genera diversi attributi per i singoli profili ritenuti idonei. Questi valori vengono utilizzati dal profilo cliente in tempo reale, che può essere utilizzato per creare e definire segmenti. La tabella seguente descrive i vari attributi rilevati nell&#39;output dell&#39;AI cliente:

| Attributo | Descrizione |
| ----- | ----------- |
| Punteggio | La probabilità relativa che un cliente raggiunga l&#39;obiettivo previsto entro il periodo di tempo definito. Questo valore non deve essere trattato come una percentuale di probabilità, ma piuttosto come la probabilità di un individuo rispetto alla popolazione complessiva. Questo punteggio va da 0 a 100. |
| Probabilità | Questo attributo è la vera probabilità di un profilo per raggiungere l&#39;obiettivo previsto entro il periodo di tempo definito. Quando si confrontano gli output tra obiettivi diversi, si consiglia di considerare la probabilità rispetto al percentile o al punteggio. La probabilità dovrebbe sempre essere utilizzata per determinare la probabilità media tra la popolazione ammissibile, in quanto la probabilità tende a essere sul lato inferiore per gli eventi che non si verificano frequentemente. I valori per l’intervallo di probabilità sono compresi tra 0 e 1. |
| Percentile | Questo valore fornisce informazioni sulle prestazioni di un profilo rispetto ad altri profili con punteggio simile. Ad esempio, un profilo con un grado percentile pari a 99 per il churn indica che il rischio di esecuzione è maggiore rispetto al 99% di tutti gli altri profili con punteggio. Le percentuali sono comprese tra 1 e 100. |
| Tipo tendenza | Il tipo di propensione selezionato. |
| Data punteggio | Data in cui si è verificato il punteggio. |
| Fattori di influenza | Motivi previsti sul motivo per cui un profilo può essere convertito o churn. I fattori sono formati dai seguenti attributi:<ul><li>Codice: L&#39;attributo di profilo o di comportamento che influenza positivamente il punteggio previsto di un profilo. </li><li>Valore: Il valore dell&#39;attributo di profilo o di comportamento.</li><li>Importanza: Indica il peso dell&#39;attributo di profilo o di comportamento sul punteggio previsto (basso, medio, alto)</li></ul> |