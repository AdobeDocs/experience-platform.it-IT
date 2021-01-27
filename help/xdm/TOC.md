---
product: experience-platform
audience: user
user-guide-title: Guida del sistema Experience Data Model (XDM)
breadcrumb-title: Guida di Data Model (XDM)
user-guide-description: Utilizza le classi e i mixin Experience Data Model (XDM) per standardizzare i dati dell’esperienza.
translation-type: tm+mt
source-git-commit: baf39df0e03170d6b2b5a151e753d4ad269a43fa
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 23%

---


# Sistema del modello dati esperienza (XDM) {#xdm}

* [Panoramica del sistema XDM](home.md)
* Schemi {#schema}
   * [Nozioni di base sulla composizione dello schema](schema/composition.md)
   * [Best practice per la modellazione dei dati](schema/best-practices.md)
   * [Vincoli del tipo di campo XDM](schema/field-constraints.md)
   * [Dizionario campo XDM](schema/field-dictionary.md)
* Classi {#classes}
   * [Profilo singolo XDM](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
* Mixins {#mixins}
   * Mixer di profilo {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [Dettagli demografici](./mixins/profile/person-details.md)
      * [Dettagli contatto personale](./mixins/profile/personal-details.md)
      * [Dettagli iscrizione segmento](./mixins/profile/segmentation.md)
      * [Dettagli contatto di lavoro](./mixins/profile/work-details.md)
   * Mixer eventi {#event}
      * [Dettagli ID utente finale](./mixins/event/enduserids.md)
      * [Dettagli ambiente](./mixins/event/environment-details.md)
   * [Aggiornamenti dei nomi misti](./mixins/name-updates.md)
* Tipi di dati {#data-types}
   * [Beacon](./data-types/beacon.md)
   * [Dettagli del browser](./data-types/browser-details.md)
   * [Consensi e preferenze](./data-types/consents.md)
   * [Dispositivo](./data-types/device.md)
   * [Indirizzo e-mail](./data-types/email-address.md)
   * [Ambiente](./data-types/environment.md)
   * [Geo](./data-types/geo.md)
   * [Cerchio geografico](./data-types/geo-circle.md)
   * [Coordinate geografiche](./data-types/geo-coordinates.md)
   * [Dettagli interazione geografica](./data-types/geo-interaction-details.md)
   * [Forma geografica](./data-types/geo-shape.md)
   * [Identità](./data-types/identity.md)
   * [Nome della persona](./data-types/person-name.md)
   * [Numero di telefono](./data-types/phone-number.md)
   * [Inserisci contesto](./data-types/place-context.md)
   * [Dettagli POI](./data-types/poi-details.md)
   * [Interazione POI](./data-types/poi-interaction.md)
   * [Indirizzo postale](./data-types/postal-address.md)
* [!UICONTROL Schemas] Interfaccia {#ui}
   * [Panoramica](./ui/overview.md)
   * [Esplora risorse XDM](./ui/explore.md)
   * Creazione e modifica di risorse {#resources}
      * [Schemi](./ui/resources/schemas.md)
      * [Classi](./ui/resources/classes.md)
      * [Mixin](./ui/resources/mixins.md)
      * [Tipi di dati](./ui/resources/data-types.md)
   * Definire i campi {#fields}
      * [Panoramica](./ui/fields/overview.md)
      * [Campi obbligatori](./ui/fields/required.md)
      * [Campi oggetto](./ui/fields/object.md)
      * [Campi Matrice](./ui/fields/array.md)
      * [campi Enum](./ui/fields/enum.md)
      * [Campi identità](./ui/fields/identity.md)
      * [Campi di relazione](./ui/fields/relationship.md)
* API del Registro di sistema dello schema {#api}
   * [Panoramica](api/overview.md)
   * [Introduzione](api/getting-started.md)
   * [Schemi](api/schemas.md)
   * [Comportamenti](api/behaviors.md)
   * [Classi](api/classes.md)
   * [Mixin](api/mixins.md)
   * [Tipi di dati](api/data-types.md)
   * [Descrittori](api/descriptors.md)
   * [Unioni](api/unions.md)
   * [Esporta/Importa](api/export-import.md)
   * [Dati di esempio](api/sample-data.md)
   * [Registro di controllo](api/audit-log.md)
   * [Schemi ad hoc](api/ad-hoc.md)
   * [Appendice](api/appendix.md)
* Tutorial {#tutorials}
   * [Creare uno schema (API)](tutorials/create-schema-api.md)
   * [Creare uno schema (interfaccia utente)](tutorials/create-schema-ui.md)
   * [Definire una relazione tra due schemi (API)](tutorials/relationship-api.md)
   * [Definire una relazione tra due schemi (interfaccia utente)](tutorials/relationship-ui.md)
   * [Creare uno schema ad hoc (API)](tutorials/ad-hoc.md)
* [Guida alla risoluzione dei problemi](troubleshooting-guide.md)
* [Riferimento API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Note sulla versione della piattaforma](https://www.adobe.com/go/platform-release-notes-en)