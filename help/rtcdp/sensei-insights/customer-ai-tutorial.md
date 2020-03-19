---
title: Predire i punteggi di propensione del cliente utilizzando l'intelligenza artificiale del cliente (alfa)
seo-title: Predire i punteggi di propensione del cliente utilizzando l'intelligenza artificiale del cliente (alfa)
description: Questa esercitazione fornisce istruzioni sull'utilizzo dell'interfaccia utente (alpha) del cliente
seo-description: Questa esercitazione fornisce istruzioni sull'utilizzo dell'interfaccia utente (alpha) del cliente
index: false
translation-type: tm+mt
source-git-commit: 1118983ce8f5704ef3a347c8c316a9cc5cc62815

---


# Predire i punteggi di propensione del cliente utilizzando l&#39;intelligenza artificiale del cliente (alfa)

>[!NOTE]
>La funzionalità dell&#39;intelligenza artificiale del cliente descritta in questo documento è in alfa. La documentazione e la funzionalità sono soggette a modifiche.

Creato e basato su Adobe Sensei, Customer AI in Adobe Experience Platform consente di generare valutazioni di propensione personalizzate senza doversi preoccupare degli aspetti di machine learning.

Questa esercitazione descrive i passaggi per lavorare con l&#39;AI cliente utilizzando l&#39;interfaccia utente della piattaforma Experience. Sono disponibili dei passaggi per i seguenti argomenti:

