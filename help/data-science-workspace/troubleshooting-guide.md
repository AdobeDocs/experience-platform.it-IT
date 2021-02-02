---
keywords: ', Experience Platform;risoluzione dei problemi;Data Science Workspace;argomenti più comuni'
solution: Experience Platform
title: Guida alla risoluzione dei problemi per l'area di lavoro di analisi dati
topic: Troubleshooting
description: Questo documento contiene le risposte alle domande frequenti su Adobe Experience Platform Data Science Workspace.
translation-type: tm+mt
source-git-commit: 045ad186efac59317635439a05b9d24e703c9859
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 0%

---


# [!DNL Data Science Workspace] guida alla risoluzione dei problemi

Questo documento contiene le risposte alle domande frequenti su Adobe Experience Platform [!DNL Data Science Workspace]. Per domande e risoluzione dei problemi relativi alle [!DNL Platform] API in generale, consultare la [Guida alla risoluzione dei problemi delle API di Adobe Experience Platform](../landing/troubleshooting.md).

## [!DNL JupyterLab] l&#39;ambiente non si sta caricando  [!DNL Google Chrome]

>[!IMPORTANT]
>
>Questo problema è stato risolto ma potrebbe essere ancora presente nel browser Google Chrome 80.x. Verificare che il browser Chrome sia aggiornato.

Con la versione del browser [!DNL Google Chrome] 80.x, tutti i cookie di terze parti sono bloccati per impostazione predefinita. Questo criterio può impedire il caricamento di [!DNL JupyterLab] in Adobe Experience Platform.

Per risolvere questo problema, attenersi alla procedura seguente:

