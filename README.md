# OpenLegalID Proposal

## Goals of the Project

The OpenLegalID resource aims to create common and freely-available unique identifiers for litigation participants that can be shared throughout the industry. It consists of an open source database and api that serves IDs for judges, lawyers, law firms, and experts seeded by well maintained legal data providers.

Positively identifying participants across data services currently requires companies and firms to maintain multiple proprietary IDs from various providers and know when to use which ID for a data request. A singular, common OpenLegalID would vastly simplify workflows and create consistant and confident exchanges between APIs.

## Guiding Principles

The database will include a small amount of identifying data with each participant. The schema will likely be different for each participant type (judges, lawyers, etc). Each participant's accompanying data should follow these principles:

1. Each participant will include a few, simple data points that, in combination with their name, will likely be unique to the person or company. This combination should give a high probability of a positive match.
1. The indentifying information must be data that will _never change_. This could be historical data such as counties they've been active in, bar numbers, first year on the bench, etc. etc.

## Using an OpenLegalID

Any communication between software applications can include an OpenLegalID and assuming both parties support them, the specific resource can be returned with no searching or selection. It is up to each implementer to connect their resource with the appropriate OpenLegalID. The project aims to provide specificly identifying information about the participant _that will never change_. Any data that needs to be curated and maintained is not a good fit for this project.

## Usage Scenarios

### Legal Data Provider

_A company that posses legal documents and aims to identify participants from those documents._

#### **Find an ID**

1. Extract a name from the source data.
1. Identify the participant type (judge, lawyer, lawfirm, or expert)
1. Send a request to: `https://api.openlegalid.org/[TYPE]?name=NAME_TO_FIND`
1. Receive an array of matched participants with some baseline identifying data
1. Choose the most relevant result and store the returned OpenLegalID in your database alongside the document/participant/etc.

### Law Firm

Download the entire particpant data set with accompanying IDs. As users navigate participants through a firm provided interface, data can be requested from all participating service apis by supplying the OpenLegalID. No more managing multiple proprietary ids.

## Examples

Looking for judge **Theresa Beaudet** in the **Los Angeles** jurisdiction:

`https://api.openlegalid.org/judge?name=theresa%20beaudet&state=ca&county=los%20angeles`

Returns:

```json
[
    {
        "name": "Theresa Beaudet",
        "openLegalId": "6e3a2eff-c569-44d0-b90d-7aeb0eec7857",
        "activeLocations": [
            {
                "county": "los angeles",
                "state": "ca"
            }
        ]
    }
]
```

Looking for lawyer **James R. Francis** in the **Broward, Texas** jurisdiction:

`https://api.openlegalid.org/lawyer?name=James%20R.%20Francis&state=tx&county=broward`

Returns:

```json
[
    {
        "name": "James R. Francis",
        "openLegalId": "6e3a2eff-c569-44d0-b90d-7aeb0eec7857",
        "activeLocations": [
            {
                "county": "broward",
                "state": "tx"
            },
            {
                "county": "dallas",
                "state": "tx"
            }
        ],
        "abaNumber": "324985"
    }
]
```

## Contributing

-   If you've created a large, well-maintained data set of litigation participants that has been deduped, it may be a suitable addition to the public api.
-   The project accepts monetary donations If you frequently use the api to power parts of your business. These contributions go to help with server costs, data review, and api development.
