---
title: Gruppo di campi schema Dettagli membro assistenza sanitaria
description: Questo documento fornisce una panoramica del gruppo di campi schema Dettagli membro assistenza sanitaria.
exl-id: 43ba025e-2acf-4cb7-8487-e6c7c7240867
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 3%

---

# [!UICONTROL Dettagli dei membri del settore sanitario] gruppo di campi schema

[!UICONTROL Dettagli dei membri del settore sanitario] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) che acquisisce i dettagli di una persona che ha o riceverà servizi o cure mediche, come le informazioni di contatto, il medico di base e le informazioni sul piano.

![Struttura del gruppo di campi](../../images/field-groups/healthcare-member-details/structure.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL Indirizzo postale]](../../data-types/postal-address.md) | Indirizzo di fatturazione della persona. |
| `faxPhone` | [[!UICONTROL Numero di telefono]](../../data-types/phone-number.md) | Numero di fax della persona. |
| `homeAddress` | [[!UICONTROL Indirizzo postale]](../../data-types/postal-address.md) | Indirizzo dell&#39;abitazione della persona. |
| `homePhone` | [[!UICONTROL Numero di telefono]](../../data-types/phone-number.md) | Numero di telefono dell&#39;abitazione della persona. |
| `mailingAddress` | [[!UICONTROL Indirizzo postale]](../../data-types/postal-address.md) | Indirizzo postale della persona. |
| `memberDetails` | Oggetto | Oggetto che contiene informazioni dettagliate sugli attributi e sulle relazioni della persona relativi all’assistenza sanitaria. Consulta la [sottosezione successiva](#memberDetails) per ulteriori informazioni sulla struttura dell&#39;oggetto. |
| `mobilePhone` | [[!UICONTROL Numero di telefono]](../../data-types/phone-number.md) | Numero di telefono cellulare della persona. |
| `person` | [[!UICONTROL Persona]](../../data-types/person.md) | Un singolo attore, contatto o proprietario correlato all’appartenenza all’assistenza sanitaria della persona. |
| `personalEmail` | [[!UICONTROL Indirizzo e-mail]](../../data-types/email-address.md) | Indirizzo e-mail personale della persona. |
| `shippingAddress` | [[!UICONTROL Indirizzo postale]](../../data-types/postal-address.md) | Indirizzo di spedizione della persona. |

{style="table-layout:auto"}

## `memberDetails` {#memberDetails}

`memberDetails` è un oggetto che contiene informazioni dettagliate sugli attributi e sulle relazioni del soggetto con riferimento all’assistenza sanitaria. La struttura di `memberDetails` è descritto di seguito.

![struttura memberDetails](../../images/field-groups/healthcare-member-details/memberDetails.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `emergencyContact` | Oggetto | Acquisisce i seguenti dettagli di contatto di emergenza per la persona: <ul><li>`fullName`: (stringa) nome completo del contatto di emergenza.</li><li>`phone`: (stringa) numero di telefono del contatto di emergenza.</li><li>`relationshipToMember`: (stringa) relazione del contatto di emergenza con la persona.</li></ul> |
| `medications` | Array di oggetti | Elenca i dettagli dei farmaci attuali e passati associati alla persona. Ogni elemento array è un oggetto che acquisisce i dettagli seguenti: <ul><li>`refillLocation`: ([[!UICONTROL Indirizzo postale]](../../data-types/postal-address.md)a) Il punto di ricarica del medicinale.</li><li>`ID`: (Stringa) ID medicinale.</li><li>`isCurrent`: (booleano) indica se il medicinale è attuale o passato.</li><li>`numberOfRefills`: (Numero intero) il numero di riempimenti prescritti dal fornitore di questo medicinale.</li><li>`startDate`: (DateTime) la data in cui la persona ha iniziato a prendere il medicinale.</li></ul> |
| `multipleBirth` | Oggetto | Acquisisce i dettagli relativi a più nascite: <ul><li>`isMultipleBirth`: (booleano) indica se la persona ha dato più nascite.</li><li>`multipleBirthNumber`: (Numero intero) il numero di bambini nati se `isMultipleBirth` è vero.</li></ul> |
| `plans` | Array di oggetti | Elenca i dettagli dei piani medici correnti e passati associati alla persona. Ogni elemento array è un oggetto che acquisisce i dettagli seguenti: <ul><li>`coverageEndDate`: (DateTime) la data in cui termina la copertura del piano.</li><li>`coverageStartDate`: (DateTime) la data di inizio della copertura del piano.</li><li>`isActive`: (booleano) indica se il piano è attivo.</li><li>`planId`: (Stringa) ID del piano.</li></ul> |
| `primaryCarePhysicians` | Array di oggetti | Elenca i dettagli dei medici di base associati alla persona. Ogni elemento array è un oggetto che acquisisce i dettagli seguenti: <ul><li>`endDate`: (DateTime) la data in cui il medico di base ha terminato le cure per la persona.</li><li>`fullname`: (Stringa) il nome completo del medico.</li><li>`providerId`: (Stringa) un identificatore univoco per il medico.</li><li>`startDate`: (DateTime) la data in cui il medico di base ha iniziato a prendersi cura della persona.</li></ul> |
| `specialists` | Array di oggetti | Elenca i dettagli degli specialisti sanitari associati alla persona. Ogni elemento array è un oggetto che acquisisce i dettagli seguenti: <ul><li>`fullname`: (Stringa) nome completo dello specialista.</li><li>`providerId`: (Stringa) identificatore univoco dello specialista.</li><li>`specialty`: (Stringa) la specialità del fornitore (ad esempio anestesia, urologia, radiologia, dermatologia e così via).</li></ul> |
| `beneficiaryRelationship` | Stringa | Il rapporto del beneficiario con il membro dell’assistenza sanitaria se la persona è a carico (esempi includono sé stesso, coniuge, figlio e così via). |
| `billingAccountID` | Stringa | Un identificatore univoco per l’account di fatturazione della persona. |
| `dateAgeCollected` | DateTime | La data in cui è stata raccolta l’età della persona. |
| `deceasedDate` | DateTime | La data in cui la persona è deceduta. |
| `isDeceased` | Booleano | Indica se la persona è deceduta. |
| `isDependent` | Booleano | Indica se la persona è una persona dipendente. |
| `nationality` | Stringa | Il rapporto giuridico tra la persona e il suo stato, rappresentato utilizzando il codice ISO 3166-1 Alpha-2. |
| `preferredAvailability` | Stringa | Il giorno e l’ora di disponibilità preferiti per un appuntamento. |
| `primaryMemberID` | Stringa | Un identificatore univoco dell’abbonato primario se la persona è una persona dipendente. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

Per ulteriori informazioni su come questo gruppo di campi può essere utilizzato per gli eventi comuni, consulta la documentazione sullo schema di settore. [casi di utilizzo del settore sanitario](../../schema/industries/healthcare.md).
