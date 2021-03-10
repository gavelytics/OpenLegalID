# OpenLegalID Proposal

## Description

The OpenLegalID project aims to create a database of civil litigation participants with unique identifiers for judges, lawyers, law firms, and experts. Many companies and lawfirms (us included) cobble together proprietary IDs from private companies to attempt to make a consistant and positive exchange between APIs.

With this publicly accessible database both parties can utilize the same unique identifier for a case participant. Here are a couple of ways that this could be implemented:

## Using an OpenLegalID

Any communication between software applications can reference an OpenLegalID and assuming both parties support them, the specific resource can be returned with no searching or selection. It is up to each implementer to connect their resource with the appropriate OpenLegalID.

## Usage Scenarios

### Legal Data Provider

_A company that posses legal documents and aims to identify participants from those documents._

#### **Getting an ID**

1. Extract a name from the source data.
1. Identify the participant type (judge, lawyer, lawfirm, or expert)
1. Send a request to: `api.openlegalid.org/[TYPE]?name=NAME_TO_FIND`
1. Receive an array of matched participants with some baseline identifying data
1. Choose the most relevant result and store the returned OpenLegalID in your database alongside the document/participant/etc.

## Examples

Looking for **Theresa Beaudet** in the **Los Angeles** jurisdiction:

`api.openlegalid.org/judge?name=theresa%20beaudet&state=ca&county=los%20angeles`

Returns:

```json
[
    {
        "displayName": "Theresa Beaudet",
        "openLegalId": "6e3a2eff-c569-44d0-b90d-7aeb0eec7857",
        "states": ["CA"],
        "counties": ["los angeles"]
    }
]
```

_This needs more identifiable information. Perhaps first year on bench or something else that will never change._
