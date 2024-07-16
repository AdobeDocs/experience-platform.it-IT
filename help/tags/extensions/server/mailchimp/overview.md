---
title: Panoramica dell’estensione Mailchimp
description: Utilizza l’inoltro degli eventi per attivare le e-mail Mailchimp.
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 4%

---

# Panoramica dell’estensione per l’inoltro di eventi Mailchimp

>[!NOTE]
>  
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) come riferimento consolidato delle modifiche terminologiche.

L&#39;estensione Mailchimp [event forwarding](../../../ui/event-forwarding/overview.md) invia eventi all&#39;API Mailchimp Marketing che può attivare le e-mail per campagne di marketing, percorsi o transazioni Mailchimp.

Questo documento illustra come impostare l’estensione e configurare le regole utilizzando l’azione Aggiungi evento.

## Prerequisiti

In questo documento si presuppone che tu abbia familiarità con i prodotti Mailchimp rilevanti utilizzati dall’estensione. Per ulteriori informazioni, consulta la guida di Mailchimp per [campagne](https://mailchimp.com/help/getting-started-with-campaigns/), [percorsi](https://mailchimp.com/help/about-customer-journeys/) e [transazioni](https://mailchimp.com/help/transactional/).

Per utilizzare questa estensione è necessario un account Mailchimp. È possibile registrarsi a un account [qui](https://login.mailchimp.com/signup/). Nel dashboard dell’account Mailchimp, annota i seguenti valori da utilizzare in questa guida:

- Prefisso del dominio Mailchimp
- Chiave API
- L’ID del pubblico
- L’indirizzo e-mail predefinito del mittente

A seconda del piano dell’account Mailchimp, puoi avere un accesso limitato agli strumenti di Percorso del cliente Mailchimp.

>[!TIP]
>  
>Se utilizzi automazioni Mailchimp come e-mail transazionali o Percorsi di clienti, i passaggi e le schermate potrebbero essere leggermente diversi da quelli elencati. Tuttavia, per utilizzare questa estensione ti servono ancora le stesse informazioni descritte in precedenza. Per informazioni dettagliate su ciascuno di questi valori per l&#39;account e il piano specifici, vedere il [Centro assistenza Mailchimp](https://mailchimp.com/help/).

### Prefisso dominio

Dopo aver effettuato l&#39;accesso a Mailchimp e aver effettuato l&#39;accesso alla visualizzazione Dashboard, nella barra degli indirizzi del browser dovrebbe essere visualizzato un URL simile a `https://us11.admin.mailchimp.com` o semplicemente a `us11.admin.mailchimp.com`. In questo esempio, il prefisso `us11` è solo un segnaposto e il valore sarà diverso. Registra l’URL con il prefisso per un passaggio successivo.

### Chiave API

Per trovare la chiave API per l&#39;account, seleziona l&#39;icona del tuo profilo nell&#39;interfaccia utente di Mailchimp, quindi seleziona **Profilo**. Dovresti visualizzare un URL come `https://us11.admin.mailchimp.com/account/profile/` ma con **il tuo** prefisso invece di `us11`.

Seleziona **Extra**, quindi **Chiavi API**:

![Menu Extra, collegamento alle chiavi API](../../../images/extensions/server/mailchimp/menu-API-keys.png)

In **Chiavi API**, puoi scegliere una chiave esistente oppure selezionare **Crea una chiave** per crearne una nuova. Puoi creare una nuova chiave da utilizzare specificamente con questa estensione. Copia la chiave API e salvala per un passaggio successivo. Per ulteriori dettagli, consulta la documentazione di Mailchimp su come [generare la chiave API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### ID pubblico e indirizzo mittente

Seleziona **Pubblico** nell&#39;area di navigazione a sinistra, quindi **Dashboard pubblico**. Quindi, seleziona il pubblico che intendi utilizzare con questa estensione. Per ulteriori informazioni, consulta il documento Mailchimp su [creazione di un pubblico](https://mailchimp.com/help/create-audience/).

Dopo aver creato e selezionato il pubblico, seleziona il menu a discesa **Gestisci pubblico** e scegli **Impostazioni**. Questa schermata mostra varie impostazioni per il pubblico.

Nella parte inferiore della schermata Settings, dovresti vedere `Unique id for audience [audience name]` dove `[audience name]` è il nome del pubblico effettivo. Copia l’ID pubblico e salvalo per un passaggio successivo.

Seleziona **Nome pubblico e impostazioni predefinite** e verifica che **Indirizzo e-mail Da predefinito** abbia il valore corretto per le campagne. Tieni presente che anche l’ID pubblico è elencato nella parte superiore di questa pagina e corrisponde al valore copiato nell’ultimo passaggio.

## Automazioni Mailchimp

A seconda del piano Mailchimp e dell’utilizzo di e-mail transazionali, Percorsi di clienti o altre automazioni di Mailchimp, le impostazioni di percorso specifiche possono variare.

>[!IMPORTANT]
>  
>Il nome dell’evento scelto per attivare l’automazione o il percorso in Mailchimp è lo stesso nome che devi inviare con questa estensione. Prendi nota del nome dell’evento nell’automazione Mailchimp e salvalo per un passaggio successivo.

## Installazione e configurazione

In questa sezione sono elencati i passaggi per installare e configurare l’estensione. Per salvare in modo sicuro la chiave API Mailchimp, è necessario utilizzare l&#39;inoltro eventi [secrets](../../../ui/event-forwarding/secrets.md).

### Creare un elemento segreto e dati

In una proprietà di inoltro eventi, [crea un [!UICONTROL Token] segreto](../../../ui/event-forwarding/secrets.md#token) denominato `Mailchimp API Key`.

Quindi, [crea un elemento dati](../../../ui/managing-resources/data-elements.md#create-a-data-element) utilizzando l&#39;estensione [!UICONTROL Core] e un tipo di elemento dati [!UICONTROL Secret] per fare riferimento al segreto `Mailchimp API Key` appena creato. Immetti `Mailchimp Token` come nome dell&#39;elemento dati.

### Installare e configurare l’estensione

Nella stessa proprietà di inoltro degli eventi, seleziona **[!UICONTROL Estensioni],** quindi **[!UICONTROL Catalogo]** per visualizzare le estensioni disponibili per l&#39;installazione. Da qui, cerca l&#39;estensione Mailchimp e seleziona **[!UICONTROL Installa]**.

![Installa estensione Mailchimp](../../../images/extensions/server/mailchimp/install.png)

Viene visualizzata la schermata di configurazione. In **[!UICONTROL Nome dominio prefisso server Mailchimp]** immettere il dominio copiato in precedenza dall&#39;account Mailchimp, incluso il prefisso di dominio univoco.

>[!IMPORTANT]
>
>Non includere `http://` o `https://` in questo campo.

![Configurazione dell&#39;estensione](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

In **[!UICONTROL Token Mailchimp]**, seleziona l&#39;icona dell&#39;elemento dati e scegli l&#39;elemento dati `Mailchimp Token` creato in precedenza. Seleziona **[!UICONTROL Salva]** per salvare le modifiche.

L&#39;estensione è ora installata e configurata per l&#39;utilizzo nella proprietà.

## Raccolta dati

Quando si utilizza questa estensione in una [regola](../../../ui/managing-resources/rules.md), esistono diversi valori di dati che l&#39;estensione invia a Mailchimp con ogni evento. Per un&#39;implementazione tipica, è possibile configurare l&#39;estensione [Adobe Experience Platform Web SDK](../../client/web-sdk/overview.md) per inviare tali dati a [!DNL Platform Edge Network] per l&#39;utilizzo da parte dell&#39;estensione nella proprietà di inoltro degli eventi.

I dati richiesti da questa estensione possono essere inviati da Web SDK come dati XDM (utilizzando l&#39;oggetto [`xdm`](/help/web-sdk/commands/sendevent/xdm.md)) o come dati non XDM (utilizzando l&#39;oggetto [`data`](/help/web-sdk/commands/sendevent/data.md)).

Ad esempio, se un cliente effettua un acquisto o si registra per un evento sul sito, puoi inviare un’e-mail di conferma tramite Mailchimp con questa estensione. Dopo aver inviato le informazioni richieste da Web SDK all’Edge Network, l’estensione attiva l’e-mail con Mailchimp.

![Aggiungi configurazione azione evento](../../../images/extensions/server/mailchimp/action-configurations.png)

### Elementi dati

La schermata nella sezione precedente mostra i dati che puoi inviare con ogni evento da questa estensione a Mailchimp. Dopo aver configurato Web SDK per inviare questi dati all’Edge Network, puoi creare elementi dati nella proprietà di inoltro degli eventi in modo che l’estensione possa accedere a tali valori.

La tabella seguente fornisce maggiori dettagli per ciascun valore possibile.

| Nome | Percorso di esempio | Tipo | Descrizione | Obbligatorio | Limiti |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> o <br /> `arc.event.data._tenant.emailId` | Stringa | Indirizzo che riceve l’e-mail | **Sì** | Deve esistere nel pubblico Mailchimp |
| `listId` | `arc.event.xdm._tenant.listId`<br /> o <br /> `arc.event.data._tenant.listid` | Stringa | ID pubblico | **Sì** | Deve corrispondere a un ID pubblico esistente |
| `name` | `arc.event.xdm._tenant.name`<br /> o <br /> `arc.event.data._tenant.name` | Stringa | Nome dell’evento | **Sì** | 2-30 caratteri |
| `properties` | `arc.event.xdm._tenant.properties`<br /> o <br /> `arc.event.data._tenant.properties` | Oggetto | Un elenco facoltativo di proprietà in formato JSON con dettagli sull’evento | No |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> o <br /> `arc.event.data._tenant.isSyncing` | booleano | Gli eventi creati con `is_syncing` impostato su `true` **non attiveranno** le automazioni | No |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> o `arc.event.data._tenant.occuredAt` | Stringa | Una marca temporale ISO 8601 del momento in cui si è verificato l’evento | No |  |

{style="table-layout:auto"}

>[!IMPORTANT]
>  
>I valori **Esempio di percorso** sopra sono solo esempi. I nomi dei campi e i [percorsi](../../../ui/event-forwarding/overview.md#data-element-path) a cui si fa riferimento in questi elementi dati possono essere diversi nella proprietà, a seconda di come è stato denominato e configurato Web SDK nei passaggi precedenti.

Nella proprietà di inoltro degli eventi, puoi creare un elemento dati per ciascuno dei campi descritti in precedenza. Una volta creati, puoi fare riferimento agli elementi dati nell&#39;azione [!UICONTROL Aggiungi evento] di questa estensione.

![Aggiungi configurazione azione evento](../../../images/extensions/server/mailchimp/action-configurations.png)

Ora puoi utilizzare questa estensione e l’azione Aggiungi evento per attivare le e-mail Mailchimp per i tipi di pubblico.

## Convalida dei dati

Quando si lavora con estensioni di inoltro eventi, l&#39;[Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) è molto utile. Nella sezione Registri, in Registri di Edge puoi visualizzare le richieste effettuate dalle regole di inoltro degli eventi dopo che sono state attivate. Le schermate seguenti mostrano una richiesta all’API Mailchimp da parte dell’estensione.

![Adobe Experience Platform Debugger](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

Nel dashboard Mailchimp, nella vista Feed attività del pubblico o del membro del pubblico, viene fornito un elenco di eventi per quel pubblico o membro del pubblico. Questo deve corrispondere agli eventi inviati dall&#39;estensione e mostrare tutti i dati facoltativi inviati, insieme all&#39;e-mail o alla campagna che hanno ricevuto. Per ulteriori informazioni, vedere le [guide per l&#39;automazione di Mailchimp](https://mailchimp.com/help/automation/).
