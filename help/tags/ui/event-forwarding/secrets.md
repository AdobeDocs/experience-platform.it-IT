---
title: Configurazione dei segreti nell’inoltro degli eventi
description: Scopri come configurare i segreti nell’interfaccia utente per l’autenticazione agli endpoint utilizzati nelle proprietà di inoltro degli eventi.
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: c314cba6b822e12aa0367e1377ceb4f6c9d07ac2
workflow-type: tm+mt
source-wordcount: '1766'
ht-degree: 1%

---

# Configurazione dei segreti nell’inoltro degli eventi

In caso di inoltro, un segreto è una risorsa che rappresenta una credenziale di autenticazione per un altro sistema, che consente lo scambio sicuro di dati. I segreti possono essere creati solo all&#39;interno delle proprietà di inoltro degli eventi.

Al momento sono disponibili tre tipi di segreto supportati:

| Tipo di segreto | Descrizione |
| --- | --- |
| [!UICONTROL Token] | Una singola stringa di caratteri che rappresenta un valore del token di autenticazione noto e compreso da entrambi i sistemi. |
| [!UICONTROL HTTP] | Contiene rispettivamente due attributi di stringa per un nome utente e una password. |
| [!UICONTROL OAuth 2] | Contiene diversi attributi per supportare il [tipo di concessione delle credenziali client](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) per [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) specifiche di autenticazione. Il sistema richiede le informazioni richieste, quindi gestisce il rinnovo di questi token per voi in un intervallo specificato. |
| [!UICONTROL OAuth 2 di Google] | Contiene diversi attributi per supportare il [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) specifiche di autenticazione per l’utilizzo in [API Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview) e [API Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview). Il sistema richiede le informazioni richieste, quindi gestisce il rinnovo di questi token per voi in un intervallo specificato. |

{style=&quot;table-layout:auto&quot;}

Questa guida fornisce una panoramica di alto livello su come configurare i segreti per un inoltro di eventi ([!UICONTROL Bordo]) nell’interfaccia utente Experience Platform o nell’interfaccia utente di raccolta dati.

>[!NOTE]
>
>Per informazioni dettagliate su come gestire i segreti nell’API del reattore, incluso l’esempio JSON della struttura di un segreto, consulta la sezione [guida all’API per segreti](../../api/guides/secrets.md).

## Prerequisiti

Questa guida presuppone che tu abbia già familiarità con le modalità di gestione delle risorse per i tag e l’inoltro di eventi nell’interfaccia utente, inclusa la modalità di creazione di un elemento dati e una regola di inoltro eventi. Consulta la guida su [gestione delle risorse](../managing-resources/overview.md) se hai bisogno di un’introduzione.

È inoltre necessario avere una conoscenza approfondita del flusso di pubblicazione per tag e inoltro eventi, tra cui come aggiungere risorse a una libreria e installare una build sul sito web per il test. Consulta la sezione [panoramica sulla pubblicazione](../publishing/overview.md) per ulteriori dettagli.

## Creare un segreto {#create}

>[!CONTEXTUALHELP]
>id="platform_eventforwarding_secrets_environments"
>title="Ambienti per segreti"
>abstract="Affinché un segreto possa essere utilizzato dall&#39;inoltro eventi, deve essere assegnato a un ambiente esistente. Se non sono stati creati ambienti per la proprietà di inoltro eventi, è necessario configurarli prima di continuare."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html" text="Panoramica sugli ambienti"

Per creare un segreto, seleziona **[!UICONTROL Inoltro eventi]** nel menu di navigazione a sinistra, apri la proprietà di inoltro eventi in cui desideri aggiungere il segreto. Quindi, seleziona **[!UICONTROL Segreti]** nella navigazione a sinistra, seguita da **[!UICONTROL Crea nuovo segreto]**.

![Crea nuovo segreto](../../images/ui/event-forwarding/secrets/create-new-secret.png)

La schermata successiva ti consente di configurare i dettagli del segreto. Affinché un segreto possa essere utilizzato dall&#39;inoltro eventi, deve essere assegnato a un ambiente esistente. Se non sono stati creati ambienti per la proprietà di inoltro eventi, consulta la guida in [ambienti](../publishing/environments.md) per informazioni su come configurarli prima di continuare.

>[!NOTE]
>
>Se desideri comunque creare e salvare il segreto prima di aggiungerlo a un ambiente, disattiva la **[!UICONTROL Allega segreto agli ambienti]** prima di inserire il resto delle informazioni. Se desideri utilizzare il segreto, devi assegnarlo a un ambiente in un secondo momento.
>
>![Disabilita ambiente](../../images/ui/event-forwarding/secrets/env-disabled.png)

Sotto **[!UICONTROL Ambiente di destinazione]**, utilizza il menu a discesa per selezionare l’ambiente a cui assegnare il segreto. Sotto **[!UICONTROL Nome segreto]**, specifica un nome per il segreto nel contesto dell&#39;ambiente. Questo nome deve essere univoco in tutti i segreti della proprietà di inoltro dell&#39;evento.

