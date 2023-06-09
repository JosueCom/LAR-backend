# REST API Documentation

## Overview
This document describes the public REST API for accessing and manipulating data on our service. The API is designed to be simple and easy to use, with predictable and resource-oriented URLs.

## Base URL
All API requests should be made to the base URL such as: `http://127.0.0.1:5000`

## Resources
Our API provides access to several resources, including:

- **Index**: Returns a message indicating that the API is working.
- **Test**: Returns location data based on the provided address.
- **Adds**: Returns location data based on the provided address and database collections.
- **Locations**: Returns location data based on the provided latitude, longitude, radius, and database collections.

## Endpoints
Here are some example endpoints for our API:

- `GET /`: Returns a message indicating that the API is working.
- `GET /test/:adds`: Returns location data based on the provided address.
- `GET /adds/:adds/:dbs`: Returns location data based on the provided address and database collections.
- `GET /locs/:lat,:lon,:radius/:dbs`: Returns location data based on the provided latitude, longitude, radius, and database collections.

## Request Parameters
The `dbs` parameter in both `/adds/:adds/:dbs` and `/locs/:lat,:lon,:radius/:dbs` endpoints represents a comma-separated list of integers representing database collections. These integers correspond to unique private IDs for a list of databases. For example, a `dbs` value of `"1,2,4"` would correspond to the collections `"Fire Stations"`, `"Hospitals"`, and `"Schools"`. To learn more, visit the [database directory](../config.json).

## Request and Response Format
All requests and responses are in JSON format. Here's an example request to get location data:

```
GET /locs/41.672747140,-70.98471383,10000/1,2
```

And here's an example response:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
    "dbs": {
        "FIRESTATIONS": [
            {
                "geometry": {
                    "coordinates": [-70.98281860299994, 41.63984680200008],
                    "type": "Point"
                }
            },
            ...
        ],
        "HOSPITALS": [
            {
                "geometry": {
                    "coordinates": [-70.98471383, 41.6727471400001],
                    "type": "Point"
                }
            },
            ...
        ]
    },
    "location": {
        "latitude": 41.67274714,
        "longitude": -70.98471383,
        "radius": 10000.0
    }
}
```
