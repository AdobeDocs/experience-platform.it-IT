---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;controllo degli accessi basato su attributi;
title: Guida end-to-end al controllo degli accessi basato su attributi
description: Questo documento fornisce una guida end-to-end sul controllo degli accessi basato su attributi in Adobe Experience Platform
role: Developer
exl-id: 7e363adc-628c-4a66-a3bd-b5b898292394
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1522'
ht-degree: 7%

---

# Guida end-to-end al controllo degli accessi basato su attributi

Utilizza il controllo degli accessi basato sugli attributi su Adobe Experience Platform per offrire a te stesso e ad altri clienti multi-brand attenti alla privacy una maggiore flessibilità nella gestione degli accessi utente. L’accesso ai singoli oggetti, come i campi dello schema e i tipi di pubblico, può essere concesso con criteri basati sugli attributi e sul ruolo dell’oggetto. Questa funzione consente di concedere o revocare l’accesso a singoli oggetti per specifici utenti di Experience Platform nella tua organizzazione.

Questa funzionalità consente di categorizzare campi dello schema, tipi di pubblico e così via con etichette che definiscono ambiti di utilizzo organizzativi o dei dati. Puoi applicare queste stesse etichette a percorsi, Offerte e altri oggetti in Adobe Journey Optimizer. Parallelamente, gli amministratori possono definire i criteri di accesso relativi ai campi dello schema Experience Data Model (XDM) e gestire meglio quali utenti o gruppi (interni, esterni o di terze parti) possono accedere a tali campi.

>[!NOTE]
>
>Questo documento si concentra sul caso d’uso dei criteri di controllo degli accessi. Se stai tentando di impostare criteri per gestire l&#39;**utilizzo** dei dati, anziché i criteri a cui gli utenti di Experience Platform hanno accesso, consulta invece la guida end-to-end sulla [governance dei dati](../../data-governance/e2e.md).

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [Servizio di segmentazione di Adobe Experience Platform](../../segmentation/home.md): il motore di segmentazione all&#39;interno di [!DNL Experience Platform] utilizzava per creare segmenti di pubblico dai profili dei clienti in base ai comportamenti e agli attributi dei clienti.

### Panoramica del caso d’uso

Seguirai un esempio di flusso di lavoro di controllo degli accessi basato su attributi in cui potrai creare e assegnare ruoli, etichette e criteri per configurare se gli utenti possono o meno accedere a risorse specifiche dell’organizzazione. Questa guida utilizza un esempio di limitazione dell’accesso ai dati sensibili per illustrare il flusso di lavoro. Questo caso d’uso è descritto di seguito:

I professionisti del settore sanitario desiderano configurare l’accesso alle risorse dell’organizzazione.

* Il team marketing interno deve essere in grado di accedere ai dati di **[!UICONTROL PHI/ Regulated Health Data]**.
* L&#39;agenzia esterna non dovrebbe essere in grado di accedere ai dati di **[!UICONTROL PHI/ Regulated Health Data]**.

A questo scopo, devi configurare ruoli, risorse e criteri.

Effettua le seguenti operazioni:

