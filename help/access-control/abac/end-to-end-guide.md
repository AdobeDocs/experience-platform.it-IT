---
keywords: Experience Platform;home;argomenti popolari;controllo accessi;controllo accessi basato su attributi;
title: Guida end-to-end per il controllo dell'accesso basato su attributi
description: Questo documento fornisce una guida end-to-end sul controllo degli accessi basato su attributi in Adobe Experience Platform
hide: true
hidefromtoc: true
source-git-commit: f7a8f9a5eb0ef3c961f9524057ff01564f88dec3
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 0%

---

# Guida end-to-end per il controllo degli accessi basato su attributi

Il controllo dell&#39;accesso basato su attributi è una funzione di Adobe Experience Platform che offre ai marchi consapevoli della privacy una maggiore flessibilità per gestire l&#39;accesso degli utenti. I singoli oggetti, ad esempio i campi e i segmenti dello schema, possono essere assegnati ai ruoli utente. Questa funzione ti consente di concedere o revocare l’accesso a singoli oggetti per utenti Platform specifici della tua organizzazione.

Questa funzionalità ti consente di classificare campi dello schema, segmenti e così via con etichette che definiscono ambiti di utilizzo organizzativi o dati. In Adobe Journey Optimizer puoi applicare queste stesse etichette a percorsi e offerte. In parallelo, gli amministratori possono definire i criteri di accesso relativi ai campi dello schema XDM e gestire meglio gli utenti o i gruppi (utenti interni, esterni o di terze parti) che possono accedere a tali campi.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [Servizio di segmentazione di Adobe Experience Platform](../../segmentation/home.md): Il motore di segmentazione in [!DNL Platform] utilizzato per creare segmenti di pubblico dai profili cliente in base ai comportamenti e agli attributi dei clienti.

### Panoramica del caso d’uso

Questa guida utilizza un caso d’uso esemplificativo di limitazione dell’accesso ai dati sensibili per illustrare il flusso di lavoro. È disponibile un esempio di flusso di lavoro per il controllo degli accessi basato su attributi, in cui puoi creare e assegnare ruoli, etichette e criteri per configurare se gli utenti possono o meno accedere a determinate risorse all’interno dell’organizzazione. Questo caso d’uso è descritto di seguito:

Sei un fornitore di servizi sanitari e vuoi configurare l’accesso alle risorse della tua organizzazione.

* Il team di marketing interno deve essere in grado di accedere a **[!UICONTROL PHI/Dati sanitari regolamentati]** dati.
* La tua agenzia esterna non dovrebbe essere in grado di accedere **[!UICONTROL PHI/Dati sanitari regolamentati]** dati.

A questo scopo, devi configurare ruoli, risorse e criteri.

Sarà possibile:

