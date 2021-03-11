# OpenLegalID Proposal

## Goals of the Project

The OpenLegalID project aims to create a database of civil litigation participants with unique identifiers for judges, lawyers, law firms, and experts. Many companies and lawfirms (us included) cobble together proprietary IDs from private companies to attempt to make a consistant and positive exchange between APIs.

With this publicly accessible database all parties can utilize the same unique identifier for a case participant. Here are a couple of ways that this could be implemented:

## Using an OpenLegalID

Any communication between software applications can reference an OpenLegalID and assuming both parties support them, the specific resource can be returned with no searching or selection. It is up to each implementer to connect their resource with the appropriate OpenLegalID. The project aims to provide specificly identifying information about the participant _that will never change_. Any data that needs to be curated and maintained is not a good fit for this project.

## Usage Scenarios

### Legal Data Provider

_A company that posses legal documents and aims to identify participants from those documents._

#### **Getting an ID**

1. Extract a name from the source data.
1. Identify the participant type (judge, lawyer, lawfirm, or expert)
1. Send a request to: `https://api.openlegalid.org/[TYPE]?name=NAME_TO_FIND`
1. Receive an array of matched participants with some baseline identifying data
1. Choose the most relevant result and store the returned OpenLegalID in your database alongside the document/participant/etc.

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

## Guiding Principles

The database will include a small amount of identifying data with each participant. The schema will likely be different for each participant type (judges, lawyers, etc). Each entities accompanying data should follow these principles:

1. Each entity will include a few, simple data points that, in combination with their name, will likely be unique to the person or company. This combination should give a high probability of a positive match.
1. The indentifying information must be data that will _never change_. This could be historical data such as counties they've been active in, bar numbers, first year on the bench, etc. etc.
