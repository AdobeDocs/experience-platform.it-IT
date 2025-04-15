---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;controllo degli accessi basato su attributi;
title: Guida end-to-end al controllo degli accessi basato su attributi
description: Questo documento fornisce una guida end-to-end sul controllo degli accessi basato su attributi in Adobe Experience Platform
role: Developer
exl-id: 7e363adc-628c-4a66-a3bd-b5b898292394
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 6%

---

# Guida end-to-end per il controllo accesso basato sugli attributi

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

* Il tuo team di marketing interno deve essere in grado di accedere ai **[!UICONTROL dati PHI/ dati sanitari regolamentati]**.
* L&#39;agenzia esterna non dovrebbe essere in grado di accedere ai dati **[!UICONTROL PHI/ dati sanitari regolamentati]**.

A questo scopo, devi configurare ruoli, risorse e criteri.

Effettua le seguenti operazioni:

* [Assegna un&#39;etichetta ai ruoli degli utenti](#label-roles): utilizza l&#39;esempio di un fornitore di assistenza sanitaria (ACME Business Group) il cui gruppo di marketing lavora con agenzie esterne.
* [Assegna un&#39;etichetta alle risorse (campi dello schema e tipi di pubblico)](#label-resources): Assegna l&#39;etichetta **[!UICONTROL PHI/ Dati integrità regolamentati]** alle risorse dello schema e ai tipi di pubblico.
* [Attiva i criteri che li collegheranno](#policy): abilita i criteri predefiniti per impedire l&#39;accesso ai campi dello schema e ai tipi di pubblico collegando le etichette delle risorse alle etichette del tuo ruolo. Gli utenti con etichette corrispondenti avranno quindi accesso al campo e al segmento dello schema in tutte le sandbox.

## Autorizzazioni

[!UICONTROL Autorizzazioni] è l&#39;area di Experience Cloud in cui gli amministratori possono definire ruoli utente e criteri per gestire le autorizzazioni per funzionalità e oggetti all&#39;interno di un&#39;applicazione di prodotto.

Tramite [!UICONTROL Autorizzazioni], puoi creare e gestire i ruoli e assegnare le autorizzazioni per le risorse desiderate per questi ruoli. [!UICONTROL Autorizzazioni] consente inoltre di gestire le etichette, le sandbox e gli utenti associati a un ruolo specifico.

Contatta l&#39;amministratore di sistema per ottenere accesso se non disponi dei privilegi di amministratore.

Una volta ottenuti i privilegi di amministratore, vai su [Adobe Experience Cloud](https://experience.adobe.com/) e accedi con le tue credenziali Adobe Systems. Una volta effettuato l&#39;accesso, viene visualizzata la **[!UICONTROL pagina Panoramica]** per la tua organizzazione per la quale disponi dei privilegi di amministratore. In questa pagina vengono illustrati i prodotti a cui è sottoscritta l&#39;organizzazione, insieme ad altri controlli per aggiungere utenti e amministratori all&#39;organizzazione. Seleziona **[!UICONTROL Autorizzazioni]** per aprire l&#39;area di lavoro per l&#39;integrazione Experience Platform.

![Immagine che mostra il prodotto Autorizzazioni selezionato in Adobe Experience Cloud](../images/flac-ui/flac-select-product.png)

Viene visualizzata l&#39;area di lavoro Autorizzazioni per il interfaccia Experience Platform, che si apre nella **[!UICONTROL pagina Panoramica]** .

## Applicare etichette a un ruolo {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="Che cosa sono le etichette?"
>abstract="Le etichette consentono di categorizzare set di dati e campi in base ai criteri di utilizzo e di accesso applicati a tali dati. Adobe Experience Platform fornisce diverse etichette di utilizzo dei dati di base</strong> definite <strong>dal Adobe Systems, che coprono un&#39;ampia gamma di restrizioni comuni applicabili alla governance dei dati. Ad esempio, le etichette <strong>S</strong> sensibili, come RHD (Regulated Health Data, dati sanitari regolamentati) consentono di categorizzare i dati riferiti alle informazioni sanitarie protette (PHI, Protected Health Information). Puoi anche definire etichette personalizzate che soddisfino le esigenze della tua organizzazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=it#understanding-data-usage-labels" text="Panoramica sulle etichette di utilizzo dei dati"

I ruoli sono modi per categorizzare i tipi di utenti che interagiscono con l’istanza Experience Platform e sono blocchi predefiniti delle policy di controllo degli accessi. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di cui hanno bisogno.

Per iniziare, seleziona **[!UICONTROL Ruoli]** nell&#39;area di navigazione a sinistra, quindi seleziona **[!UICONTROL Gruppo aziendale ACME]**.

![Immagine che mostra il business group ACME selezionato nei ruoli](../images/abac-end-to-end-user-guide/abac-select-role.png)

Quindi, seleziona **[!UICONTROL Etichette]**, quindi seleziona **[!UICONTROL Aggiungi etichette]**.

![Immagine visualizzazione delle etichette Aggiungi selezionate nella scheda Etichette](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

Viene visualizzato un elenco di tutte le etichette presenti nell&#39;organizzazione. Selezionare **[!UICONTROL RHD]** per aggiungere l&#39;etichetta per **[!UICONTROL PHI/Dati]** sanitari regolamentati, quindi selezionare **[!UICONTROL Salva]**.

![Immagine mostra l&#39;etichetta RHD selezionata e salvata](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>Quando si aggiunge un gruppo dell&#39;organizzazione a un ruolo, tutti gli utenti di tale gruppo verranno aggiunti al ruolo. Qualsiasi modifica apportata al gruppo dell&#39;organizzazione (utenti rimossi o aggiunti) verrà aggiornata automaticamente all&#39;interno del ruolo.

## Applica etichette ai campi schema {#label-resources}

Dopo aver configurato un ruolo utente con l&#39;etichetta [!UICONTROL RHD], il passaggio successivo consiste nell&#39;aggiungere la stessa etichetta alle risorse che si desidera controllare per tale ruolo.

Nella parte superiore navigazione selezionare il **commutatore** applicazione, rappresentato dall&#39;icona del ![commutatore](/help/images/icons/apps.png) applicazione, quindi selezionare **[!UICONTROL Experience Platform]**.

![Immagine mostra Experience Platform selezionata dal menu a discesa del commutatore applicazione](../images/abac-end-to-end-user-guide/abac-select-experience-platform.png)

Selezionare **[!UICONTROL Schemi]** dal navigazione sinistro, quindi selezionare **[!UICONTROL ACME Healthcare]** dall&#39;elenco degli schemi visualizzati.

![Immagine che mostra lo schema ACME Healthcare selezionato dalla scheda Schemas](../images/abac-end-to-end-user-guide/abac-select-schema.png)

Quindi, seleziona **[!UICONTROL Etichette]** per visualizzare un elenco con i campi associati allo schema. Da qui è possibile assegnare le etichette a uno o più campi alla volta. Selezionare i campi **[!UICONTROL BloodGlucose]** e **[!UICONTROL InsulinLevel]**, quindi selezionare **[!UICONTROL Applica etichette di accesso e governance dei dati]**.

![Immagine che mostra la selezione di BloodGlucose e InsulinLevel e la selezione delle etichette di accesso e governance dei dati](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Modifica etichette]**, che consente di scegliere le etichette da applicare ai campi dello schema. Per questo caso d&#39;uso, seleziona l&#39;etichetta **[!UICONTROL PHI/ Regulated Health Data]**, quindi seleziona **[!UICONTROL Salva]**.

![Immagine che mostra l&#39;etichetta RHD selezionata e salvata](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>Quando un’etichetta viene aggiunta a un campo, viene applicata alla risorsa principale del campo (una classe o un gruppo di campi). Se la classe o il gruppo di campi padre è utilizzato da altri schemi, questi ereditano la stessa etichetta.

## Applicare etichette ai tipi di pubblico

>[!NOTE]
>
>Anche i tipi di pubblico che utilizzano un attributo con etichetta devono essere etichettati, se desideri applicare le stesse restrizioni di accesso.

Una volta completata l’etichettatura dei campi dello schema, puoi iniziare a etichettare i tipi di pubblico.

Seleziona **[!UICONTROL Tipi di pubblico]** dalla barra di navigazione a sinistra nella sezione **[!UICONTROL Clienti]**. Viene visualizzato un elenco dei tipi di pubblico disponibili nell’organizzazione. In questo esempio, i due tipi di pubblico seguenti devono essere etichettati in quanto contengono dati sanitari sensibili:

* Glucosio ematico > 100
* Insulina &lt; 50

Seleziona **[!UICONTROL Glucosio ematico >100]** (in base al nome del pubblico, non alla casella di controllo) per iniziare a etichettare il pubblico.

![Immagine che mostra la glicemia >100 selezionata dalla scheda Tipi di pubblico](../images/abac-end-to-end-user-guide/abac-select-audience.png)

Viene visualizzata la schermata **[!UICONTROL Dettagli]** del segmento. Seleziona **[!UICONTROL Gestisci accesso]**.

![Immagine che mostra la selezione dell&#39;accesso a Gestisci](../images/abac-end-to-end-user-guide/abac-audience-fields-manage-access.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Applica etichette di accesso e governance dei dati]**, che consente di scegliere le etichette da applicare al pubblico. Per questo caso d&#39;uso, seleziona l&#39;etichetta **[!UICONTROL PHI/ Regulated Health Data]**, quindi seleziona **[!UICONTROL Salva]**.

![Immagine che mostra la selezione dell&#39;etichetta RHD e il salvataggio in corso](../images/abac-end-to-end-user-guide/abac-select-audience-labels.png)

Ripetere i passaggi precedenti con **[!UICONTROL Insulina &lt;50]**.

>[!NOTE]
>
> Assegnare le etichette create nell&#39;area di lavoro [!UICONTROL Autorizzazioni] (come le etichette dei segmenti di cui sopra) a vari oggetti in Adobe Journey Optimizer utilizzando [Controllo dell&#39;accesso a livello di oggetto](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/object-based-access).&quot;

## Attivare il criterio di controllo degli accessi {#policy}

I criteri di controllo di accesso predefiniti sfrutteranno le etichette per definire quali ruoli utente hanno accesso a risorse Experience Platform specifiche. In questo esempio, l’accesso ai campi dello schema e ai tipi di pubblico verrà negato in tutte le sandbox per gli utenti che non si trovano in un ruolo con le etichette corrispondenti nel campo dello schema.

Per attivare il criterio di controllo degli accessi, selezionare [!UICONTROL Autorizzazioni] nell&#39;area di navigazione a sinistra, quindi selezionare **[!UICONTROL Criteri]**.

![Elenco dei criteri visualizzato](../images/abac-end-to-end-user-guide/abac-policies-page.png)

Selezionare quindi i puntini di sospensione (`...`) accanto a **[!UICONTROL Default-Field-Level-Access-Control-Policy]** e un elenco a discesa visualizza i controlli per modificare, attivare, eliminare o duplicare il ruolo. Seleziona **[!UICONTROL Attiva]** dal menu a discesa.

![Elenco a discesa per attivare i criteri](../images/abac-end-to-end-user-guide/abac-policies-activate.png)

Viene visualizzata la finestra di dialogo attiva criterio, in cui viene richiesto di confermare l’attivazione. Seleziona **[!UICONTROL Conferma]**.

![Attiva finestra di dialogo criteri](../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)

Si riceve la conferma dell regola attivazione e si ritorna alla [!UICONTROL pagina Criteri] .

![Attiva regola conferma](../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

<!-- ## Create an access control policy {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="What are policies?"
>abstract="Policies are statements that bring attributes together to establish permissible and impermissible actions. Every organization comes with a default policy that you must activate to define rules for resources like segments and schema fields. Default policies can neither be edited nor deleted. However, default policies can be activated or deactivated."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html" text="Manage policies"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Create a policy"
>abstract="Create a policy to define the actions that your users can and cannot take against your segments and schema fields."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html#create-a-new-policy" text="Create a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configure permissible and impermissible actions for a policy"
>abstract="A <b>deny access to</b> policy will deny users access when the criteria is met. Combined with <b>The following being false</b> - all users will be denied access unless they meet the matching criteria set. This type of policy allows you to protect a sensitive resource and only allow access to users with matching labels. <br>A <b>permit access to</b> policy will permit users access when the criteria are met. When combined with <b>The following being true</b> - users will be given access if they meet the matching criteria set. This does not explicitly deny access to users, but adds a permit access. This type of policy allows you to give additional access to resource and in addition to those users who might already have access through role permissions."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html#edit-a-policy" text="Edit a policy"

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

![Image showing the Policy being activated ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png) -->

## Passaggi successivi

Hai completato il applicazione delle etichette per un ruolo, campi schema e audience. L&#39;agenzia esterna assegnata a questi ruoli non può visualizzare queste etichette e i relativi valori nella visualizzazione schema, set di dati e profilo. Inoltre, è possibile utilizzare questi campi nella definizione del segmento quando si utilizza il Generatore di segmenti.

Per ulteriori informazioni sul controllo accesso basato su attributi, vedere Cenni preliminari](./overview.md) sul [controllo accesso basato su attributi.

Il video seguente ha lo scopo di illustrare il controllo degli accessi basato su attributi e illustra come configurare ruoli, risorse e criteri.

>[!VIDEO](https://video.tv.adobe.com/v/345641?learn=on)