* [Assegna un&#39;etichetta ai ruoli degli utenti](#label-roles): utilizza l&#39;esempio di un fornitore di assistenza sanitaria (ACME Business Group) il cui gruppo di marketing lavora con agenzie esterne.
* [Assegna un&#39;etichetta alle risorse (campi dello schema e tipi di pubblico)](#label-resources): Assegna l&#39;etichetta **[!UICONTROL PHI/ Regulated Health Data]** alle risorse e ai tipi di pubblico dello schema.
* [Attiva i criteri che li collegheranno](#policy): abilita i criteri predefiniti per impedire l&#39;accesso ai campi dello schema e ai tipi di pubblico collegando le etichette delle risorse alle etichette del tuo ruolo. Gli utenti con etichette corrispondenti avranno quindi accesso al campo e al segmento dello schema in tutte le sandbox.

## Autorizzazioni

[!UICONTROL Permissions] è l&#39;area di Experience Cloud in cui gli amministratori possono definire ruoli utente e criteri per gestire le autorizzazioni per funzionalità e oggetti all&#39;interno di un&#39;applicazione di prodotto.

Tramite [!UICONTROL Permissions] è possibile creare e gestire i ruoli e assegnare le autorizzazioni per le risorse desiderate per tali ruoli. [!UICONTROL Permissions] consente inoltre di gestire le etichette, le sandbox e gli utenti associati a un ruolo specifico.

Se non disponi dei privilegi di amministratore, contatta l’amministratore di sistema per ottenere l’accesso.

Una volta che hai i privilegi di amministratore, vai a [Adobe Experience Cloud](https://experience.adobe.com/) e accedi utilizzando le tue credenziali Adobe. Una volta effettuato l&#39;accesso, viene visualizzata la pagina **[!UICONTROL Overview]** per l&#39;organizzazione per la quale si dispone dei privilegi di amministratore. Questa pagina mostra i prodotti a cui la tua organizzazione è abbonata, insieme ad altri controlli per aggiungere utenti e amministratori all’organizzazione. Seleziona **[!UICONTROL Permissions]** per aprire l&#39;area di lavoro per l&#39;integrazione Experience Platform.

![Immagine che mostra il prodotto Autorizzazioni selezionato in Adobe Experience Cloud](../images/flac-ui/flac-select-product.png)

Viene visualizzata l&#39;area di lavoro Autorizzazioni per l&#39;interfaccia utente di Experience Platform, che si apre nella pagina **[!UICONTROL Overview]**.

## Applicare etichette a un ruolo {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="Che cosa sono le etichette?"
>abstract="Le etichette consentono di categorizzare set di dati e campi in base ai criteri di utilizzo e di accesso applicati a tali dati. Adobe Experience Platform fornisce diverse etichette di utilizzo dei dati <strong>principali</strong> definite da Adobe che coprono un’ampia gamma di restrizioni comuni applicabili alla governance dei dati. Ad esempio, le etichette <strong>S</strong> sensibili, come RHD (Regulated Health Data, dati sanitari regolamentati) consentono di categorizzare i dati riferiti alle informazioni sanitarie protette (PHI, Protected Health Information). Puoi anche definire etichette personalizzate che soddisfino le esigenze della tua organizzazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=it#understanding-data-usage-labels" text="Panoramica sulle etichette di utilizzo dei dati"

I ruoli sono modi per categorizzare i tipi di utenti che interagiscono con l’istanza Experience Platform e sono blocchi predefiniti delle policy di controllo degli accessi. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di cui hanno bisogno.

Per iniziare, seleziona **[!UICONTROL Roles]** dal menu di navigazione a sinistra, quindi seleziona **[!UICONTROL ACME Business Group]**.

![Immagine che mostra il business group ACME selezionato nei ruoli](../images/abac-end-to-end-user-guide/abac-select-role.png)

Selezionare **[!UICONTROL Labels]**, quindi **[!UICONTROL Add Labels]**.

![Immagine che mostra la selezione di Aggiungi etichette nella scheda Etichette](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

Viene visualizzato un elenco di tutte le etichette dell’organizzazione. Selezionare **[!UICONTROL RHD]** per aggiungere l&#39;etichetta per **[!UICONTROL PHI/Regulated Health Data]**, quindi selezionare **[!UICONTROL Save]**.

![Immagine che mostra l&#39;etichetta RHD selezionata e salvata](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>Quando si aggiunge un gruppo organizzazione a un ruolo, tutti gli utenti di tale gruppo verranno aggiunti al ruolo. Eventuali modifiche apportate al gruppo di organizzazioni (utenti rimossi o aggiunti) verranno automaticamente aggiornate all’interno del ruolo.

## Applica etichette ai campi schema {#label-resources}

Dopo aver configurato un ruolo utente con l&#39;etichetta [!UICONTROL RHD], il passaggio successivo consiste nell&#39;aggiungere la stessa etichetta alle risorse che si desidera controllare per tale ruolo.

Dalla navigazione in alto, seleziona il **selettore di applicazioni**, rappresentato dall&#39;icona ![selettore di applicazioni](/help/images/icons/apps.png), quindi seleziona **[!UICONTROL Experience Platform]**.

![Immagine che mostra Experience Platform selezionato dal menu a discesa del commutatore dell&#39;applicazione](../images/abac-end-to-end-user-guide/abac-select-experience-platform.png)

Selezionare **[!UICONTROL Schemas]** dal menu di navigazione a sinistra, quindi selezionare **[!UICONTROL ACME Healthcare]** dall&#39;elenco degli schemi visualizzati.

![Immagine che mostra lo schema ACME Healthcare selezionato dalla scheda Schemi](../images/abac-end-to-end-user-guide/abac-select-schema.png)

Quindi, seleziona **[!UICONTROL Labels]** per visualizzare un elenco che mostra i campi associati allo schema. Da qui è possibile assegnare le etichette a uno o più campi alla volta. Selezionare i campi **[!UICONTROL BloodGlucose]** e **[!UICONTROL InsulinLevel]**, quindi selezionare **[!UICONTROL Apply access and data governance labels]**.

![Immagine che mostra la selezione di BloodGlucose e InsulinLevel e la selezione delle etichette di accesso e governance dei dati](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Edit labels]**, che consente di scegliere le etichette da applicare ai campi dello schema. Per questo caso d&#39;uso, seleziona l&#39;etichetta **[!UICONTROL PHI/ Regulated Health Data]**, quindi seleziona **[!UICONTROL Save]**.

![Immagine che mostra l&#39;etichetta RHD selezionata e salvata](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>Quando un’etichetta viene aggiunta a un campo, viene applicata alla risorsa principale del campo (una classe o un gruppo di campi). Se la classe o il gruppo di campi padre è utilizzato da altri schemi, questi ereditano la stessa etichetta.

## Applicare etichette ai tipi di pubblico

>[!NOTE]
>
>Anche i tipi di pubblico che utilizzano un attributo con etichetta devono essere etichettati, se desideri applicare le stesse restrizioni di accesso.

Una volta completata l’etichettatura dei campi dello schema, puoi iniziare a etichettare i tipi di pubblico.

Seleziona **[!UICONTROL Audiences]** dal menu di navigazione a sinistra nella sezione **[!UICONTROL Customers]**. Viene visualizzato un elenco dei tipi di pubblico disponibili nell’organizzazione. In questo esempio, i due tipi di pubblico seguenti devono essere etichettati in quanto contengono dati sanitari sensibili:

* Glucosio ematico > 100
* Insulina &lt; 50

Seleziona **[!UICONTROL Blood Glucose >100]** (in base al nome del pubblico, non alla casella di controllo) per iniziare a etichettare il pubblico.

![Immagine che mostra la glicemia >100 selezionata dalla scheda Tipi di pubblico](../images/abac-end-to-end-user-guide/abac-select-audience.png)

Viene visualizzata la schermata del segmento **[!UICONTROL Details]**. Seleziona **[!UICONTROL Manage Access]**.

![Immagine che mostra la selezione dell&#39;accesso a Gestisci](../images/abac-end-to-end-user-guide/abac-audience-fields-manage-access.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Apply access and data governance labels]**, che consente di scegliere le etichette da applicare al pubblico. Per questo caso d&#39;uso, seleziona l&#39;etichetta **[!UICONTROL PHI/ Regulated Health Data]**, quindi seleziona **[!UICONTROL Save]**.

![Immagine che mostra la selezione dell&#39;etichetta RHD e il salvataggio in corso](../images/abac-end-to-end-user-guide/abac-select-audience-labels.png)

Ripetere i passaggi precedenti con **[!UICONTROL Insulin <50]**.

>[!NOTE]
>
> Assegnare le etichette create nell&#39;area di lavoro [!UICONTROL Permissions] (come le etichette dei segmenti di cui sopra) a vari oggetti in Adobe Journey Optimizer utilizzando [Controllo dell&#39;accesso a livello di oggetto](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/access-control/object-based-access).&quot;

## Attivare il criterio di controllo degli accessi {#policy}

I criteri di controllo di accesso predefiniti sfrutteranno le etichette per definire quali ruoli utente hanno accesso a risorse Experience Platform specifiche. In questo esempio, l’accesso ai campi dello schema e ai tipi di pubblico verrà negato in tutte le sandbox per gli utenti che non si trovano in un ruolo con le etichette corrispondenti nel campo dello schema.

Per attivare il criterio di controllo degli accessi, selezionare [!UICONTROL Permissions] dal menu di navigazione a sinistra, quindi selezionare **[!UICONTROL Policies]**.

![Elenco dei criteri visualizzato](../images/abac-end-to-end-user-guide/abac-policies-page.png)

Quindi, selezionare i puntini di sospensione (`...`) accanto a **[!UICONTROL Default-Field-Level-Access-Control-Policy]** e un menu a discesa visualizza i controlli per modificare, attivare, eliminare o duplicare il ruolo. Seleziona **[!UICONTROL Activate]** dal menu a discesa.

![Elenco a discesa per attivare i criteri](../images/abac-end-to-end-user-guide/abac-policies-activate.png)

Viene visualizzata la finestra di dialogo attiva criterio, in cui viene richiesto di confermare l’attivazione. Seleziona **[!UICONTROL Confirm]**.

![Attiva finestra di dialogo criteri](../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)

È stata ricevuta la conferma dell&#39;attivazione dei criteri e si ritorna alla pagina [!UICONTROL Policies].

![Attiva conferma criterio](../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

<!-- ## Create an access control policy {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="What are policies?"
>abstract="Policies are statements that bring attributes together to establish permissible and impermissible actions. Every organization comes with a default policy that you must activate to define rules for resources like segments and schema fields. Default policies can neither be edited nor deleted. However, default policies can be activated or deactivated."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=it" text="Manage policies"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Create a policy"
>abstract="Create a policy to define the actions that your users can and cannot take against your segments and schema fields."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=it#create-a-new-policy" text="Create a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configure permissible and impermissible actions for a policy"
>abstract="A <b>deny access to</b> policy will deny users access when the criteria is met. Combined with <b>The following being false</b> - all users will be denied access unless they meet the matching criteria set. This type of policy allows you to protect a sensitive resource and only allow access to users with matching labels. <br>A <b>permit access to</b> policy will permit users access when the criteria are met. When combined with <b>The following being true</b> - users will be given access if they meet the matching criteria set. This does not explicitly deny access to users, but adds a permit access. This type of policy allows you to give additional access to resource and in addition to those users who might already have access through role permissions."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=it#edit-a-policy" text="Edit a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configure permissions for a resource"
>abstract="A resource is the asset or object that a user can or cannot access. Resources can be segments or schemas fields. You can configure write, read, or delete permissions for segments and schema fields."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Edit conditions"
>abstract="Apply conditional statements to your policy to configure user access to certain resources. Select match all to require users to have roles with the same labels as a resource to be permitted access. Select match any to require users to have a role with just one label matching a label on a resource. Labels can either be defined as core or custom labels, with core labels representing labels created and provided by Adobe and custom labels representing labels that you created for your organization."

Access control policies leverage labels to define which user roles have access to specific Experience Platform resources. Policies can either be local or global and can override other policies. In this example, access to schema fields and segments will be denied in all sandboxes for users who don't have the corresponding labels in the schema field.

>[!NOTE]
>
>A "deny policy" is created to grant access to sensitive resources because the role grants permission to the subjects. The written policy in this example **denies** you access if you are missing the required labels.
a
To create an access control policy, select **[!UICONTROL Permissions]** from the left navigation and then select **[!UICONTROL Policies]**. Next, select **[!UICONTROL Create policy]**.

![Image showing Create policy being selected in the Permissions](../images/abac-end-to-end-user-guide/abac-create-policy.png)

The **[!UICONTROL Create new policy]** dialog appears, prompting you to enter a name and an optional description. Select **[!UICONTROL Confirm]** when finished.

![Image showing the Create new policy dialog and selecting Confirm](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

To deny access to the schema fields, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Schema Field]** and then select **[!UICONTROL All]**.

![Image showing Deny access and resources selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

The table below shows the conditions available when creating a policy:

| Conditions | Description |
| --- | --- |
| The following being false| When 'Deny access to' is set, access will be restricted if the user does not meet the criteria selected. |
| The following being true| When 'Permit access to' is set, access will be permitted if the user meets the selected criteria. |
| Matches any| The user has a label that matches any label applied to a resource. |
| Matches all| The user has all labels that matches all labels applied to a resource. |
| Core label| A core label is an Adobe-defined label that is available in all Experience Platform instances.|
| Custom label| A custom label is a label that has been created by your organization.|

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Add resource]**.

![Image showing the conditions being selected and Add resource being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>A resource is the asset or object that a subject can or cannot access. Resources can be segments or schemas.

To deny access to the segments, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Segment]** and then select **[!UICONTROL All]**.

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Save]**.

![Image showing conditions selected and Save being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Select **[!UICONTROL Activate]** to activate the policy, and a dialog appears which prompts you to confirm activation. Select **[!UICONTROL Confirm]** and then select **[!UICONTROL Close]**.

![Image showing the Policy being activated](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png) -->

## Passaggi successivi

Hai completato l’applicazione delle etichette a un ruolo, a campi di schema e a tipi di pubblico. L’agenzia esterna assegnata a questi ruoli non può visualizzare queste etichette e i relativi valori nella vista schema, set di dati e profilo. Inoltre, questi campi non possono essere utilizzati nella definizione del segmento quando si utilizza il Generatore di segmenti.

Per ulteriori informazioni sul controllo degli accessi basato su attributi, vedere la [panoramica sul controllo degli accessi basato su attributi](./overview.md).

Il video seguente ha lo scopo di illustrare il controllo degli accessi basato su attributi e illustra come configurare ruoli, risorse e criteri.

>[!VIDEO](https://video.tv.adobe.com/v/345641?learn=on)
