---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: Guida alla risoluzione dei problemi per l'area di lavoro di analisi dati
topic: Troubleshooting
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---


# [!DNL Data Science Workspace] guida alla risoluzione dei problemi

Questo documento contiene le risposte alle domande frequenti sul  Adobe Experience Platform [!DNL Data Science Workspace]. Per domande e risoluzione dei problemi relativi alle [!DNL Platform] API in generale, consultate la guida alla risoluzione dei problemi delle API di [Adobe Experience Platform](../landing/troubleshooting.md).

## [!DNL JupyterLab] l&#39;ambiente non si sta caricando [!DNL Google Chrome]

>[!IMPORTANT]
>
>Questo problema è stato risolto ma potrebbe essere ancora presente nel browser Google Chrome 80.x. Verificare che il browser Chrome sia aggiornato.

Con la versione del [!DNL Google Chrome] browser 80.x, tutti i cookie di terze parti sono bloccati per impostazione predefinita. Questo criterio può impedire [!DNL JupyterLab] il caricamento entro  Adobe Experience Platform.

Per risolvere questo problema, attenersi alla procedura seguente:

Nel [!DNL Chrome] browser, andate in alto a destra e selezionate **Impostazioni** (in alternativa, potete copiare e incollare &quot;chrome://settings/&quot; nella barra degli indirizzi). Quindi, scorrete fino in fondo alla pagina e fate clic sul menu a discesa **Avanzate** .

![chrome avanzato](./images/faq/chrome-advanced.png)

Viene visualizzata la sezione *Privacy e sicurezza* . Quindi, fate clic sulle impostazioni **del** sito seguite da **cookie e dati** del sito.

![chrome avanzato](./images/faq/privacy-security.png)

![chrome avanzato](./images/faq/cookies.png)

Infine, scegliete &quot;Blocca cookie di terze parti&quot; su &quot;OFF&quot;.

![chrome avanzato](./images/faq/toggle-off.png)

>[!NOTE]
>
>In alternativa, puoi disattivare i cookie di terze parti e aggiungere [*.]ds.adobe.net all&#39;elenco consentiti .

Andate a &quot;chrome://flags/&quot; nella barra degli indirizzi. Cercate e disattivate il flag *&quot;SameSite by default cookies&quot;* utilizzando il menu a discesa a destra.

![disattiva flag samesite](./images/faq/samesite-flag.png)

Dopo il passaggio 2, viene richiesto di riavviare il browser. Dopo il riavvio, [!DNL Jupyterlab] dovrebbe essere accessibile.

## Perché non è possibile accedere a [!DNL JupyterLab] Safari?

Per impostazione predefinita, Safari disattiva i cookie di terze parti in Safari &lt; 12. Poiché l&#39;istanza della macchina [!DNL Jupyter] virtuale risiede in un dominio diverso da quello del relativo frame padre,  Adobe Experience Platform richiede attualmente l&#39;abilitazione dei cookie di terze parti. Abilita i cookie di terze parti o passa a un altro browser, ad esempio [!DNL Google Chrome].

Per Safari 12, è necessario sostituire l&#39;agente utente con &#39;[!DNL Chrome]&#39; o &#39;[!DNL Firefox]&#39;. Per cambiare agente utente, aprite il menu *Safari* e selezionate **Preferenze**. Viene visualizzata la finestra delle preferenze.

![Preferenze di Safari](./images/faq/preferences.png)

Nella finestra delle preferenze di Safari, selezionate **Avanzate**. Dal menu *Mostra sviluppo nella casella della barra* dei menu. Al termine di questo passaggio, potete chiudere la finestra delle preferenze.

![Safari avanzato](./images/faq/advanced.png)

Quindi, dalla barra di navigazione superiore, selezionate il menu **Sviluppo** . Dall’interno del menu a discesa *Sviluppo* , passa il puntatore del mouse sull’agente ** utente. È possibile selezionare la stringa agente **[!DNL Chrome]** o agente **[!DNL Firefox]** utente che si desidera utilizzare.

![Menu Sviluppo](./images/faq/user-agent.png)

## Perché viene visualizzato un messaggio &#39;403 Vietato&#39; quando si tenta di caricare o eliminare un file in [!DNL JupyterLab]?

Se il browser è abilitato con un software di blocco dell&#39;annuncio pubblicitario come [!DNL Ghostery] o [!DNL AdBlock] Plus, il dominio &quot;\*.adobe.net&quot; deve essere consentito in ciascun software di blocco dell&#39;annuncio per [!DNL JupyterLab] funzionare normalmente. Questo perché [!DNL JupyterLab] le macchine virtuali vengono eseguite su un dominio diverso da quello del [!DNL Experience Platform] dominio.

## Perché alcune parti del mio [!DNL Jupyter Notebook] aspetto sono frammentate o non vengono rappresentate come codice?

Ciò può accadere se la cella in questione viene accidentalmente modificata da &quot;Code&quot; a &quot;Markdown&quot;. Mentre una cella di codice è attiva, premendo la combinazione di tasti **ESC+M** il tipo di cella viene cambiato in Markdown. Il tipo di cella può essere modificato dall&#39;indicatore a discesa nella parte superiore del blocco appunti per le celle selezionate. Per modificare un tipo di cella in codice, iniziare selezionando la cella specificata da modificare. Fare clic sul menu a discesa che indica il tipo corrente della cella, quindi selezionare &quot;Codice&quot;.

![](./images/faq/code_type.png)

## Come si installano [!DNL Python] le librerie personalizzate?

Il [!DNL Python] kernel è preinstallato con molte librerie di machine learning popolari. Tuttavia, potete installare librerie personalizzate aggiuntive eseguendo il comando seguente all’interno di una cella di codice:

```shell
!pip install {LIBRARY_NAME}
```

Per un elenco completo delle [!DNL Python] librerie preinstallate, consultate la sezione [appendice della Guida](./jupyterlab/overview.md#supported-libraries)utente di JupyterLab.

## È possibile installare librerie PySpark personalizzate?

Purtroppo non è possibile installare librerie aggiuntive per il kernel PySpark. Tuttavia, potete contattare il rappresentante del servizio clienti Adobe per richiedere l&#39;installazione di librerie PySpark personalizzate.

Per un elenco delle librerie PySpark preinstallate, consultate la sezione [appendice della Guida](./jupyterlab/overview.md#supported-libraries)utente di JupyterLab.

## È possibile configurare le risorse del [!DNL Spark] cluster per il kernel [!DNL JupyterLab] PySpark [!DNL Spark] ?

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

Per ulteriori informazioni sulla configurazione delle risorse del [!DNL Spark] cluster, compreso l&#39;elenco completo delle proprietà configurabili, consulta la Guida [utente di](./jupyterlab/overview.md#kernels)JupyterLab.