![Ambiente e nome](../../images/ui/event-forwarding/secrets/env-and-name.png)

Un segreto può essere assegnato a un solo ambiente alla volta, ma se lo desideri puoi assegnare le stesse credenziali a più segreti in ambienti diversi. Seleziona **[!UICONTROL Aggiungi ambiente]** per aggiungere un’altra riga all’elenco.

![Aggiungi ambiente](../../images/ui/event-forwarding/secrets/add-env.png)

Per ogni ambiente aggiunto, devi fornire un altro nome univoco per il segreto associato. Se scarichi tutti gli ambienti disponibili, la **[!UICONTROL Aggiungi ambiente]** il pulsante non sarà disponibile.

![Aggiungi ambiente non disponibile](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

Da qui, i passaggi per creare il segreto variano a seconda del tipo di segreto che stai creando. Per ulteriori informazioni, consulta le sottosezioni seguenti:

* [[!UICONTROL Token]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth 2]](#oauth2)
* [[!UICONTROL OAuth 2 di Google]](#google-oauth2)

### [!UICONTROL Token] {#token}

Per creare un segreto token, seleziona **[!UICONTROL Token]** dal **[!UICONTROL Tipo]** a discesa. In **[!UICONTROL Token]** specificare la stringa di credenziale riconosciuta dal sistema a cui si sta eseguendo l&#39;autenticazione. Seleziona **[!UICONTROL Crea segreto]** per salvare il segreto.

![Segreto token](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

Per creare un segreto HTTP, seleziona **[!UICONTROL HTTP semplice]** dal **[!UICONTROL Tipo]** a discesa. Nei campi visualizzati di seguito, fornisci un nome utente e una password per la credenziale prima di selezionare **[!UICONTROL Crea segreto]** per salvare il segreto.

>[!NOTE]
>
>Al momento del salvataggio, la credenziale viene codificata utilizzando [Schema di autenticazione HTTP &quot;Basic&quot;](https://www.rfc-editor.org/rfc/rfc7617.html).

![segreto HTTP](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth 2] {#oauth2}

Per creare un segreto OAuth 2, seleziona **[!UICONTROL OAuth 2]** dal **[!UICONTROL Tipo]** a discesa. Nei campi visualizzati di seguito, fornisci [[!UICONTROL ID client] e [!UICONTROL Segreto client]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/), nonché [[!UICONTROL URL token]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) per l’integrazione con OAuth. La [!UICONTROL URL token] nell’interfaccia utente è una concatenazione tra l’host del server di autorizzazione e il percorso del token.

![Segreto OAuth 2](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

Sotto **[!UICONTROL Opzioni credenziali]**, è possibile fornire altre opzioni di credenziale, ad esempio `scope` e `audience` sotto forma di coppie chiave-valore. Per aggiungere altre coppie chiave-valore, seleziona **[!UICONTROL Aggiungi un altro]**.

![Opzioni credenziali](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

Infine, puoi configurare il **[!UICONTROL Aggiorna offset]** valore del segreto. Rappresenta il numero di secondi prima della scadenza del token per cui il sistema eseguirà un aggiornamento automatico. L’ora equivalente in ore e minuti viene visualizzata a destra del campo e si aggiorna automaticamente durante la digitazione.

![Aggiorna offset](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

Ad esempio, se l&#39;offset di aggiornamento è impostato sul valore predefinito di `14400` (quattro ore) e il token di accesso ha un `expires_in` valore `86400` (24 ore), il sistema aggiornerà automaticamente il segreto in 20 ore.

>[!IMPORTANT]
>
>Un segreto OAuth richiede almeno quattro ore di aggiornamento e deve essere valido anche per almeno otto ore. Questa limitazione ti dà un minimo di quattro ore per intervenire in caso di problemi con il token generato.
>
>Ad esempio, se l&#39;offset è impostato su `28800` (otto ore) e il token di accesso ha un `expires_in` di `36000` (10 ore), lo scambio avrebbe avuto esito negativo a causa della differenza risultante inferiore a quattro ore.

Al termine, seleziona **[!UICONTROL Crea segreto]** per salvare il segreto.

![Salva offset OAuth 2](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

### [!UICONTROL OAuth 2 di Google] {#google-oauth2}

Per creare un segreto OAuth 2 di Google, seleziona **[!UICONTROL OAuth 2 di Google]** dal **[!UICONTROL Tipo]** a discesa. Sotto **[!UICONTROL Ambiti]**, seleziona le API Google a cui desideri utilizzare questo segreto per concedere l’accesso. Sono attualmente supportati i seguenti prodotti:

* [API Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview)
* [API Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)

Al termine, seleziona **[!UICONTROL Crea segreto]**.

![Segreto OAuth 2 di Google](../../images/ui/event-forwarding/secrets/google-oauth.png)

Un popopover ti informa che il segreto deve essere autorizzato manualmente tramite Google. Seleziona **[!UICONTROL Crea e autorizza]** per continuare.

![Pover di autorizzazione Google](../../images/ui/event-forwarding/secrets/google-authorization.png)

Viene visualizzata una finestra di dialogo che consente di immettere le credenziali per l’account Google. Segui le istruzioni per concedere l’accesso all’inoltro eventi ai tuoi dati nell’ambito selezionato. Una volta completato il processo di autorizzazione, viene creato il segreto.

>[!IMPORTANT]
>
>Se nell’organizzazione è impostato un criterio di riautenticazione per le applicazioni Google Cloud, i segreti creati non verranno aggiornati correttamente dopo la scadenza dell’autenticazione (tra 1 e 24 ore a seconda della configurazione del criterio).
>
>Per risolvere il problema, accedi a Google Admin Console e passa alla **[!DNL App access control]** in modo da poter contrassegnare l’app di inoltro eventi (Adobe Real-Time CDP Event Forwarding) come [!DNL Trusted]. Consulta la documentazione Google su [impostazione delle lunghezze di sessione per i servizi Google Cloud](https://support.google.com/a/answer/9368756?hl=it) per ulteriori informazioni.

## Modificare un segreto

Dopo aver creato segreti per una proprietà, puoi trovarli elencati nella sezione **[!UICONTROL Segreti]** workspace. Per modificare i dettagli di un segreto esistente, selezionane il nome dall’elenco.

![Selezionare il segreto da modificare](../../images/ui/event-forwarding/secrets/edit-secret.png)

La schermata successiva ti consente di modificare il nome e le credenziali del segreto.

![Modifica segreto](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>Se il segreto è associato a un ambiente esistente, non è possibile riassegnare il segreto a un altro ambiente. Se desideri utilizzare le stesse credenziali in un ambiente diverso, devi [crea un nuovo segreto](#create) invece. L’unico modo per riassegnare l’ambiente da questa schermata è se non hai mai assegnato il segreto a un ambiente in precedenza o se hai eliminato l’ambiente a cui era associato il segreto.

### Ritentare uno scambio segreto

È possibile riprovare o aggiornare uno scambio segreto dalla schermata di modifica. Questo processo varia a seconda del tipo di segreto in corso di modifica:

| Tipo di segreto | Nuovo protocollo |
| --- | --- |
| [!UICONTROL Token] | Seleziona **[!UICONTROL Segreto Exchange]** per riprovare lo scambio segreto. Questo controllo è disponibile solo quando è presente un ambiente collegato al segreto. |
| [!UICONTROL HTTP] | Se non è presente alcun ambiente collegato al segreto, seleziona **[!UICONTROL Segreto Exchange]** per scambiare le credenziali con base64. Se un ambiente è collegato, seleziona Seleziona **[!UICONTROL Exchange e Distribuzione di segreti]** per scambiare con base64 e distribuire il segreto. |
| [!UICONTROL OAuth 2] | Seleziona **[!UICONTROL Genera token]** per scambiare le credenziali e restituire un token di accesso dal provider di autenticazione. |

## Elimina un segreto

Per eliminare un segreto esistente nel  **[!UICONTROL Segreti]** area di lavoro, seleziona la casella di controllo accanto al nome prima di selezionare **[!UICONTROL Elimina]**.

![Elimina segreto](../../images/ui/event-forwarding/secrets/delete.png)

## Utilizzo dei segreti nell’inoltro degli eventi

Per utilizzare un segreto nell&#39;inoltro degli eventi, devi prima creare un [elemento dati](../managing-resources/data-elements.md) che fa riferimento al segreto stesso. Dopo aver salvato l&#39;elemento dati, puoi includerlo nell&#39;inoltro degli eventi [regole](../managing-resources/rules.md) e aggiungi tali regole a un [libreria](../publishing/libraries.md), che a sua volta può essere distribuito ai server di Adobe come [build](../publishing/builds.md).

Quando crei l’elemento dati, seleziona la **[!UICONTROL Core]** estensione , quindi seleziona **[!UICONTROL Segreto]** per il tipo di elemento dati. Il pannello a destra aggiorna e fornisce controlli a discesa per assegnare fino a tre segreti all’elemento dati: uno per [!UICONTROL Sviluppo], [!UICONTROL Staging]e [!UICONTROL Produzione] rispettivamente.

![Elemento dati](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>Per i rispettivi elenchi a discesa vengono visualizzati solo i segreti associati agli ambienti di sviluppo, staging e produzione.

Assegnando più segreti a un singolo elemento dati e includendolo in una regola, puoi modificare il valore dell&#39;elemento dati a seconda di dove si trova la libreria contenitore nel [flusso di pubblicazione](../publishing/publishing-flow.md).

![Elemento dati con più segreti](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>Quando crei l’elemento dati, devi assegnare un ambiente di sviluppo. I segreti per gli ambienti di staging e produzione non sono necessari, ma le build che tentano di eseguire la transizione a tali ambienti avranno esito negativo se gli elementi dati di tipo segreto non dispongono di un segreto selezionato per l’ambiente in questione.

## Passaggi successivi

Questa guida illustra come gestire i segreti nell’interfaccia utente di . Per informazioni su come interagire con i segreti utilizzando l’API di Reactor, consulta la [guida all’endpoint segreti](../../api/endpoints/secrets.md).
