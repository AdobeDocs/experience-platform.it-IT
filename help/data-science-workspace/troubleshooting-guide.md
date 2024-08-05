---
keywords: Experience Platform; risoluzione dei problemi; Data Science Area di lavoro; Argomenti comuni
solution: Experience Platform
title: Guida alla risoluzione dei problemi di Data Science Workspace
description: Questo documento fornisce le risposte alle domande più frequenti su Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi di [!DNL Data Science Workspace]

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

In questo documento vengono fornite le risposte alle domande più frequenti su Adobe Experience Platform [!DNL Data Science Workspace]. Per domande e risoluzione dei problemi relativi alle [!DNL Platform] API in generale, consulta la [Adobe Experience Platform Guida](../landing/troubleshooting.md) alla risoluzione dei problemi relativi alle API.

## Stato della query JupyterLab Notebook bloccato nello stato di esecuzione

Un notebook JupyterLab può indicare che una cella si trova nello stato di esecuzione, a tempo indeterminato, in alcune condizioni di memoria esaurita. Ad esempio, quando si esegue una query su un set di dati di grandi dimensioni o si eseguono più query successive, JupyterLab Notebook può esaurire la memoria disponibile per memorizzare l’oggetto dataframe risultante. Vi sono alcuni indicatori che possono essere osservati in questa situazione. Innanzitutto, il kernel entra nello stato inattivo anche se la cella viene visualizzata come in esecuzione, indicata dall&#39;icona [`*`] accanto alla cella. Inoltre, la barra inferiore indica la quantità di RAM utilizzata/disponibile.

![RAM disponibile](./images/jupyterlab/user-guide/allocate-ram.png)

Durante la lettura dei dati, la memoria può aumentare fino a raggiungere la quantità massima di memoria allocata. La memoria viene liberata non appena viene raggiunta la memoria massima e il kernel si riavvia. Ciò significa che la memoria utilizzata in questo scenario potrebbe essere molto bassa a causa del riavvio del kernel, mentre appena prima del riavvio, la memoria sarebbe stata molto vicina alla RAM massima allocata.

Per risolvere questo problema, seleziona l&#39;icona ingranaggio in alto a destra di JupyterLab e fai scorrere il dispositivo di scorrimento verso destra, quindi seleziona **[!UICONTROL Aggiorna configurazioni]** per allocare più RAM. Inoltre, se si eseguono più query e il valore RAM si avvicina alla quantità massima allocata, a meno che non siano necessari i risultati delle query precedenti, riavviare il kernel per reimpostare la quantità di RAM disponibile. In questo modo è possibile disporre della quantità massima di RAM disponibile per la query corrente.

![allocare più ram](./images/jupyterlab/user-guide/notebook-gpu-config.png)

Nel caso in cui si stia allocando la quantità massima di memoria (RAM) e si verifichi ancora questo problema, è possibile modificare la query per operare su un set di dati di dimensioni inferiori riducendo le colonne o l’intervallo di dati. Per utilizzare l&#39;intera quantità di dati, si consiglia di utilizzare un notebook Spark.

## L&#39;ambiente [!DNL JupyterLab] non viene caricato in [!DNL Google Chrome]

>[!IMPORTANT]
>
>Questo problema è stato risolto ma potrebbe essere ancora presente nel browser Google Chrome 80.x. Verifica che il browser Chrome sia aggiornato.

Con la versione 80.x del browser [!DNL Google Chrome], tutti i cookie di terze parti sono bloccati per impostazione predefinita. Questo criterio può impedire il caricamento di [!DNL JupyterLab] in Adobe Experience Platform.

Per risolvere il problema, attenersi alla procedura descritta di seguito.

