---
title: Panoramica sull'estensione di Mailchimp
description: Utilizza l’inoltro eventi per attivare le e-mail Mailchimp.
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 5%

---

# Panoramica sull&#39;estensione dell&#39;inoltro eventi Mailchimp

>[!NOTE]
>  
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) come riferimento consolidato delle modifiche terminologiche.

Il Mailchimp [inoltro eventi](../../../ui/event-forwarding/overview.md) l’estensione invia gli eventi all’API marketing Mailchimp che può attivare le e-mail per campagne di marketing, percorsi o transazioni Mailchimp.

Questo documento illustra come impostare l&#39;estensione e configurare le regole utilizzando l&#39;azione Aggiungi evento .

## Prerequisiti

Questo documento presuppone che tu abbia familiarità con i prodotti Mailchimp pertinenti sfruttati dall&#39;estensione. Per ulteriori informazioni, consulta la documentazione di aiuto di Mailchimp per [campagne](https://mailchimp.com/help/getting-started-with-campaigns/), [percorsi](https://mailchimp.com/help/about-customer-journeys/)e [transazioni](https://mailchimp.com/help/transactional/).

Per utilizzare questa estensione è necessario un account Mailchimp. È possibile registrarsi per un account [qui](https://login.mailchimp.com/signup/). Nel dashboard dell’account Mailchimp, prendi nota dei seguenti valori da utilizzare in questa guida:

- Prefisso del dominio Mailchimp
- Chiave API
- ID del pubblico
- L’indirizzo e-mail predefinito &quot;Da&quot;

A seconda del piano del tuo account Mailchimp, potresti avere accesso limitato agli strumenti del Percorso cliente Mailchimp.

>[!TIP]
>  
>Se utilizzi automazioni Mailchimp come e-mail transazionali o Percorsi di clienti, i passaggi e gli schermi possono essere leggermente diversi da quelli elencati qui. Tuttavia, per utilizzare questa estensione sono comunque necessarie le stesse informazioni descritte in precedenza. Consulta la sezione [Centro assistenza di Mailchimp](https://mailchimp.com/help/) per informazioni dettagliate su ciascuno di questi valori per il tuo account e piano specifico.

### Prefisso dominio

Dopo aver effettuato l’accesso a Mailchimp e aver effettuato la destinazione nella vista Dashboard, la barra degli indirizzi del browser dovrebbe visualizzare un URL come `https://us11.admin.mailchimp.com` o semplicemente `us11.admin.mailchimp.com`. In questo esempio, il prefisso `us11` è solo un segnaposto e il tuo valore sarà diverso. Registra l&#39;URL con il prefisso per un passaggio successivo.

### API key

Per trovare la chiave API del tuo account, seleziona l’icona del tuo profilo nell’interfaccia utente di Mailchimp, quindi seleziona **Profilo**. Dovresti visualizzare un URL come `https://us11.admin.mailchimp.com/account/profile/` ma con **le** prefisso anziché `us11`.

Seleziona **Extra**, quindi **Chiavi API**:

![Menu Extra, collegamento chiavi API](../../../images/extensions/server/mailchimp/menu-API-keys.png)

Sotto **Le chiavi API**, puoi scegliere una chiave esistente oppure selezionare **Creare Una Chiave** per crearne una nuova. Puoi creare una nuova chiave da utilizzare specificatamente con questa estensione. Copia la chiave API e salvala per un passaggio successivo. Per ulteriori dettagli, consulta la documentazione di Mailchimp su come [genera la chiave API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### ID pubblico e indirizzo Da

Seleziona **Pubblico** nella navigazione a sinistra, quindi **Dashboard del pubblico**. Quindi, seleziona il pubblico che intendi utilizzare con questa estensione. Per ulteriori informazioni, consulta il documento Mailchimp su [creazione di un pubblico](https://mailchimp.com/help/create-audience/).

Con il pubblico creato e selezionato, seleziona la **Gestire il pubblico** menu a discesa e scegli **Impostazioni**. Questa schermata mostra varie impostazioni per il pubblico.

Nella parte inferiore della schermata Settings (Impostazioni), dovresti vedere `Unique id for audience [audience name]` dove `[audience name]` è il nome del pubblico effettivo. Copia l&#39;ID del pubblico e salvalo per un passaggio successivo.

Seleziona **Nome e impostazioni predefinite del pubblico** e confermare che **Indirizzo e-mail predefinito da** ha il valore corretto per le campagne. Tieni presente che l’ID pubblico è elencato anche nella parte superiore della pagina ed è lo stesso valore copiato nell’ultimo passaggio.

## Automazioni Mailchimp

A seconda del piano Mailchimp e se utilizzi e-mail transazionali, Percorsi di clienti o altre automazioni Mailchimp, le impostazioni di percorso specifiche possono variare.

>[!IMPORTANT]
>  
>Il nome evento scelto per attivare l&#39;automazione o il percorso in Mailchimp è lo stesso nome evento che devi inviare con questa estensione. Osserva il nome dell’evento nell’automazione Mailchimp e salvalo per un passaggio successivo.

## Installazione e configurazione

In questa sezione sono elencati i passaggi per installare e configurare l&#39;estensione . Per salvare in modo sicuro la chiave API Mailchimp, devi utilizzare l’inoltro eventi [segreti](../../../ui/event-forwarding/secrets.md).

### Creare un segreto e un elemento dati

In una proprietà di inoltro eventi, [creare un [!UICONTROL Token] segreto](../../../ui/event-forwarding/secrets.md#token) chiamato `Mailchimp API Key`.

Successivamente, [creare un elemento dati](../../../ui/managing-resources/data-elements.md#create-a-data-element) utilizzando [!UICONTROL Core] estensione e [!UICONTROL Segreto] tipo di elemento dati per fare riferimento al `Mailchimp API Key` segreto che hai appena creato. Invio `Mailchimp Token` come nome dell’elemento dati.

### Installa e configura l&#39;estensione 

Nella stessa proprietà di inoltro eventi, seleziona **[!UICONTROL Estensioni],** then **[!UICONTROL Catalogo]** per visualizzare le estensioni disponibili per l&#39;installazione. Da qui, cerca l&#39;estensione Mailchimp e seleziona **[!UICONTROL Installa]**.

![Installa estensione Mailchimp](../../../images/extensions/server/mailchimp/install.png)

Viene visualizzata la schermata di configurazione. Sotto **[!UICONTROL Nome di dominio del prefisso del server Mailchimp]**, immetti il dominio copiato in precedenza dall’account Mailchimp, incluso il prefisso di dominio univoco.

>[!IMPORTANT]
>
>Non includere `http://` o `https://` in questo campo.

![Configurazione dell&#39;estensione](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

Sotto **[!UICONTROL Token Mailchimp]**, seleziona l’icona dell’elemento dati e scegli la `Mailchimp Token` elemento dati creato in precedenza. Seleziona **[!UICONTROL Salva]** per salvare le modifiche.

L&#39;estensione viene ora installata e configurata per l&#39;utilizzo nella proprietà .

## Raccolta dati

Quando utilizzi questa estensione in un [regola](../../../ui/managing-resources/rules.md), esistono diversi valori di dati che l’estensione invia a Mailchimp con ogni evento. Per un’implementazione tipica, puoi configurare le [Estensione Adobe Experience Platform Web SDK](../../client/sdk/overview.md) per inviare tali dati a [!DNL Platform Edge Network] per l&#39;utilizzo da parte dell&#39;estensione nella proprietà di inoltro eventi.

I dati richiesti da questa estensione possono essere inviati dall’SDK per web come dati XDM o non XDM. Per ulteriori informazioni, consulta la documentazione . [invio di dati XDM](../../../../edge/fundamentals/tracking-events.md#sending-non-xdm-data).

Ad esempio, se un cliente effettua un acquisto o si registra per un evento sul tuo sito, puoi inviare un’e-mail di conferma tramite Mailchimp con questa estensione. Una volta inviate le informazioni richieste dall’SDK web alla rete Edge, l’estensione attiva l’e-mail con Mailchimp.

![Aggiungi configurazione azione evento](../../../images/extensions/server/mailchimp/action-configurations.png)

### Elementi dati

La schermata nella sezione precedente mostra i dati che puoi inviare con ogni evento da questa estensione a Mailchimp. Una volta configurato l’SDK web per l’invio di tali dati alla rete Edge, puoi creare elementi dati nella proprietà di inoltro eventi in modo che l’estensione possa accedere a tali valori.

La tabella seguente fornisce ulteriori dettagli per ogni possibile valore.

| Nome | Esempio di percorso | Tipo | Descrizione | Obbligatorio | Limiti |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> oppure<br /> `arc.event.data._tenant.emailId` | Stringa | Indirizzo che riceve l’e-mail | **Sì** | Deve esistere nel pubblico di Mailchimp |
| `listId` | `arc.event.xdm._tenant.listId`<br /> oppure<br /> `arc.event.data._tenant.listid` | Stringa | ID pubblico | **Sì** | Deve corrispondere a un ID pubblico esistente |
| `name` | `arc.event.xdm._tenant.name`<br /> oppure<br /> `arc.event.data._tenant.name` | Stringa | Nome dell’evento | **Sì** | 2-30 caratteri in lunghezza |
| `properties` | `arc.event.xdm._tenant.properties`<br /> oppure<br /> `arc.event.data._tenant.properties` | Oggetto | Un elenco facoltativo di proprietà in formato JSON con dettagli sull’evento | No |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> oppure<br /> `arc.event.data._tenant.isSyncing` | booleano | Eventi creati con `is_syncing` impostato su `true` **non** attivazione automatizzazioni | No |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> oppure `arc.event.data._tenant.occuredAt` | Stringa | Una marca temporale ISO 8601 di quando si è verificato l’evento | No |  |

{style=&quot;table-layout:auto&quot;}

>[!IMPORTANT]
>  
>La **Esempio di percorso** i valori sopra riportati sono solo esempi. I nomi dei campi e [paths](../../../ui/event-forwarding/overview.md#data-element-path) i riferimenti in questi elementi dati possono essere diversi nella tua proprietà, a seconda della modalità con cui hai denominato e configurato l’SDK web nei passaggi precedenti.

Nella proprietà inoltro eventi, puoi creare un elemento dati per ciascuno dei campi descritti in precedenza. Una volta creato, puoi fare riferimento agli elementi dati nel [!UICONTROL Aggiungi evento] dell&#39;estensione.

![Aggiungi configurazione azione evento](../../../images/extensions/server/mailchimp/action-configurations.png)

Ora puoi utilizzare questa estensione e l’azione Aggiungi evento per attivare le e-mail Mailchimp per i tipi di pubblico.

## Convalida dei dati

Quando si lavora con estensioni di inoltro eventi, la [Debugger Adobe Experience Platform](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) è molto utile. Nella sezione Registri , sotto i registri di Edge puoi vedere le richieste effettuate dalle regole di inoltro degli eventi dopo l’attivazione. Le schermate seguenti mostrano una richiesta effettuata all’API Mailchimp dall’estensione .

![Debugger Adobe Experience Platform](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

Nel dashboard di Mailchimp, nella vista Feed attività del pubblico o membro del pubblico, viene fornito un elenco di eventi per quel pubblico o membro del pubblico. Questo deve corrispondere agli eventi inviati dall’estensione e mostrare eventuali dati facoltativi inviati, insieme all’e-mail o alla campagna ricevuta. Consulta la sezione [Guide guida all&#39;automazione di Mailchimp](https://mailchimp.com/help/automation/) per ulteriori dettagli.
