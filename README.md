# Event Notifications Data/Publication Linkages

## Examples

### `examples/event_notification_1.jsonld`

A COAR Notify [Event Notification](https://www.eventnotifications.net) sent by a "My Research Data Linker" **actor** to the "Ghent University Academic Bibliography" **target**.

The notification announces for the Biblio artifact https://biblio.ugent.be/publication/01HGZ2RXXGK39KV1T0NJV1W6CX a related data set at https://doi.org/10.5281/ZENODO.10017325.

Documentation of the fields, see [COAR Notify](https://coar-notify.net/specification/1.0.0/announce-relationship/).

These notifications are sent by the **actor** to the inbox http://biblio.ugent.be/inbox/ of the *target* using a HTTP POST:

```
curl -X POST -H 'Content-Type: application/ld+json' \
    --data-binary '@examples/event_notification_1.jsonld' \
    http://biblio.ugent.be/inbox/
```

### `examples/event_log.jsonld`

An event log for the Biblio artifact https://biblio.ugent.be/publication/01HGZ2RXXGK39KV1T0NJV1W6CX recording changes to the state of an artifact:

- `as:Create` : creation of the artifact
- `as:Update` : update of the artifact (or its metadata)
- `as:Remove` : removal of the artifact

or, changes that pertain to value-adding services for an artifact:

- `as:Offer` : an offer of an artifact to a web service
- `as:Accept` : a web service accepting offering services on an artifact
- `as:Reject` : a web service rejecting the artifact
- `as:Undo`: the undo of an offer
- `as:Announce`: a web service announcing a some information (or a service result) pertaining to an artifact

### What an artifact?

An artifact in the context of Biblio is in general a complex object that is identified by the biblio record identifier. It is the intellectual entity that is described by that identifier.

To talk about the artifact as a whole use its record id in the object position:

```
"object" : {
    "id": "https://biblio.ugent.be/publication/01HGZ2RXXGK39KV1T0NJV1W6CX"
    ...
}
```

To talk about a part of an artifact, using the COAR Notify context, it is possible to add an `ietf:item` to the object:

```
"object" : {
    "id": "https://biblio.ugent.be/publication/01HGZ2RXXGK39KV1T0NJV1W6CX",
    "ietf:item": {
      "id": "https://biblio.ugent.be/publication/01HGZ2RXXGK39KV1T0NJV1W6CX/file/01HGZ306AMP301PHQN7DVHXD9X.pdf",
      "mediaType": "application/pdf",
      "type": "Article"
    },
    ...
}
```