Nel browser [!DNL Chrome], passa in alto a destra e seleziona **Impostazioni** (in alternativa puoi copiare e incollare &quot;chrome://settings/&quot; nella barra degli indirizzi). Successivo, scorri fino alla parte inferiore della pagina e fai clic sul **menu a discesa Avanzate** .

![avanzato per Chrome](./images/faq/chrome-advanced.png)

Viene visualizzata la sezione **Privacy e sicurezza**. Fare clic su **Impostazioni sito** seguito da **Cookie e dati sito**.

![avanzato per Chrome](./images/faq/privacy-security.png)

![avanzato per Chrome](./images/faq/cookies.png)

Infine, imposta &quot;Blocca cookie di terze parti&quot; su &quot;OFF&quot;.

![Chrome Advanced](./images/faq/toggle-off.png)

>[!NOTE]
>
>In alternativa, è possibile disabilitare i cookie di terze parti e aggiungere [*.]ds.adobe.net all&#39;elenco Consenti.

Vai a &quot;chrome://flags/&quot; nella barra degli indirizzi. Search e disabilita il contrassegno intitolato *&quot;Cookie SameSite by default&quot;* utilizzando il menu a discesa sulla destra.

![Disattiva contrassegno SameSite](./images/faq/samesite-flag.png)

Dopo il passaggio 2, viene richiesto di riavviare il browser. Dopo il riavvio, [!DNL Jupyterlab] dovrebbe essere accessibile.

## Perché non riesco a accesso [!DNL JupyterLab] in Safari?

Safari disabilita i cookie di terze parti per impostazione predefinita in Safari &lt; 12. Poiché il [!DNL Jupyter] istanza della macchina virtuale risiede in un dominio diverso da quello del frame padre, Adobe Experience Platform attualmente richiede che i cookie di terze parti siano abilitati. Abilita i cookie di terze parti o passa a un browser diverso, ad esempio [!DNL Google Chrome].

Per Safari 12, devi impostare l&#39;agente utente su &#39;[!DNL Chrome]&#39; o &#39;[!DNL Firefox]&#39;. Per cambiare agente utente, apri il *menu Safari* e seleziona **Preferenze**. Viene visualizzata la finestra delle preferenze.

![Preferenze Safari](./images/faq/preferences.png)

Nella finestra delle preferenze di Safari, seleziona **Avanzate**. Selezionare quindi la casella *Mostra menu Sviluppo nella barra dei menu*. Al termine di questo passaggio è possibile chiudere la finestra delle preferenze.

![Safari avanzato](./images/faq/advanced.png)

Quindi, dalla barra di navigazione superiore, seleziona il menu **Sviluppo**. Dall&#39;elenco a discesa **Sviluppo**, passa il puntatore del mouse su **Agente utente**. Puoi selezionare la stringa o **[!DNL Firefox]** agente **[!DNL Chrome]** utente che desideri like usare.

![Menu Sviluppo](./images/faq/user-agent.png)

## Perché viene visualizzato il messaggio &quot;403 Vietato&quot; quando provo a caricare o eliminare un file in [!DNL JupyterLab]?

Se il tuo browser è abilitato con software di blocco degli annunci pubblicitari come [!DNL Ghostery] o [!DNL AdBlock] Plus, il dominio &quot;\*.adobe.net&quot; deve essere consentito in ogni software di blocco degli annunci per [!DNL JupyterLab] funzionare normalmente. Questo perché [!DNL JupyterLab] le macchine virtuali vengono eseguite in un dominio diverso da quello del [!DNL Experience Platform] dominio.

## Perché alcune parti del mio [!DNL Jupyter Notebook] aspetto vengono codificate o non vengono visualizzate come codice?

Questo può accadere se la cella in questione viene accidentalmente modificata da &quot;Code&quot; a &quot;Markdown&quot;. Mentre una cella di codice è attiva, premendo la combinazione **di tasti ESC+M** il tipo di cella viene impostato su Markdown. Il tipo di cella può essere modificato dall&#39;indicatore a discesa nella parte superiore del blocco appunti per le celle selezionate. Per modificare un tipo di cella in codice, selezionare innanzitutto la cella specificata che si desidera modificare. Successivo, fai clic sul menu a discesa che indica il tipo corrente della cella, quindi seleziona &quot;Code&quot;.

![](./images/faq/code_type.png)

## Come si installano i librerie personalizzati [!DNL Python] ?

Il [!DNL Python] kernel è preinstallato con molti librerie di machine learning popolari. Tuttavia, è possibile installare ulteriori librerie personalizzati eseguendo il comando seguente all&#39;interno di una cella di codice:

```shell
!pip install {LIBRARY_NAME}
```

Per un elenco completo dei librerie preinstallati [!DNL Python] , vedere la [sezione appendice del Guida utente](./jupyterlab/overview.md#supported-libraries) JupyterLab.

## Posso installare librerie PySpark personalizzati?

Sfortunatamente, non è possibile installare librerie aggiuntive per il kernel PySpark. Tuttavia, puoi contattare il tuo rappresentante del servizio clienti Adobe Systems per installare librerie PySpark personalizzati.

Per un elenco delle librerie PySpark preinstallate, consulta la [sezione dell&#39;appendice della Guida utente di JupyterLab](./jupyterlab/overview.md#supported-libraries).

## È possibile configurare [!DNL Spark] risorse cluster per [!DNL JupyterLab] [!DNL Spark] o il kernel PySpark?

È possibile configurare le risorse aggiungendo il seguente blocco alla prima cella del blocco appunti:

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

Per ulteriori informazioni sulla [!DNL Spark] configurazione delle risorse del cluster, incluso l&#39;elenco completo delle proprietà configurabili, vedere la [Guida utente](./jupyterlab/overview.md#kernels) JupyterLab.

## Perché ricevo un errore quando provo a eseguire determinate attività per set di dati più grandi?

Se viene visualizzato un errore con un motivo come `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Ciò significa in genere che il driver o un esecutore sta esaurendo la memoria. Per ulteriori informazioni sui limiti dei dati e su come eseguire attività su set di dati di grandi dimensioni, vedere la documentazione relativa ai dati accesso di](./jupyterlab/access-notebook-data.md) JupyterLab Notebooks[. In genere questo errore può essere risolto modificando il `mode` da `interactive` a `batch`.

Inoltre, durante la scrittura di set di dati Spark/PySpark di grandi dimensioni, caching i dati (`df.cache()`) prima di eseguire il codice di scrittura può migliorare notevolmente le prestazioni.

<!-- remove this paragraph at a later date once the sdk is updated -->

Se riscontri problemi durante la lettura dei dati e applichi trasformazioni ai dati, prova a memorizzare i dati nella cache prima delle trasformazioni. La memorizzazione nella cache dei dati impedisce la lettura multipla in rete. Inizia leggendo i dati. Quindi, memorizzare nella cache (`df.cache()`) i dati. Infine, esegui le tue trasformazioni.

## Perché i miei notebook Spark/PySpark impiegano così tanto tempo per leggere e scrivere dati?

Se si eseguono trasformazioni sui dati, ad esempio utilizzando `fit()`, è possibile che le trasformazioni vengano eseguite più volte. Per migliorare le prestazioni, memorizzare i dati nella cache utilizzando `df.cache()` prima di eseguire `fit()`. In questo modo le trasformazioni vengono eseguite una sola volta e si evitano più letture in rete.

**Ordine consigliato:** Iniziare con la lettura dei dati. Eseguire quindi le trasformazioni seguite dalla memorizzazione nella cache (`df.cache()`) dei dati. Infine, eseguire `fit()`.

## Perché i notebook Spark/PySpark non vengono eseguiti?

Se ricevi uno dei seguenti errori:

- Processo interrotto a causa di un errore della fase... È possibile comprimere solo gli RDD con lo stesso numero di elementi in ogni partizione.
- Client RPC remoto disassociato e altri errori di memoria.
- Scarse prestazioni durante la lettura e la scrittura di set di dati.

Verificare che i dati vengano memorizzati nella cache (`df.cache()`) prima di scriverli. Durante l&#39;esecuzione del codice nei blocchi appunti, l&#39;utilizzo di `df.cache()` prima di un&#39;azione come `fit()` può migliorare notevolmente le prestazioni del blocco appunti. L&#39;utilizzo `df.cache()` prima della scrittura di un dataset garantisce che le trasformazioni vengano eseguite una sola volta anziché più volte.

## [!DNL Docker Hub] limitare le restrizioni in Data Science Area di lavoro

A partire dal 20 novembre 2020, sono entrati in vigore i limiti di tariffa per l’uso anonimo e gratuito autenticato di Docker Hub. Gli utenti anonimi e gratuiti di [!DNL Docker Hub] sono limitati a 100 richieste pull di immagini contenitore ogni sei ore. Se sono state apportate queste modifiche, verrà visualizzato il seguente messaggio di errore: `ERROR: toomanyrequests: Too Many Requests.` o `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Attualmente, questo limite influisce sull’organizzazione solo se si sta tentando di creare 100 notebook su ricette entro il periodo di sei ore o se si utilizzano notebook basati su Spark in Data Science Workspace che sono spesso scalabili verso l’alto o verso il basso. Tuttavia, questo è improbabile, poiché il cluster su cui vengono eseguiti rimane attivo per due ore prima di essere disattivato. Questo riduce il numero di pull necessari quando il cluster è attivo. Se ricevi uno degli errori di cui sopra, dovrai aspettare che il limite di [!DNL Docker] venga reimpostato.

Per ulteriori informazioni sui limiti di tariffa [!DNL Docker Hub], consulta la [documentazione DockerHub](https://www.docker.com/increase-rate-limits). Una soluzione a questo problema è attualmente in fase di elaborazione ed è prevista in una versione successiva.
