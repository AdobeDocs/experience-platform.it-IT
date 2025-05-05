---
title: Configurazione dei segreti nell'inoltro eventi
description: Scopri come configurare i segreti nel interfaccia per l'autenticazione agli endpoint utilizzati nelle proprietà di inoltro eventi.
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: 592acdd45b1db5da95430b4e707cd9a2c18c1645
workflow-type: tm+mt
source-wordcount: '2426'
ht-degree: 3%

---

# Configurazione dei segreti nell&#39;inoltro degli eventi

Nell&#39;inoltro di eventi, un segreto è una risorsa che rappresenta una credenziale di autenticazione per un altro sistema, consentendo lo scambio sicuro di dati. I segreti possono essere creati solo all&#39;interno delle proprietà di inoltro degli eventi.

I seguenti tipi di segreti sono attualmente supportati:

| Tipo segreto | Descrizione |
| --- | --- |
| [!UICONTROL Google OAuth 2] | Contiene diversi attributi a supporto delle [specifiche di autenticazione OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) da utilizzare nell&#39;API[&#128279;](https://developers.google.com/google-ads/api/docs/oauth/overview) Google Ads e nell&#39;API [&#128279;](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)Pub/Sub. Il sistema richiede le informazioni richieste, quindi gestisce il rinnovo di questi token per te in un intervallo specificato. |
| [!UICONTROL HTTP] | Contiene due attributi stringa rispettivamente per un nome utente e un password. |
| [!UICONTROL [!DNL LinkedIn] OAuth 2] | Il sistema richiede le informazioni richieste, quindi gestisce il rinnovo di questi token per te in un intervallo specificato. |
| [!UICONTROL OAuth 2] | Contiene diversi attributi per supportare il tipo[&#128279;](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) di concessione delle credenziali client per le specifiche di [autenticazione OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749). Il sistema richiede le informazioni richieste, quindi gestisce il rinnovo di questi token per te in un intervallo specificato. |
| [!UICONTROL OAuth 2 JWT] | Contiene diversi attributi per supportare il profilo JWT (Web Token) per [le concessioni di autorizzazione](https://datatracker.ietf.org/doc/html/rfc7523#section-2.1) OAuth 2.0. Il sistema richiede le informazioni richieste, quindi gestisce il rinnovo di questi token per te in un intervallo specificato. |
| [!UICONTROL Token] | Una singola stringa di caratteri che rappresenta un valore del token di autenticazione conosciuto e compreso da entrambi i sistemi. |

{style="table-layout:auto"}

Questa guida fornisce una panoramica generale su come configurare i segreti per una proprietà di inoltro eventi ([!UICONTROL Edge]) nel interfaccia interfaccia Experience Platform o di raccolta dati.

>[!NOTE]
>
>Per indicazioni dettagliate su come gestire segreti nell&#39;API di Reactor, incluso l&#39;esempio [JSON della struttura di un segreto, fare riferimento alla guida](../../api/guides/secrets.md) API dei segreti.

## Prerequisiti

In questa guida si presuppone che l&#39;utente abbia già familiarità con le modalità di gestire delle risorse per i tag e l&#39;inoltro degli eventi nella interfaccia, inclusa la creazione di un elemento dati e di un regola di inoltro degli eventi. Per presentazioni, consulta la guida alla [gestione delle risorse](../managing-resources/overview.md) .

È inoltre necessario avere una conoscenza pratica del flusso di pubblicazione per i tag e l&#39;inoltro degli eventi, incluso come aggiungere risorse a un libreria e installare un versione nel sito Web per il test. Per ulteriori informazioni, consulta la panoramica[&#128279;](../publishing/overview.md) sulla pubblicazione.

## Creare un segreto {#create}

>[!CONTEXTUALHELP]
>id="platform_eventforwarding_secrets_environments"
>title="Ambienti per segreti"
>abstract="Affinché un segreto possa essere utilizzato dall’inoltro eventi, deve essere assegnato a un ambiente esistente. Se non sono stati creati ambienti per la proprietà di inoltro eventi, devi configurarli prima di continuare."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=it" text="Panoramica sugli ambienti"

Per creare un segreto, seleziona **[!UICONTROL Inoltro]** eventi nel navigazione sinistro, quindi apri la proprietà di inoltro dell&#39;evento sotto la quale desideri aggiungere il segreto. Successivo, seleziona **[!UICONTROL Segreti]** nella navigazione sinistra, quindi Crea **[!UICONTROL Nuovo Segreto]**.

![Crea nuovo segreto](../../images/ui/event-forwarding/secrets/create-new-secret.png)

La schermata successiva consente di configurare i dettagli del segreto. Affinché un segreto possa essere utilizzato dall’inoltro eventi, deve essere assegnato a un ambiente esistente. Se non hai creato ambienti per la proprietà di inoltro eventi, consulta la guida sugli [ambienti](../publishing/environments.md) per indicazioni su come configurarli prima di continuare.

>[!NOTE]
>
>Se si desidera comunque creare e salvare il segreto prima di aggiungerlo a un ambiente, disabilitare l&#39;interruttore **[!UICONTROL Allega segreto agli ambienti]** prima di compilare il resto delle informazioni. Si noti che sarà necessario assegnarlo a un ambiente in un secondo momento se si desidera utilizzare il segreto.
>
>![Disabilita ambiente](../../images/ui/event-forwarding/secrets/env-disabled.png)

In **[!UICONTROL Ambiente]** Target, utilizza il menu a discesa per selezionare l&#39;ambiente a cui assegnare il segreto. In **[!UICONTROL Nome]** segreto specificare un nome per il segreto nel contesto dell&#39;ambiente. Questo nome deve essere univoco in tutti i segreti inclusi nella proprietà di inoltro eventi.

![Ambiente e nome](../../images/ui/event-forwarding/secrets/env-and-name.png)

Un segreto può essere assegnato a un solo ambiente alla volta, ma è possibile assegnare le stesse credenziali a più segreti in ambienti diversi, se lo si desidera. Selezionare **[!UICONTROL Aggiungi ambiente]** per aggiungere un&#39;altra riga all&#39;elenco.

![Aggiungi ambiente](../../images/ui/event-forwarding/secrets/add-env.png)

Per ogni ambiente aggiunto, è necessario fornire un altro nome univoco per il segreto associato. Se esaurisci tutti gli ambienti disponibili, la **[!UICONTROL pulsante Aggiungi ambiente]** non sarà disponibile.

![Aggiungi ambiente non disponibile](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

Da qui, i passaggi per creare il segreto differiscono a seconda del tipo di segreto che si sta creando. Per informazioni dettagliate, fare riferimento alle sottosezioni seguenti:

* [[!UICONTROL Token]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth 2]](#oauth2)
* [[!UICONTROL OAuth 2 JWT]](#oauth2jwt)
* [[!UICONTROL Google OAuth 2]](#google-oauth2)
* [[!UICONTROL OAuth [!DNL LinkedIn] 2]](#linkedin-oauth2)

### [!UICONTROL Token] {#token}

Per creare un segreto token, selezionare **[!UICONTROL Token]** dall&#39;elenco **[!UICONTROL a discesa Tipo]** . **[!UICONTROL Nel campo Token]** visualizzato, specificare la stringa delle credenziali riconosciuta dal sistema in cui si esegue l&#39;autenticazione. Selezionare **[!UICONTROL Crea segreto]** per salvare il segreto.

![Token segreto](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

Per creare un segreto HTTP, selezionare **[!UICONTROL HTTP]** semplice dall&#39;elenco a **[!UICONTROL discesa Tipo]** . Nei campi riportati di seguito, fornisci un nome utente e un password per la credenziale prima di selezionare **[!UICONTROL Crea Segreto]** per salvare il segreto.

>[!NOTE]
>
>Dopo il salvataggio, la credenziale viene codificata utilizzando lo [schema](https://www.rfc-editor.org/rfc/rfc7617.html) di autenticazione HTTP &quot;Basic&quot;.

![Segreto HTTP](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth 2] {#oauth2}

Per creare un segreto OAuth 2, seleziona **[!UICONTROL OAuth 2]** dall&#39;elenco a **[!UICONTROL discesa Tipo]** . Nei campi riportati di seguito, fornisci l&#39;ID&rbrack; client e [&#128279;](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/)il [[[!UICONTROL segreto]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/)] client, nonché il URL &lbrack;del token per l&#39;integrazione OAuth. Il [!UICONTROL campo Token URL] nel interfaccia è una concatenazione tra l&#39;host del server di autorizzazione e il percorso del token.

![Segreto di OAuth 2](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

In **[!UICONTROL Opzioni]** credenziali è possibile fornire altre opzioni di credenziali, ad esempio `scope` e `audience` sotto forma di coppie chiave-valore. Per aggiungere altre coppie chiave-valore, selezionare **[!UICONTROL Aggiungi un&#39;altra]**.

![Opzioni relative alle credenziali](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

Infine, puoi configurare il valore Offset **&#x200B;**&#x200B;Aggiorna per il segreto. Questo rappresenta il numero di secondi prima della scadenza del token che il sistema eseguirà un aggiornamento automatico. L&#39;ora equivalente in ore e minuti viene visualizzata a destra del campo e viene aggiornata automaticamente durante la digitazione.

![Offset Aggiorna](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

Ad esempio, se l&#39;offset di aggiornamento è impostato sul valore predefinito di `14400` (quattro ore) e il token accesso ha un `expires_in` valore di `86400` (24 ore), il sistema aggiornerà automaticamente il segreto in 20 ore.

>[!IMPORTANT]
>
>Un segreto OAuth richiede almeno quattro ore tra un aggiornamento e l&#39;altro e deve essere valido per almeno otto ore. Questa restrizione ti dà un minimo di quattro ore per intervenire in caso di problemi con il token generato.
>
>Ad esempio, se l&#39;offset è impostato su `28800` (otto ore) e il token accesso ha un `expires_in` valore di `36000` (dieci ore), lo scambio avrà esito negativo a causa della differenza risultante inferiore a quattro ore.

Al termine, selezionare **[!UICONTROL Crea Segreto]** per salvare il segreto.

![Salva Offset OAuth 2](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

### [!UICONTROL OAuth 2 JWT] {#oauth2jwt}

Per creare un segreto JWT per OAuth 2, seleziona **[!UICONTROL OAuth 2 JWT]** dall&#39;elenco a **[!UICONTROL discesa Tipo]** .

![Il [!UICONTROL scheda segreto Crea] con il segreto JWT di OAuth 2 evidenziato nell&#39;elenco a [!UICONTROL discesa Tipo] .](../../images/ui/event-forwarding/secrets/oauth-jwt-secret.png)

>[!NOTE]
>
>L&#39;unico [!UICONTROL algoritmo] attualmente supportato per la firma del JWT è RS256.

Nei campi riportati di seguito, fornisci l&#39;emittente, l&#39;oggetto, [!UICONTROL il pubblico], [!UICONTROL le attestazioni] personalizzate, [!UICONTROL il TTL,] quindi seleziona l&#39;algoritmo  dal menu a discesa. Successivo, inserisci l&#39;ID della chiave privata e il URL [&#128279;](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) del token per l&#39;integrazione OAuth. Il [!UICONTROL campo Token URL] non è un campo obbligatorio. Se viene fornito un valore, il JWT viene scambiato con un token accesso. Il segreto verrà aggiornato in base all&#39;attributo `expires_in` della risposta e al [!UICONTROL valore di offset] Aggiorna. Se non viene fornito un valore, il segreto spinto all&#39;edge è il JWT. Il JWT verrà aggiornato in base ai [!UICONTROL valori TTL] e [!UICONTROL Aggiorna Offset] .

![La [!UICONTROL scheda segreta Crea] con una selezione di campi di input evidenziata.](../../images/ui/event-forwarding/secrets/oauth-jwt-information.png)

In **[!UICONTROL Opzioni]** credenziali è possibile fornire altre opzioni di credenziale, ad esempio `jwt_param` sotto forma di coppie chiave-valore. Per aggiungere altre coppie chiave-valore, selezionare **[!UICONTROL Aggiungi un&#39;altra]**.

![Il [!UICONTROL segreto Crea] scheda evidenziando i [!UICONTROL campi della Opzioni] Credenziale.](../../images/ui/event-forwarding/secrets/oauth-jwt-credential-options.png)

Infine, puoi configurare il valore Offset **&#x200B;**&#x200B;Aggiorna per il segreto. Questo rappresenta il numero di secondi prima della scadenza del token che il sistema eseguirà un aggiornamento automatico. L&#39;ora equivalente in ore e minuti viene visualizzata a destra del campo e viene aggiornata automaticamente durante la digitazione.

![Il [!UICONTROL Crea Segreto] scheda evidenzia il [!UICONTROL campo Offset] Aggiorna.](../../images/ui/event-forwarding/secrets/oauth-jwt-refresh-offset.png)

Ad esempio, se l&#39;offset di aggiornamento è impostato sul valore predefinito di `1800` (30 minuti) e il token accesso ha un `expires_in` valore di `3600` (un&#39;ora), il sistema aggiornerà automaticamente il segreto in un&#39;ora.

>[!IMPORTANT]
>
>Un segreto JWT OAuth 2 richiede almeno 30 minuti tra un aggiornamento e l&#39;altro e deve essere valido per almeno un&#39;ora. Questa restrizione ti dà un minimo di 30 minuti per intervenire in caso di problemi con il token generato.
>
>Ad esempio, se l&#39;offset è impostato su `1800` (30 minuti) e il token accesso ha un valore `expires_in` di `2700` (45 minuti), lo scambio avrà esito negativo a causa della differenza risultante inferiore a 30 minuti.

Al termine, selezionare **[!UICONTROL Crea Segreto]** per salvare il segreto.

![The [!UICONTROL Crea Secret] scheda evidenziando [!UICONTROL Crea Secret]](../../images/ui/event-forwarding/secrets/oauth-jwt-create-secret.png)

### [!UICONTROL Google OAuth 2] {#google-oauth2}

Per creare un segreto di Google OAuth 2, seleziona **[!UICONTROL Google OAuth 2]** dal **[!UICONTROL menu a discesa Tipo]** . In **[!UICONTROL Ambiti]**, seleziona le API di Google a cui desideri concedere il accesso questo segreto. I seguenti prodotti sono attualmente supportati:

* [Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/overview)
* [Pub/Sub API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)

Al termine, selezionare **[!UICONTROL Crea Segreto]**.

![Google OAuth 2 segreto](../../images/ui/event-forwarding/secrets/google-oauth.png)

Viene visualizzato un popover che ti informa che il segreto deve essere autorizzato manualmente tramite Google. Seleziona **[!UICONTROL Crea e autorizza]** per continuare.

![Popover di autorizzazione di Google](../../images/ui/event-forwarding/secrets/google-authorization.png)

Viene visualizzata una finestra di dialogo che consente di inserire le credenziali per il account Google. Segui le istruzioni per concedere l&#39;inoltro degli eventi accesso ai tuoi dati nella ambito selezionata. Una volta completato il processo di autorizzazione, viene creato il segreto.

>[!IMPORTANT]
>
>Se la tua organizzazione dispone di un regola di riautenticazione impostato per le applicazioni Google Cloud, i segreti creati non verranno aggiornati correttamente dopo la scadenza dell&#39;autenticazione (tra 1 e 24 ore a seconda della configurazione regola).
>
>Per risolvere il problema, accedi alla Console di amministrazione Google e vai alla **[!DNL App access control]** pagina in modo da poter contrassegnare l&#39;app di inoltro degli eventi (Adobe Systems Real-Time CDP Event Forwarding) come [!DNL Trusted]. Per ulteriori informazioni, consulta la documentazione di Google sull&#39;impostazione [della durata delle sessioni per i servizi](https://support.google.com/a/answer/9368756) Google Cloud.

### [!UICONTROL [!DNL LinkedIn] OAuth 2] {#linkedin-oauth2}

Per creare un [!DNL LinkedIn] segreto OAuth 2, seleziona **[!UICONTROL [!DNL LinkedIn]OAuth 2]** dall&#39;elenco a **[!UICONTROL discesa Tipo]** . Successivo, seleziona **[!UICONTROL Crea segreto]**.

![Il [!UICONTROL scheda segreto Crea] con il [!UICONTROL campo Tipo] evidenziato.](../../images/ui/event-forwarding/secrets/linkedin-oauth.png)

Viene visualizzato un popover che informa che il segreto deve essere autorizzato manualmente tramite [!DNL LinkedIn]. Seleziona **[!UICONTROL Crea e autorizza segreto con[!DNL LinkedIn]]** per continuare.

![[!DNL LinkedIn] popover di autorizzazione che evidenzia [!UICONTROL Crea &amp; Autorizza segreto con [!DNL LinkedIn]].](../../images/ui/event-forwarding/secrets/linkedin-authorization.png)

Viene visualizzata una finestra di dialogo in cui viene richiesto di immettere le credenziali [!DNL LinkedIn] . Segui le istruzioni per concedere l&#39;inoltro degli eventi accesso ai tuoi dati.

Una volta completato il processo di autorizzazione, si ritorna all&#39;scheda Segreti **, dove è possibile vedere il** segreto appena creato. Qui puoi vedere lo stato del segreto e la data di scadenza.

![Il [!UICONTROL Segreto] scheda evidenziando il segreto appena creato.](../../images/ui/event-forwarding/secrets/linkedin-new-secret.png)

#### Riautorizzare un [!UICONTROL [!DNL LinkedIn] segreto OAuth 2]

>IMPORTANTE
>
>È necessario ripetere l&#39;autorizzazione utilizzando le credenziali [!DNL LinkedIn] ogni 365 giorni. Se non autorizzi nuovamente a tempo debito, il tuo segreto non verrà aggiornato e le richieste di [!DNL LinkedIn] conversione non riusciranno.

Tre mesi prima che il segreto richieda la riautorizzazione, un popup inizierà a mostrare quando si naviga in qualsiasi pagina della proprietà. Seleziona **[!UICONTROL Clicca qui per andare ai tuoi segreti]**.

![La [!UICONTROL panoramica] sulla proprietà scheda evidenziando il popup di ri-autorizzazione segreta.](../../images/ui/event-forwarding/secrets/linkedin-reauthorization-popup.png)

Vieni reindirizzato all&#39;scheda [!UICONTROL Segreti] . I segreti elencati in questa pagina vengono filtrati in modo da mostrare solo i segreti che devono essere nuovamente autorizzati. Seleziona **[!UICONTROL Autenticazione necessaria]** per il segreto che devi riautorizzare.

![The [!UICONTROL Secret scheda] evidenziando [!UICONTROL l&#39;autenticazione necessaria]per il [!DNL LinkedIn] segreto.](../../images/ui/event-forwarding/secrets/linkedin-reauthorization.png)

Viene visualizzata una finestra di dialogo in cui viene richiesto di immettere le credenziali [!DNL LinkedIn] . Segui le istruzioni per riautorizzare il tuo segreto.

## Modifica un segreto

Dopo aver creato i segreti per una proprietà, è possibile trovarli elencati nell&#39;area **[!UICONTROL di lavoro Segreti]** . Per modificare i dettagli di un segreto esistente, selezionarne il nome dall&#39;elenco.

![Seleziona segreto da modificare](../../images/ui/event-forwarding/secrets/edit-secret.png)

La schermata successiva consente di modificare il nome e le credenziali del segreto.

![Modifica segreto](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>Se il segreto è associato a un ambiente esistente, non è possibile riassegnarlo a un altro ambiente. Se si desidera utilizzare le stesse credenziali in un ambiente diverso, è necessario [creare un nuovo segreto](#create) . L&#39;unico modo per riassegnare l&#39;ambiente da questa schermata è se non è mai stato assegnato il segreto a un ambiente in anticipo o se è stato eliminato l&#39;ambiente a cui era collegato il segreto.

### Riprova uno scambio segreto

È possibile riprovare o aggiornare uno scambio segreto dalla schermata di modifica. Questo processo varia a seconda del tipo di segreto che si sta modificando:

| Tipo segreto | Protocollo Riprova |
| --- | --- |
| [!UICONTROL Token] | Selezionare **[!UICONTROL Segreto]** di scambio per ritentare lo scambio segreto. Questo controllo è disponibile solo quando esiste un ambiente associato al segreto. |
| [!UICONTROL HTTP] | Se non è presente alcun ambiente collegato al segreto, selezionare **[!UICONTROL Segreto]** di scambio per scambiare le credenziali con base64. Se è collegato un ambiente, selezionare eleggere **[!UICONTROL Exchange e distribuire segreto]** per scambiare in base64 e distribuire il segreto. |
| [!UICONTROL OAuth 2] | Selezionare **[!UICONTROL Genera token]** per scambiare le credenziali e restituire un token accesso dal provider di autenticazione. |

## Elimina un segreto

Per eliminare un segreto esistente nell&#39;area  **[!UICONTROL di lavoro Segreti]** , selezionare la casella di controllo accanto al nome prima di selezionare **[!UICONTROL Elimina]**.

![Elimina segreto](../../images/ui/event-forwarding/secrets/delete.png)

## Utilizzo dei segreti nell&#39;inoltro degli eventi

Per utilizzare un segreto nell&#39;inoltro degli eventi, è innanzitutto necessario creare un [elemento](../managing-resources/data-elements.md) dati che faccia riferimento al segreto stesso. Dopo aver salvato l&#39;elemento dati, è possibile includerlo nelle regole[&#128279;](../managing-resources/rules.md) di inoltro degli eventi e aggiungere tali regole a un [libreria](../publishing/libraries.md), che a sua volta può essere distribuito ai server di Adobe Systems come [versione](../publishing/builds.md).

Quando crei l&#39;elemento dati, seleziona l&#39;estensione **[!UICONTROL core]** , quindi seleziona **[!UICONTROL Segreto]** per il tipo di elemento dati. Il pannello di destra si aggiorna e fornisce controlli a discesa per assegnare fino a tre segreti all&#39;elemento dati: uno rispettivamente per [!UICONTROL Sviluppo, [!UICONTROL Staging]] e [!UICONTROL Produzione].

![Elemento dati](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>Vengono visualizzati solo i segreti associati agli ambienti di sviluppo, gestione temporanea e produzione per i rispettivi elenchi a discesa.

Assegnando più segreti a un singolo elemento dati e includendolo in un regola, è possibile modificare il valore dell&#39;elemento dati a seconda di dove si trova il libreria contenitore nel flusso[&#128279;](../publishing/publishing-flow.md) di pubblicazione.

![Elemento dati con più segreti](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>Quando si crea l&#39;elemento dati, è necessario assegnare un ambiente di sviluppo. I segreti per gli ambienti di staging e produzione non sono necessari, ma le build che tentano di transizione a tali ambienti avranno esito negativo se gli elementi di dati di tipo segreto non dispongono di un segreto selezionato per l&#39;ambiente in questione.

## Passaggi successivi

Questa guida spiega come gestire segreti in interfaccia. Per informazioni su come interagire con i segreti utilizzando l&#39;API di Reactor, vedere la [guida](../../api/endpoints/secrets.md) agli endpoint dei segreti.