* [Configurare un&#39;istanza](#configure-an-instance)
* [Creazione di segmenti di clienti con punteggi previsti](#create-customer-segments-with-predicted-scores)

## Introduzione

Questa guida richiede una buona conoscenza dei vari servizi della piattaforma coinvolti nell&#39;utilizzo dell&#39;AI del cliente. Prima di iniziare questa esercitazione, consulta i documenti seguenti:

* [Panoramica del profilo cliente in tempo reale](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)
* [Panoramica del servizio di segmentazione](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segmentation-overview.md)
* [Guida utente di Segment Builder](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segment-builder-guide.md)

## Configurare un&#39;istanza

La piattaforma Experience offre ai clienti un servizio semplice per utilizzare il servizio Adobe Sensei che può essere configurato per diversi casi di utilizzo. Le sezioni seguenti forniscono i passaggi per configurare un&#39;istanza dell&#39;API cliente.

### Impostazione dell’istanza

Nell’interfaccia utente della piattaforma, fai clic su **Servizi** nella barra di navigazione a sinistra. Viene visualizzato il browser **Servizi** , che visualizza tutti i servizi disponibili. Nel contenitore per l&#39;API cliente, fate clic su **Apri**.

![](./images/service.png)

Nella schermata *Customer AI* (AI cliente) sono visualizzate tutte le istanze AI del cliente esistenti. Fate clic su **Crea istanza**.

![](./images/customer_ai.png)

Viene visualizzato il flusso di lavoro per la creazione dell’istanza, a partire dal passaggio *Configurazione* .

Di seguito sono riportate informazioni importanti sui valori per i quali è necessario fornire all&#39;istanza:

* Il nome dell&#39;istanza verrà utilizzato in tutti i punti in cui viene visualizzato il punteggio AI del cliente. Per questo motivo i nomi dovrebbero descrivere ciò che i punteggi di previsione rappresentano, ad esempio, &quot;Probabilità di annullare l&#39;iscrizione alla rivista&quot;.

* Il tipo di propensione determina l&#39;intento del punteggio e la polarità della metrica. È possibile scegliere **Churn** o **Conversion**.

* L&#39;origine dati fa riferimento al set di dati di input che verrà utilizzato per prevedere i punteggi. Per impostazione predefinita, l&#39;AI del cliente utilizza i dati Evento esperienza cliente per calcolare i punteggi di propensione. Quando si seleziona un dataset dal selettore a discesa, saranno elencati solo quelli compatibili con l&#39;API del cliente.

* Per impostazione predefinita, i punteggi di propensione vengono generati per tutti i profili, a meno che non sia specificata una popolazione idonea. Potete specificare una popolazione idonea definendo le condizioni per includere o escludere i profili in base agli eventi.

Immettete i valori richiesti e fate clic su **Avanti**.

![](./images/setup.png)

### Definire un obiettivo

Viene visualizzato il passaggio *Definisci obiettivo* , che fornisce un ambiente interattivo per definire visivamente un obiettivo. Un obiettivo è composto da uno o più eventi, in cui ogni occorrenza dell&#39;evento è basata sulla condizione in cui si trova. L&#39;obiettivo di un&#39;istanza AI del cliente è determinare la probabilità di raggiungere il suo obiettivo entro un determinato intervallo di tempo.

Fare clic su **Inserisci nome** campo e selezionare un campo dall&#39;elenco a discesa. Fate clic sul secondo input e selezionate una clausola per la condizione dell&#39;evento, quindi fornite il valore target per completare l&#39;evento. È possibile configurare altri eventi facendo clic su **Aggiungi evento**. Infine, completare l&#39;obiettivo applicando un periodo di tempo di previsione in numero di giorni, quindi fare clic su **Avanti**.

![](./images/goal.png)

### Configurare una pianificazione *(facoltativo)*

Viene visualizzato il passaggio *avanzato* . Questo passaggio facoltativo consente di configurare una pianificazione per l&#39;automazione delle esecuzioni di previsione, definire esclusioni di previsione per filtrare determinati eventi, oppure fare clic su **Fine** se non è necessario nulla.

Imposta una pianificazione del punteggio configurando la Frequenza ** punteggio. Le esecuzioni di previsione automatizzate possono essere pianificate per essere eseguite su base settimanale o mensile.

![](./images/schedule.png)

Sotto la configurazione della pianificazione, potete definire esclusioni di previsione per evitare che gli eventi che soddisfano determinate condizioni vengano valutati al momento della generazione dei punteggi. Questa funzione può essere utilizzata per filtrare gli input di dati irrilevanti.

Per escludere determinati eventi, fate clic su **Aggiungi esclusione** e definite l&#39;evento nello stesso modo in cui è definito l&#39;obiettivo. Per rimuovere un&#39;esclusione, fate clic sulle ellissi (**...**) in alto a destra del contenitore dell&#39;evento, quindi fate clic su **Rimuovi contenitore**.

![](./images/exclusion.png)

Escludete gli eventi in base alle esigenze, quindi fate clic su **Fine** per creare l&#39;istanza.

![](./images/advanced.png)

Se l&#39;istanza viene creata correttamente, verrà attivata immediatamente un&#39;esecuzione di previsione e quelle successive verranno eseguite in base alla pianificazione definita.

>   **Nota:** A seconda della dimensione dei dati di input, l&#39;esecuzione della previsione può richiedere fino a 24 ore per essere completata.

Seguendo questa sezione, hai configurato un&#39;istanza dell&#39;AI cliente ed è stata eseguita un&#39;esecuzione di previsione. Al completamento dell&#39;esecuzione, le informazioni di punteggio verranno automaticamente idratate nei Profili con punteggi previsti. Attendere 24 ore prima di continuare con la sezione successiva dell&#39;esercitazione.

## Creazione di segmenti di clienti con punteggi previsti

Al termine di un&#39;esecuzione della previsione, i punteggi di propensione previsti vengono automaticamente utilizzati da Profili. L&#39;arricchimento dei profili con i punteggi AI del cliente consente di creare segmenti di clienti basati sui punteggi di propensione. Questa sezione descrive i passaggi per la creazione di segmenti con Segment Builder (Generatore di segmenti). Per un’esercitazione più affidabile sulla creazione di segmenti, consulta la guida [utente di](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segment-builder-guide.md)Segment Builder (Generatore di segmenti).

Nell’interfaccia utente della piattaforma, fai clic su **Segmenti** nella barra di navigazione a sinistra, quindi fai clic su **Crea segmento**.

![](./images/segments.png)

Viene visualizzato *Segment Builder (Generatore* di segmenti). Dalla colonna *Campi* a sinistra e nella scheda *Attributi* , fare clic sulla cartella denominata **XDM Individuale Profile** , quindi fare clic sulla cartella contenente lo spazio dei nomi dell&#39;organizzazione. La cartella denominata **Customer AI** contiene i risultati delle esecuzioni di previsione e prende il nome dall’istanza a cui appartengono i punteggi. Fate clic su e accedete ai risultati dell’istanza desiderata.

![](./images/results.png)

Situato al centro di Segment Builder (Generatore di segmenti), trascina l’attributo **Score** nell’area di lavoro del generatore di *regole* per definire una regola.

Nella colonna delle proprietà ** del segmento destra, seleziona un criterio *di* unione e specifica un nome per il segmento, quindi fai clic su **Salva** per creare il segmento.

![](./images/properties.png)

## Passaggi successivi

Seguendo questa esercitazione, hai configurato con successo un&#39;istanza di AI cliente, generato punteggi di propensione e creato un segmento imposto dai punteggi di propensione utilizzando il Generatore di segmenti. Ora il segmento del cliente può essere utilizzato dalle destinazioni attivate per indirizzare il pubblico. Per ulteriori informazioni, consulta la panoramica [](../destinations/destinations-overview.md) Destinazioni.