Nel browser [!DNL Chrome], andate in alto a destra e selezionate **Impostazioni** (in alternativa, potete copiare e incollare &quot;chrome://settings/&quot; nella barra degli indirizzi). Quindi, scorrete fino in fondo alla pagina e fate clic sul menu a discesa **Avanzate**.

![chrome avanzato](./images/faq/chrome-advanced.png)

Viene visualizzata la sezione **Privacy e sicurezza**. Fare clic su **Impostazioni del sito** seguito da **Cookie e dati del sito**.

![chrome avanzato](./images/faq/privacy-security.png)

![chrome avanzato](./images/faq/cookies.png)

Infine, scegliete &quot;Blocca cookie di terze parti&quot; su &quot;OFF&quot;.

![chrome avanzato](./images/faq/toggle-off.png)

>[!NOTE]
>
>In alternativa, puoi disattivare i cookie di terze parti e aggiungere [*.]ds.adobe.net all&#39;elenco consentiti .

Andate a &quot;chrome://flags/&quot; nella barra degli indirizzi. Cercare e disabilitare il flag denominato *&quot;SameSite by default cookies&quot;* utilizzando il menu a discesa a destra.

![disattiva flag samesite](./images/faq/samesite-flag.png)

Dopo il passaggio 2, viene richiesto di riavviare il browser. Dopo il riavvio, [!DNL Jupyterlab] deve essere accessibile.

## Perché non è possibile accedere a [!DNL JupyterLab] in Safari?

Per impostazione predefinita, Safari disattiva i cookie di terze parti in Safari &lt; 12. Poiché l&#39;istanza della macchina virtuale [!DNL Jupyter] risiede in un dominio diverso da quello del relativo frame principale, Adobe Experience Platform richiede attualmente l&#39;abilitazione dei cookie di terze parti. Abilitare i cookie di terze parti o passare a un altro browser, ad esempio [!DNL Google Chrome].

Per Safari 12, è necessario sostituire l&#39;agente utente con &#39;[!DNL Chrome]&#39; o &#39;[!DNL Firefox]&#39;. Per cambiare agente utente, aprite il menu *Safari* e selezionate **Preferenze**. Viene visualizzata la finestra delle preferenze.

![Preferenze di Safari](./images/faq/preferences.png)

Nella finestra delle preferenze di Safari, selezionare **Avanzate**. Quindi, selezionate il menu *Mostra sviluppo nella barra dei menu*. Al termine di questo passaggio, potete chiudere la finestra delle preferenze.

![Safari avanzato](./images/faq/advanced.png)

Quindi, dalla barra di navigazione superiore, selezionate il menu **Sviluppo**. Dall&#39;interno del menu a discesa **Sviluppa**, passare il puntatore del mouse sull&#39; **Agente utente**. È possibile selezionare la stringa **[!DNL Chrome]** o **[!DNL Firefox]** Agente utente che si desidera utilizzare.

![Menu Sviluppo](./images/faq/user-agent.png)

## Perché viene visualizzato un messaggio &#39;403 Vietato&#39; quando si tenta di caricare o eliminare un file in [!DNL JupyterLab]?

Se il browser è abilitato con un software di blocco dell&#39;annuncio pubblicitario, ad esempio [!DNL Ghostery] o [!DNL AdBlock] Plus, il dominio &quot;\*.adobe.net&quot; deve essere consentito in ogni software di blocco dell&#39;annuncio per [!DNL JupyterLab] funzionare normalmente. Questo perché le [!DNL JupyterLab] macchine virtuali vengono eseguite su un dominio diverso da quello del [!DNL Experience Platform].

## Perché alcune parti del mio [!DNL Jupyter Notebook] sembrano frammentate o non vengono rappresentate come codice?

Ciò può accadere se la cella in questione viene accidentalmente modificata da &quot;Code&quot; a &quot;Markdown&quot;. Mentre una cella di codice è attiva, premendo la combinazione di tasti **ESC+M** il tipo di cella viene cambiato in Markdown. Il tipo di cella può essere modificato dall&#39;indicatore a discesa nella parte superiore del blocco appunti per le celle selezionate. Per modificare un tipo di cella in codice, iniziare selezionando la cella specificata da modificare. Fare clic sul menu a discesa che indica il tipo corrente della cella, quindi selezionare &quot;Codice&quot;.

![](./images/faq/code_type.png)

## Come si installano le librerie [!DNL Python] personalizzate?

Il kernel [!DNL Python] è preinstallato con molte librerie di machine learning popolari. Tuttavia, potete installare librerie personalizzate aggiuntive eseguendo il comando seguente all’interno di una cella di codice:

```shell
!pip install {LIBRARY_NAME}
```

Per un elenco completo delle [!DNL Python] librerie preinstallate, consultate la sezione [appendice della Guida utente di JupyterLab](./jupyterlab/overview.md#supported-libraries).

## È possibile installare librerie PySpark personalizzate?

Purtroppo non è possibile installare librerie aggiuntive per il kernel PySpark. Tuttavia, potete contattare il rappresentante del servizio clienti  Adobe per ottenere librerie PySpark personalizzate installate.

Per un elenco delle librerie PySpark preinstallate, consultate la sezione [appendice della Guida utente di JupyterLab](./jupyterlab/overview.md#supported-libraries).

## È possibile configurare le risorse del cluster [!DNL Spark] per il kernel [!DNL JupyterLab] [!DNL Spark] o PySpark?

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

Per ulteriori informazioni sulla [!DNL Spark] configurazione delle risorse del cluster, compreso l&#39;elenco completo delle proprietà configurabili, vedere la [Guida utente di JupyterLab](./jupyterlab/overview.md#kernels).

## Perché si verifica un errore durante l&#39;esecuzione di determinate attività per set di dati più grandi?

Se si riceve un errore per un motivo come `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Questo indica in genere che il driver o l&#39;esecutore non dispongono di memoria sufficiente. Per ulteriori informazioni sui limiti dei dati e su come eseguire attività su set di dati di grandi dimensioni, consultare la documentazione relativa ai notebook JupyterLab [data access](./jupyterlab/access-notebook-data.md). In genere questo errore può essere risolto modificando il `mode` da `interactive` a `batch`.

## [!DNL Docker Hub] limitazioni in Data Science Workspace

A partire dal 20 novembre 2020, i limiti di tariffa per l&#39;uso anonimo e gratuito autenticato di Docker Hub sono entrati in vigore. Gli utenti anonimi e gratuiti [!DNL Docker Hub] sono limitati a 100 richieste di immagini contenitore ogni sei ore. Se queste modifiche interessano, riceverai questo messaggio di errore: `ERROR: toomanyrequests: Too Many Requests.` o `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Al momento, questo limite interesserà la tua organizzazione solo se stai tentando di creare 100 notebook in Ricette entro i sei orari o se stai utilizzando notebook basati su Spark in Data Science Workspace che vengono spesso ridimensionati. Tuttavia, ciò è improbabile, dal momento che il cluster su cui viene eseguito rimane attivo per due ore prima di essere disattivato. Questo riduce il numero di pull necessari quando il cluster è attivo. Se ricevi uno degli errori di cui sopra, dovrai aspettare che il limite [!DNL Docker] venga reimpostato.

Per ulteriori informazioni sui limiti di tariffa [!DNL Docker Hub], consultare la [Documentazione DockerHub](https://www.docker.com/increase-rate-limits). Una soluzione a questo problema è in fase di elaborazione e prevista in una versione successiva.