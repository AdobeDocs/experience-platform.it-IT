---
title: Configurazione dei segreti nell’inoltro degli eventi
description: Scopri come configurare i segreti nell’interfaccia utente per l’autenticazione negli endpoint utilizzati nelle proprietà di inoltro degli eventi.
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: 592acdd45b1db5da95430b4e707cd9a2c18c1645
workflow-type: tm+mt
source-wordcount: '2426'
ht-degree: 3%

---

# Configurazione dei segreti nell’inoltro degli eventi

Nell’inoltro degli eventi, un segreto è una risorsa che rappresenta una credenziale di autenticazione per un altro sistema, consentendo lo scambio sicuro di dati. I segreti possono essere creati solo all’interno delle proprietà di inoltro degli eventi.

Sono attualmente supportati i seguenti tipi di segreto:

| Tipo di segreto | Descrizione |
| --- | --- |
| [!UICONTROL Google OAuth 2] | Contiene diversi attributi per supportare [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) specifica di autenticazione da utilizzare in [API di Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview) e [API Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview). Il sistema richiede le informazioni richieste, quindi gestisce il rinnovo di questi token per te in un intervallo specificato. |
| [!UICONTROL HTTP] | Contiene due attributi di stringa rispettivamente per nome utente e password. |
| [!UICONTROL [!DNL LinkedIn] OAuth 2] | Il sistema richiede le informazioni richieste, quindi gestisce il rinnovo di questi token per te in un intervallo specificato. |
| [!UICONTROL OAuth 2] | Contiene diversi attributi per supportare [tipo di concessione credenziali client](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) per [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) specifica di autenticazione. Il sistema richiede le informazioni richieste, quindi gestisce il rinnovo di questi token per te in un intervallo specificato. |
| [!UICONTROL OAuth 2 JWT] | Contiene diversi attributi per supportare il profilo JSON Web Token (JWT) per [Autorizzazione OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc7523#section-2.1) sovvenzioni. Il sistema richiede le informazioni richieste, quindi gestisce il rinnovo di questi token per te in un intervallo specificato. |
| [!UICONTROL Token] | Una singola stringa di caratteri che rappresenta un valore del token di autenticazione noto e compreso da entrambi i sistemi. |

{style="table-layout:auto"}

Questa guida fornisce una panoramica di alto livello sulla configurazione dei segreti per l’inoltro di un evento ([!UICONTROL Bordo]) nell’interfaccia di Experienci Platform o nell’interfaccia di Data Collection.

>[!NOTE]
>
>Per istruzioni dettagliate su come gestire i segreti nell’API di Reactor, incluso un esempio di JSON della struttura di un segreto, consulta [guida API per i segreti](../../api/guides/secrets.md).

## Prerequisiti

Questa guida presuppone che tu abbia già familiarità con le modalità di gestione delle risorse per i tag e l’inoltro di eventi nell’interfaccia utente, incluso come creare un elemento dati e una regola per l’inoltro di eventi. Consulta la guida su [gestione delle risorse](../managing-resources/overview.md) se hai bisogno di un’introduzione.

È inoltre necessario avere una buona conoscenza del flusso di pubblicazione per i tag e l’inoltro degli eventi, incluso come aggiungere risorse a una libreria e installare una build sul sito web per i test. Consulta la [panoramica sulla pubblicazione](../publishing/overview.md) per ulteriori dettagli.

## Creare un segreto {#create}

>[!CONTEXTUALHELP]
>id="platform_eventforwarding_secrets_environments"
>title="Ambienti per segreti"
>abstract="Affinché un segreto possa essere utilizzato dall’inoltro eventi, deve essere assegnato a un ambiente esistente. Se non sono stati creati ambienti per la proprietà di inoltro eventi, devi configurarli prima di continuare."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=it" text="Panoramica sugli ambienti"

Per creare un segreto, seleziona **[!UICONTROL Inoltro eventi]** nel menu di navigazione a sinistra, apri la proprietà di inoltro degli eventi in cui desideri aggiungere il segreto. Quindi, seleziona **[!UICONTROL Segreti]** nel menu di navigazione a sinistra, seguito da **[!UICONTROL Crea nuovo segreto]**.

![Crea nuovo segreto](../../images/ui/event-forwarding/secrets/create-new-secret.png)

La schermata successiva ti consente di configurare i dettagli del segreto. Affinché un segreto possa essere utilizzato dall’inoltro eventi, deve essere assegnato a un ambiente esistente. Se non hai creato ambienti per la proprietà di inoltro degli eventi, consulta la guida su [ambienti](../publishing/environments.md) per informazioni su come configurarli prima di continuare.

>[!NOTE]
>
>Se desideri comunque creare e salvare il segreto prima di aggiungerlo a un ambiente, disattiva il **[!UICONTROL Allega segreto agli ambienti]** prima di inserire le altre informazioni. Se desideri utilizzare il segreto, in un secondo momento dovrai assegnarlo a un ambiente.
>
>![Disabilita ambiente](../../images/ui/event-forwarding/secrets/env-disabled.png)

Sotto **[!UICONTROL Ambiente di destinazione]**, utilizza il menu a discesa per selezionare l’ambiente a cui assegnare il segreto. Sotto **[!UICONTROL Nome segreto]**, specifica un nome per il segreto nel contesto dell’ambiente. Questo nome deve essere univoco in tutti i segreti nella proprietà di inoltro degli eventi.

![Ambiente e nome](../../images/ui/event-forwarding/secrets/env-and-name.png)

Un segreto può essere assegnato a un solo ambiente alla volta, ma se lo desideri, puoi assegnare le stesse credenziali a più segreti in ambienti diversi. Seleziona **[!UICONTROL Aggiungi ambiente]** per aggiungere un&#39;altra riga all&#39;elenco.

![Aggiungi ambiente](../../images/ui/event-forwarding/secrets/add-env.png)

Per ogni ambiente aggiunto, devi fornire un altro nome univoco per il segreto associato. Se si esauriscono tutti gli ambienti disponibili, il **[!UICONTROL Aggiungi ambiente]** non sarà disponibile.

![Aggiungi ambiente non disponibile](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

Da qui, i passaggi per creare il segreto variano a seconda del tipo di segreto che stai creando. Per ulteriori informazioni, consulta le sottosezioni seguenti:

* [[!UICONTROL Token]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth 2]](#oauth2)
* [[!UICONTROL OAuth 2 JWT]](#oauth2jwt)
* [[!UICONTROL Google OAuth 2]](#google-oauth2)
* [[!UICONTROL [!DNL LinkedIn] OAuth 2]](#linkedin-oauth2)

### [!UICONTROL Token] {#token}

Per creare un segreto token, seleziona **[!UICONTROL Token]** dal **[!UICONTROL Tipo]** a discesa. In **[!UICONTROL Token]** campo visualizzato, fornire la stringa di credenziali riconosciuta dal sistema a cui si sta effettuando l&#39;autenticazione. Seleziona **[!UICONTROL Crea segreto]** per salvare il segreto.

![Segreto token](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

Per creare un segreto HTTP, seleziona **[!UICONTROL HTTP semplice]** dal **[!UICONTROL Tipo]** a discesa. Nei campi visualizzati di seguito, fornisci un nome utente e una password per le credenziali prima di selezionare **[!UICONTROL Crea segreto]** per salvare il segreto.

>[!NOTE]
>
>Al momento del salvataggio, le credenziali vengono codificate utilizzando [Schema di autenticazione HTTP &quot;Basic&quot;](https://www.rfc-editor.org/rfc/rfc7617.html).

![Segreto HTTP](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth 2] {#oauth2}

Per creare un segreto OAuth 2, seleziona **[!UICONTROL OAuth 2]** dal **[!UICONTROL Tipo]** a discesa. Fornisci il tuo [[!UICONTROL ID client] e [!UICONTROL Segreto client]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/), nonché [[!UICONTROL URL token]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) per l’integrazione OAuth. Il [!UICONTROL URL token] nell’interfaccia utente è una concatenazione tra l’host del server autorizzazioni e il percorso del token.

![Segreto OAuth 2](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

Sotto **[!UICONTROL Opzioni credenziali]**, è possibile fornire altre opzioni per le credenziali, ad esempio `scope` e `audience` sotto forma di coppie chiave-valore. Per aggiungere altre coppie chiave-valore, seleziona **[!UICONTROL Aggiungi un altro]**.

![Opzioni credenziali](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

Infine, puoi configurare il **[!UICONTROL Aggiorna offset]** valore per il segreto. Rappresenta il numero di secondi prima della scadenza del token durante i quali il sistema eseguirà un aggiornamento automatico. Il tempo equivalente in ore e minuti viene visualizzato a destra del campo e viene aggiornato automaticamente durante la digitazione.

![Aggiorna offset](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

Ad esempio, se l&#39;offset di aggiornamento è impostato sul valore predefinito `14400` (quattro ore) e il token di accesso ha `expires_in` valore di `86400` (24 ore), il sistema aggiornerà automaticamente il segreto in 20 ore.

>[!IMPORTANT]
>
>Un segreto OAuth richiede almeno quattro ore tra un aggiornamento e l’altro e deve anche essere valido per almeno otto ore. Questa limitazione ti consente di intervenire per un minimo di quattro ore in caso di problemi con il token generato.
>
>Ad esempio, se l&#39;offset è impostato su `28800` (otto ore) e il token di accesso ha `expires_in` di `36000` (dieci ore), lo scambio non sarebbe riuscito a causa della differenza risultante inferiore a quattro ore.

Al termine, seleziona **[!UICONTROL Crea segreto]** per salvare il segreto.

![Salva offset OAuth 2](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

### [!UICONTROL OAuth 2 JWT] {#oauth2jwt}

Per creare un segreto JWT OAuth 2, seleziona **[!UICONTROL OAuth 2 JWT]** dal **[!UICONTROL Tipo]** a discesa.

![Il [!UICONTROL Crea segreto] con il segreto JWT di OAuth 2 evidenziato nella [!UICONTROL Tipo] a discesa.](../../images/ui/event-forwarding/secrets/oauth-jwt-secret.png)

>[!NOTE]
>
>L&#39;unico [!UICONTROL Algoritmo] attualmente supportato per la firma del file JWT: RS256.

Fornisci il tuo [!UICONTROL Emittente], [!UICONTROL Oggetto], [!UICONTROL Pubblico], [!UICONTROL Attestazioni personalizzate], [!UICONTROL TTL], quindi seleziona la [!UICONTROL Algoritmo] dal menu a discesa. Quindi, immetti il [!UICONTROL ID chiave privata], nonché [[!UICONTROL URL token]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) per l’integrazione OAuth. Il [!UICONTROL URL token] non è un campo obbligatorio. Se viene fornito un valore, il JWT viene scambiato con un token di accesso. Il segreto verrà aggiornato in base al `expires_in` dalla risposta e dall&#39;attributo [!UICONTROL Aggiorna offset] valore. Se non viene fornito un valore, il segreto inviato al bordo è il JWT. Il JWT verrà aggiornato in base al [!UICONTROL TTL] e [!UICONTROL Aggiorna offset] valori.

![Il [!UICONTROL Crea segreto] con una selezione di campi di input evidenziati.](../../images/ui/event-forwarding/secrets/oauth-jwt-information.png)

Sotto **[!UICONTROL Opzioni credenziali]**, è possibile fornire altre opzioni per le credenziali, ad esempio `jwt_param` sotto forma di coppie chiave-valore. Per aggiungere altre coppie chiave-valore, seleziona **[!UICONTROL Aggiungi un altro]**.

![Il [!UICONTROL Crea segreto] scheda che evidenzia [!UICONTROL Opzioni credenziali] campi.](../../images/ui/event-forwarding/secrets/oauth-jwt-credential-options.png)

Infine, puoi configurare il **[!UICONTROL Aggiorna offset]** valore per il segreto. Rappresenta il numero di secondi prima della scadenza del token durante i quali il sistema eseguirà un aggiornamento automatico. Il tempo equivalente in ore e minuti viene visualizzato a destra del campo e viene aggiornato automaticamente durante la digitazione.

![Il [!UICONTROL Crea segreto] scheda che evidenzia [!UICONTROL Aggiorna offset] campo.](../../images/ui/event-forwarding/secrets/oauth-jwt-refresh-offset.png)

Ad esempio, se l&#39;offset di aggiornamento è impostato sul valore predefinito `1800` (30 minuti) e il token di accesso ha un `expires_in` valore di `3600` (un&#39;ora), il sistema aggiornerà automaticamente il segreto in un&#39;ora.

>[!IMPORTANT]
>
>Un segreto JWT OAuth 2 richiede almeno 30 minuti tra un aggiornamento e l’altro e deve anche essere valido per almeno un’ora. Questa limitazione ti consente di intervenire per un minimo di 30 minuti in caso di problemi con il token generato.
>
>Ad esempio, se l&#39;offset è impostato su `1800` (30 minuti) e il token di accesso ha un `expires_in` di `2700` (45 minuti), lo scambio non sarebbe riuscito perché la differenza risultante era inferiore a 30 minuti.

Al termine, seleziona **[!UICONTROL Crea segreto]** per salvare il segreto.

![Il [!UICONTROL Crea segreto] evidenziazione scheda [!UICONTROL Crea segreto]](../../images/ui/event-forwarding/secrets/oauth-jwt-create-secret.png)

### [!UICONTROL Google OAuth 2] {#google-oauth2}

Per creare un segreto Google OAuth 2, seleziona **[!UICONTROL Google OAuth 2]** dal **[!UICONTROL Tipo]** a discesa. Sotto **[!UICONTROL Ambiti]**, seleziona le API Google a cui desideri concedere l’accesso con questo segreto. Sono attualmente supportati i seguenti prodotti:

* [API di Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview)
* [API Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)

Al termine, seleziona **[!UICONTROL Crea segreto]**.

![Segreto Google OAuth 2](../../images/ui/event-forwarding/secrets/google-oauth.png)

Viene visualizzato un messaggio che informa che il segreto deve essere autorizzato manualmente tramite Google. Seleziona **[!UICONTROL Crea e autorizza]** per continuare.

![Popover di autorizzazione Google](../../images/ui/event-forwarding/secrets/google-authorization.png)

Viene visualizzata una finestra di dialogo che consente di immettere le credenziali per l’account Google. Segui le istruzioni per concedere l’accesso all’inoltro degli eventi ai tuoi dati nell’ambito selezionato. Una volta completato il processo di autorizzazione, viene creato il segreto.

>[!IMPORTANT]
>
>Se nell’organizzazione è impostato un criterio di riautenticazione per le applicazioni Google Cloud, i segreti creati non vengono aggiornati correttamente alla scadenza dell’autenticazione (tra 1 e 24 ore a seconda della configurazione del criterio).
>
>Per risolvere questo problema, accedi a Google Admin Console e passa a **[!DNL App access control]** in modo da poter contrassegnare l’app di inoltro eventi (Inoltro eventi di Adobe Real-Time CDP) come [!DNL Trusted]. Consulta la documentazione di Google su [impostazione della durata delle sessioni per i servizi Google Cloud](https://support.google.com/a/answer/9368756) per ulteriori informazioni.

### [!UICONTROL [!DNL LinkedIn] OAuth 2] {#linkedin-oauth2}

Per creare un [!DNL LinkedIn] Segreto OAuth 2, seleziona **[!UICONTROL [!DNL LinkedIn]OAuth 2]** dal **[!UICONTROL Tipo]** a discesa. Quindi, seleziona **[!UICONTROL Crea segreto]**.

![Il [!UICONTROL Crea segreto] scheda con [!UICONTROL Tipo] campo evidenziato.](../../images/ui/event-forwarding/secrets/linkedin-oauth.png)

Viene visualizzato un messaggio che informa che il segreto deve essere autorizzato manualmente tramite [!DNL LinkedIn]. Seleziona **[!UICONTROL Crea e autorizza segreto con[!DNL LinkedIn]]** per continuare.

![[!DNL LinkedIn] evidenziazione a comparsa autorizzazione [!UICONTROL Crea e autorizza segreto con [!DNL LinkedIn]].](../../images/ui/event-forwarding/secrets/linkedin-authorization.png)

Viene visualizzata una finestra di dialogo in cui viene richiesto di immettere [!DNL LinkedIn] credenziali. Segui le istruzioni per concedere l’accesso ai tuoi dati con inoltro eventi.

Una volta completato il processo di autorizzazione, si ritorna al **[!UICONTROL Segreti]** , in cui puoi visualizzare il segreto appena creato. Qui puoi vedere lo stato del segreto e la data di scadenza.

![Il [!UICONTROL Segreto] evidenziare il segreto appena creato.](../../images/ui/event-forwarding/secrets/linkedin-new-secret.png)

#### Autorizza nuovamente un [!UICONTROL [!DNL LinkedIn] OAuth 2] segreto

>IMPORTANTE
>
>È necessario autorizzare nuovamente utilizzando [!DNL LinkedIn] ogni 365 giorni. Se non esegui nuovamente l’autorizzazione in tempo utile, il segreto non verrà aggiornato e [!DNL LinkedIn] le richieste di conversione non avranno esito positivo.

Tre mesi prima del segreto che richiede la riautorizzazione, quando visiti una pagina della proprietà inizia a essere visualizzato un pop-up. Seleziona **[!UICONTROL Fai clic qui per accedere ai tuoi segreti]**.

![Il [!UICONTROL Panoramica delle proprietà] scheda che evidenzia la finestra a comparsa di ri-autorizzazione segreta.](../../images/ui/event-forwarding/secrets/linkedin-reauthorization-popup.png)

Sei reindirizzato al [!UICONTROL Segreti] scheda. I segreti elencati in questa pagina vengono filtrati in modo da mostrare solo i segreti che devono essere nuovamente autorizzati. Seleziona **[!UICONTROL Autenticazione necessaria]** per il segreto che devi autorizzare di nuovo.

![Il [!UICONTROL Segreto] evidenziazione scheda [!UICONTROL Autenticazione necessaria]per [!DNL LinkedIn] segreto.](../../images/ui/event-forwarding/secrets/linkedin-reauthorization.png)

Viene visualizzata una finestra di dialogo in cui viene richiesto di immettere [!DNL LinkedIn] credenziali. Segui le istruzioni per autorizzare nuovamente il segreto.

## Modifica un segreto

Dopo aver creato i segreti per una proprietà, puoi trovarli elencati in **[!UICONTROL Segreti]** Workspace. Per modificare i dettagli di un segreto esistente, selezionarne il nome dall&#39;elenco.

![Seleziona segreto da modificare](../../images/ui/event-forwarding/secrets/edit-secret.png)

La schermata successiva consente di modificare il nome e le credenziali per il segreto.

![Modifica segreto](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>Se il segreto è associato a un ambiente esistente, non è possibile riassegnarlo a un altro ambiente. Se desideri utilizzare le stesse credenziali in un ambiente diverso, devi [crea un nuovo segreto](#create) invece. L’unico modo per riassegnare l’ambiente da questa schermata è se non hai mai assegnato in precedenza il segreto a un ambiente o se hai eliminato l’ambiente a cui era associato il segreto.

### Riprovare uno scambio segreto

Puoi riprovare o aggiornare uno scambio segreto dalla schermata di modifica. Questo processo varia a seconda del tipo di segreto da modificare:

| Tipo di segreto | Ritenta protocollo |
| --- | --- |
| [!UICONTROL Token] | Seleziona **[!UICONTROL Segreto di Exchange]** per ritentare lo scambio segreto. Questo controllo è disponibile solo quando è presente un ambiente associato al segreto. |
| [!UICONTROL HTTP] | Se non è presente alcun ambiente associato al segreto, seleziona **[!UICONTROL Segreto di Exchange]** per scambiare le credenziali in base64. Se un ambiente è collegato, seleziona Seleziona **[!UICONTROL Segreto di Exchange e distribuzione]** per scambiare in base64 e distribuire il segreto. |
| [!UICONTROL OAuth 2] | Seleziona **[!UICONTROL Genera token]** per scambiare le credenziali e restituire un token di accesso dal provider di autenticazione. |

## Eliminare un segreto

Per eliminare un segreto esistente in  **[!UICONTROL Segreti]** , seleziona la casella di controllo accanto al nome prima di selezionare **[!UICONTROL Elimina]**.

![Elimina segreto](../../images/ui/event-forwarding/secrets/delete.png)

## Utilizzo dei segreti nell’inoltro degli eventi

Per utilizzare un segreto nell’inoltro degli eventi, devi innanzitutto creare un [elemento dati](../managing-resources/data-elements.md) che fa riferimento al segreto stesso. Dopo aver salvato l’elemento dati, puoi includerlo nell’inoltro degli eventi [regole](../managing-resources/rules.md) e aggiungi tali regole a una [libreria](../publishing/libraries.md), che a sua volta può essere implementato sui server di Adobe come [build](../publishing/builds.md).

Durante la creazione dell’elemento dati, seleziona la **[!UICONTROL Core]** , quindi seleziona **[!UICONTROL Segreto]** per il tipo di elemento dati. Il pannello a destra viene aggiornato e fornisce controlli a discesa per assegnare fino a tre segreti all’elemento dati: uno per [!UICONTROL Sviluppo], [!UICONTROL Staging], e [!UICONTROL Produzione] rispettivamente.

![Elemento dati](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>Solo i segreti allegati agli ambienti di sviluppo, staging e produzione vengono visualizzati per i rispettivi elenchi a discesa.

Assegnando più segreti a un singolo elemento dati e includendolo in una regola, il valore dell’elemento dati può cambiare a seconda di dove si trova la libreria contenitore in [flusso di pubblicazione](../publishing/publishing-flow.md).

![Elemento dati con più segreti](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>Durante la creazione dell’elemento dati, è necessario assegnare un ambiente di sviluppo. Non sono necessari segreti per gli ambienti di staging e produzione, ma le build che tentano di passare a tali ambienti avranno esito negativo se i loro elementi di dati di tipo segreto non hanno un segreto selezionato per l’ambiente in questione.

## Passaggi successivi

Questa guida illustra come gestire i segreti nell’interfaccia utente di. Per informazioni su come interagire con i segreti utilizzando l’API di Reactor, consulta [guida dell’endpoint &quot;secrets&quot;](../../api/endpoints/secrets.md).