* [Etichettare i ruoli per gli utenti]{#label-roles}: Utilizzare l&#39;esempio di un fornitore di assistenza sanitaria (ACME Business Group) il cui gruppo di marketing lavora con agenzie esterne.
* [Etichettare le risorse (campi e segmenti di schema)]{#label-resources}: Assegna **[!UICONTROL PHI/Dati sanitari regolamentati]** alle risorse e ai segmenti dello schema.
* [Creare il criterio che li collegherà]{#policy}: Crea un criterio per collegare le etichette delle risorse alle etichette nel tuo ruolo negando l’accesso ai campi e ai segmenti dello schema. In questo modo verrà negato l’accesso al campo dello schema e al segmento in tutte le sandbox per gli utenti che non dispongono di etichette corrispondenti.

## Autorizzazioni

[!UICONTROL Autorizzazioni] è l’area di Experience Cloud in cui gli amministratori possono definire ruoli utente e criteri di accesso per gestire le autorizzazioni di accesso per funzioni e oggetti all’interno di un’applicazione di prodotto.

Attraverso [!UICONTROL Autorizzazioni], puoi creare e gestire i ruoli e assegnare le autorizzazioni di risorse desiderate per questi ruoli. [!UICONTROL Autorizzazioni] consente inoltre di gestire le etichette, le sandbox e gli utenti associati a un ruolo specifico.

Se non disponi di privilegi di amministratore, contatta l’amministratore di sistema per ottenere l’accesso.

Una volta disponibili i privilegi di amministratore, vai a [Adobe Experience Cloud](https://experience.adobe.com/) e accedi utilizzando le tue credenziali Adobe. Una volta effettuato l&#39;accesso, il **[!UICONTROL Panoramica]** viene visualizzata la pagina della tua organizzazione per la quale disponi dei privilegi di amministratore. Questa pagina mostra i prodotti a cui l’organizzazione è abbonata, insieme ad altri controlli per aggiungere utenti e amministratori all’organizzazione nel suo complesso. Seleziona **[!UICONTROL Autorizzazioni]** per aprire l’area di lavoro per l’integrazione con Platform.

![Immagine che mostra il prodotto Autorizzazioni selezionato in Adobe Experience Cloud](../images/flac-ui/flac-select-product.png)

Viene visualizzata l’area di lavoro Autorizzazioni per l’interfaccia utente di Platform, che si apre nella **[!UICONTROL Ruoli]** pagina.

## Applicare etichette a un ruolo {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="Cosa sono le etichette?"
>abstract="Le etichette consentono di classificare set di dati e campi in base ai criteri di utilizzo applicati a tali dati. Platform fornisce diverse etichette per l’utilizzo dei dati &quot;core&quot; definite da Adobi, che coprono un’ampia gamma di restrizioni comuni applicabili alla governance dei dati. Ad esempio, le etichette &quot;S&quot; sensibili come RHD (Regulated Health Data) consentono di classificare i dati che si riferiscono a Protected Health Information (PHI). Puoi anche definire etichette personalizzate che soddisfano le esigenze della tua organizzazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#understanding-data-usage-labels" text="Panoramica delle etichette di utilizzo dei dati"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Crea nuova etichetta"
>abstract="Puoi creare etichette personalizzate per adattarle alle esigenze della tua organizzazione. Le etichette personalizzate possono essere utilizzate per applicare ai dati sia le configurazioni di governance dei dati che di controllo degli accessi."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#manage-labels" text="Gestire le etichette personalizzate"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="Cosa sono i ruoli?"
>abstract="I ruoli sono modi per classificare i tipi di utenti che interagiscono con l’istanza Platform e costituiscono blocchi costitutivi dei criteri di controllo degli accessi. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di visualizzazione o scrittura necessario."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en" text="Gestire i ruoli"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Crea nuovo ruolo"
>abstract="Puoi creare un nuovo ruolo per classificare meglio gli utenti che accedono all’istanza di Platform. Ad esempio, puoi creare un ruolo per un team di marketing interno e applicare l’etichetta RHD a tale ruolo, in modo da consentire al team di marketing interno di accedere alle informazioni sulla salute protetta (PHI). In alternativa, è anche possibile creare un ruolo per un&#39;agenzia esterna e negare l&#39;accesso di ruolo ai dati PHI non applicando l&#39;etichetta RHD a quel ruolo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en#create-a-new-role" text="Creare un nuovo ruolo"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Panoramica del ruolo"
>abstract="Nella finestra di dialogo panoramica ruolo vengono visualizzate le risorse e le sandbox a cui un determinato ruolo può accedere."

I ruoli sono modi per classificare i tipi di utenti che interagiscono con l’istanza Platform e costituiscono blocchi costitutivi dei criteri di controllo degli accessi. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di cui hanno bisogno.

Per iniziare, seleziona **[!UICONTROL ACME Business Group]** dal **[!UICONTROL Ruoli]** pagina.

![Immagine che mostra il ruolo aziendale ACME selezionato in Ruoli](../images/abac-end-to-end-user-guide/abac-select-role.png)

Quindi, seleziona **[!UICONTROL Etichette]** quindi seleziona **[!UICONTROL Aggiungi etichette]**.

![Immagine che mostra Aggiungi etichette selezionate nella scheda Etichette](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

Viene visualizzato un elenco di tutte le etichette dell’organizzazione. Seleziona **[!UICONTROL RHD]** per aggiungere l’etichetta **[!UICONTROL PHI/Dati sanitari regolamentati]**. Lasciare che accanto all’etichetta venga visualizzato un segno di spunta blu, quindi selezionare **[!UICONTROL Salva]**.

![Immagine che mostra l’etichetta RHD selezionata e salvata](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

## Applicare etichette ai campi dello schema {#label-resources}

Ora che hai configurato un ruolo utente con il [!UICONTROL RHD] etichetta, il passaggio successivo consiste nell’aggiungere la stessa etichetta alle risorse che si desidera controllare per quel ruolo.

Seleziona **[!UICONTROL Schemi]** dalla navigazione a sinistra, quindi seleziona **[!UICONTROL Medicale ACME]** dall’elenco degli schemi visualizzati.

![Immagine che mostra lo schema ACME Healthcare selezionato dalla scheda Schemi](../images/abac-end-to-end-user-guide/abac-select-schema.png)

Quindi, seleziona **[!UICONTROL Etichette]** per visualizzare un elenco dei campi associati allo schema. Da qui è possibile assegnare etichette a uno o più campi contemporaneamente. Seleziona la **[!UICONTROL Glucosio nel sangue]** e **[!UICONTROL LivelloInsulina]** campi, quindi selezionare **[!UICONTROL Modifica delle etichette di governance]**.

![Immagine che mostra i valori BloodGlucosio e InsulinLevel selezionati e modifica le etichette di governance selezionate](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

La **[!UICONTROL Modificare le etichette]** viene visualizzata una finestra di dialogo che consente di scegliere le etichette da applicare ai campi dello schema. Per questo caso d’uso, seleziona la **[!UICONTROL PHI/Dati sanitari regolamentati]** etichetta, quindi seleziona **[!UICONTROL Salva]**.

![Immagine che mostra l’etichetta RHD selezionata e salvata](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>Quando un’etichetta viene aggiunta a un campo, l’etichetta viene applicata alla risorsa principale del campo (classe o gruppo di campi). Se la classe o il gruppo di campi padre è utilizzato da altri schemi, questi schemi erediteranno la stessa etichetta.

## Applicare etichette ai segmenti

Una volta completata l’etichettatura dei campi dello schema, puoi iniziare a etichettare i segmenti.

Seleziona **[!UICONTROL Segmenti]** dalla navigazione a sinistra. Viene visualizzato un elenco dei segmenti disponibili nell’organizzazione. In questo esempio, i due segmenti seguenti devono essere etichettati in quanto contengono dati di integrità sensibili:

* Glucosio nel sangue >100
* Insulina &lt;50

Seleziona **[!UICONTROL Glucosio nel sangue >100]** per iniziare a etichettare il segmento.

![Immagine che mostra il glucosio nel sangue >100 selezionato dalla scheda Segmenti](../images/abac-end-to-end-user-guide/abac-select-segment.png)

Il segmento **[!UICONTROL Dettagli]** viene visualizzata la schermata . Seleziona **[!UICONTROL Gestisci accesso]**.

![Immagine che mostra la selezione di Gestione accesso](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

La **[!UICONTROL Modificare le etichette]** viene visualizzata una finestra di dialogo che consente di scegliere le etichette da applicare al segmento. Per questo caso d’uso, seleziona la **[!UICONTROL PHI/Dati sanitari regolamentati]** etichetta, quindi seleziona **[!UICONTROL Salva]**.

![Immagine che mostra la selezione dell’etichetta RHD e il salvataggio selezionato](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

Ripeti i passaggi precedenti con **[!UICONTROL Insulina &lt;50]**.

## Creare un criterio di controllo degli accessi {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="Che cosa sono le politiche?"
>abstract="Le politiche sono dichiarazioni che riuniscono gli attributi per stabilire azioni ammissibili e non ammissibili. A ogni organizzazione viene fornito un criterio predefinito che è necessario attivare per definire regole per risorse quali segmenti e campi dello schema. I criteri predefiniti non possono essere modificati o eliminati. Tuttavia, i criteri predefiniti possono essere attivati o disattivati."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en" text="Gestire i criteri"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Creare un criterio"
>abstract="Crea un criterio per definire le azioni che gli utenti possono e non possono eseguire sui segmenti e sui campi dello schema."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#create-a-new-policy" text="Creare un criterio"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configurare le azioni ammissibili e non ammissibili per una politica"
>abstract="Seleziona Consenti accesso a per configurare le azioni consentite che gli utenti possono eseguire rispetto alle risorse. Seleziona nega l’accesso a per configurare azioni non consentite che gli utenti non possono eseguire in base alle risorse."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#edit-a-policy" text="Modificare un criterio"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configurare le autorizzazioni per una risorsa"
>abstract="Una risorsa è la risorsa o l’oggetto a cui un utente può o non può accedere. Le risorse possono essere segmenti o schemi. Puoi configurare le autorizzazioni di scrittura, lettura o eliminazione per segmenti e campi dello schema."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Modifica condizioni"
>abstract="Applicare istruzioni condizionali al criterio per configurare l’accesso degli utenti a determinate risorse. Seleziona abbina tutto per richiedere agli utenti di avere ruoli con le stesse etichette di una risorsa per poter accedere. Seleziona fai clic su &quot;abbina&quot; per richiedere agli utenti di avere un ruolo con una sola etichetta che corrisponda a una risorsa. Le etichette possono essere definite come etichette di base o personalizzate, con etichette di base che rappresentano le etichette create e fornite da etichette Adobi e personalizzate che rappresentano le etichette create per la tua organizzazione."

I criteri di controllo degli accessi sfruttano le etichette per definire quali ruoli utente hanno accesso a risorse specifiche di Platform. I criteri possono essere locali o globali e possono sostituire altri criteri. In questo esempio, l’accesso ai campi e ai segmenti dello schema verrà negato in tutte le sandbox agli utenti che non hanno le etichette corrispondenti nel campo dello schema.

Per creare un criterio di controllo accessi, selezionare **[!UICONTROL Autorizzazioni]** dalla navigazione a sinistra, quindi seleziona **[!UICONTROL Criteri]**. Quindi, seleziona **[!UICONTROL Crea criterio]**.

![Immagine che mostra l&#39;opzione Crea criterio selezionata nelle autorizzazioni](../images/abac-end-to-end-user-guide/abac-create-policy.png)

La **[!UICONTROL Crea nuovo criterio]** viene visualizzata una finestra di dialogo in cui viene richiesto di immettere un nome e una descrizione facoltativa. Seleziona **[!UICONTROL Conferma]** una volta finito.

![Immagine che mostra la finestra di dialogo Crea nuovo criterio e seleziona Conferma](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

Per negare l’accesso ai campi dello schema, utilizza la freccia a discesa e seleziona **[!UICONTROL Nega l&#39;accesso a]** quindi seleziona **[!UICONTROL Nessuna risorsa selezionata]**. Quindi, seleziona **[!UICONTROL Campo schema]** quindi seleziona **[!UICONTROL Tutto]**.

![Immagine che mostra l&#39;accesso negato e le risorse selezionate](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

La tabella seguente mostra le condizioni disponibili per la creazione di un criterio:

| Condizioni | Descrizione |
| --- | --- |
| Il seguente è falso | Se è impostata l’opzione &quot;Nega accesso a&quot;, l’accesso verrà limitato se l’utente non soddisfa i criteri selezionati. |
| Il seguente è vero | Se è impostato il valore &quot;Permette l’accesso a&quot;, l’accesso sarà limitato se l’utente soddisfa i criteri selezionati. |
| Corrisponde a qualsiasi | L’utente dispone di un’etichetta che corrisponde a qualsiasi etichetta applicata a una risorsa. |
| Corrisponde a tutti | L’utente dispone di tutte le etichette che corrispondono a tutte le etichette applicate a una risorsa. |
| Etichetta core | Un’etichetta di base è un’etichetta definita da un Adobe disponibile in tutte le istanze di Platform. |
| Etichetta personalizzata | Un’etichetta personalizzata è un’etichetta creata dall’organizzazione. |

Seleziona **[!UICONTROL Il seguente è falso]** quindi seleziona **[!UICONTROL Nessun attributo selezionato]**. Quindi, seleziona l’utente **[!UICONTROL Etichetta core]**, quindi seleziona **[!UICONTROL Corrisponde a tutti]**. Seleziona la risorsa **[!UICONTROL Etichetta core]** e infine seleziona **[!UICONTROL Aggiungi risorsa]**.

![Immagine che mostra le condizioni selezionate e Aggiungi risorsa selezionata](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>Una risorsa è la risorsa o l’oggetto a cui un soggetto può o non può accedere. Le risorse possono essere segmenti o schemi.

Per negare l’accesso ai segmenti, utilizza la freccia a discesa e seleziona **[!UICONTROL Nega l&#39;accesso a]** quindi seleziona **[!UICONTROL Nessuna risorsa selezionata]**. Quindi, seleziona **[!UICONTROL Segmento]** quindi seleziona **[!UICONTROL Tutto]**.

Seleziona **[!UICONTROL Il seguente è falso]** quindi seleziona **[!UICONTROL Nessun attributo selezionato]**. Quindi, seleziona l’utente **[!UICONTROL Etichetta core]**, quindi seleziona **[!UICONTROL Corrisponde a tutti]**. Seleziona la risorsa **[!UICONTROL Etichetta core]** e infine seleziona **[!UICONTROL Salva]**.

![Immagine che mostra le condizioni selezionate e l&#39;opzione Salva](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Seleziona **[!UICONTROL Attiva]** per attivare il criterio, viene visualizzata una finestra di dialogo che richiede di confermare l’attivazione. Seleziona **[!UICONTROL Conferma]** quindi seleziona **[!UICONTROL Chiudi]**.

![Immagine che mostra il criterio da attivare ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png)

## Passaggi successivi

È stata completata l’applicazione di etichette a un ruolo, campi di schema e segmenti. All’agenzia esterna assegnata a questi ruoli è impedito di visualizzare queste etichette e i relativi valori nello schema, nel set di dati e nella visualizzazione del profilo. A questi campi è inoltre impedito di essere utilizzati nella definizione del segmento quando si utilizza il Generatore di segmenti.

Per ulteriori informazioni sul controllo degli accessi basato su attributi, consulta la sezione [panoramica sul controllo dell&#39;accesso basato sugli attributi](./overview.md).
