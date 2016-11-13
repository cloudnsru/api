# API Documentation

## Zones

### [GET] /api/dns/v1/zones/

Get all user zones

    curl -X GET https://cloudns.ru/api/dns/v1/zones/ -u <email>:<secret>

Results

    {
      "items": [
        {
          "id": 15,
          "name": "test2.com",
          "status": "inactive"
        },
        {
          "id": 14,
          "name": "test1.com",
          "status": "inactive"
        },
        {
          "id": 16,
          "name": "test3.com",
          "status": "inactive"
        }
      ],
      "total": 3
    }

### [POST] /api/dns/v1/zones/

Create new zone

Request

     curl -XPOST https://cloudns.ru/dns/v1/zones/ -u {EMAIL}:{SECRET} -d '{"zone": "test4.com"}' -H "Content-Type: application/json"

Response

    {
      "message": "ok",
      "status": 0,
      "zone_id": 20
    }

### [DELETE] /api/dns/v1/zones/{ZONE}

Delete zone

**Request**

    curl -XDELETE https://cloudns.ru/api/dns/v1/zones/{ZONE} -u {EMAIL}:{SECRET}

**Response**

    {
      "status": 0
    }

## Layers

### [GET] /api/dns/v1/zones/{ZONE}

Get Zone details with layers list

**Example**

    curl -XGET https://cloudns.ru/api/dns/v1/zones/{ZONE} -u {EMAIL}:{SECRET}

**Response**

    {
      "items": [
        "default",
        "qojrp"
      ],
      "status": 0,
      "total": 2
    }

### [POST] /api/dns/v1/zones/{ZONE}

Create zone layer

**Example**

    curl -XPOST https://cloudns.ru/api/dns/v1/zones/{ZONE} -u {EMAIL}:{SECRET} -d '{"regions": ["caribbean","polinesia"]}' -H "Content-Type: application/json"

**Response**

    {
      "status": 0
    }

**Error**

    {
      "message": "region already used",
      "status": 1
    }

### [PUT] /api/dns/v1/zones/{ZONE}/{LAYER}

Update layer

**Example**

    curl -XPOST https://cloudns.ru/api/dns/v1/zones/{ZONE}/{LAYER}/regions -u {EMAIL}:{SECRET} -d '{"regions": ["northern_america", "south_america", "eastern_europe"]}' -H "Content-Type: application/json"

**Response**

    {
      "status": 0
    }


### [DELETE] /api/dns/v1/zones/{ZONE}/{LAYER}

Delete zone layer

**Example**

    curl -XDELETE https://cloudns.ru/api/dns/v1/zones/{ZONE}/{LAYER} -u {EMAIL}:{SECRET}

**Response**

    {
      "status": 0
    }


## Records

### [POST] /api/dns/v1/zones/{ZONE}/{LAYER}/records

Create record

    curl -XPOST https://cloudns.ru/api/dns/v1/zones/{ZONE}/{LAYER}/records -u {EMAIL}:{SECRET} -d '{"name": "test2.com", "record_type": "A", "ttl": 7700, "value": "8.8.8.8"}' -H "Content-Type: application/json"


### [DELETE] /api/dns/v1/zones/{ZONE}/{LAYER}/records

Delete record

**Request**

    curl -XDELETE https://cloudns.ru/api/dns/v1/zones/{ZONE}/{LAYER}/records -u {EMAIL}:{SECRET} -d '{"record_id": 3}' -H "Content-Type: application/json"

**Response**

    {
      "message": "record deleted",
      "status": 0
    }

**Error**

    {
      "message": "record not exists",
      "status": 5
    }


### [PUT] /api/dns/v1/zones/{ZONE}/{LAYER}/records

Update record

**Example request**

    curl -XPUT https://cloudns.ru/api/dns/v1/zones/{ZONE}/{LAYER}/records -u {EMAIL}:{SECRET} -d '{"record_id": 4, "host": "test2.com", "ttl": 3600, "value": "7.7.7.7"}' -H "Content-Type: application/json"

**Response**

    {
      "status": 0
    }

## Regions

### [GET] /api/dns/v1/regions/

Get available regions

**Example request**

    curl -X GET https://cloudns.ru/api/dns/v1/regions -u {EMAIL}:{SECRET}

Response

    {
        "items": [
            "all",
            "caribbean",
            ...
            "polinesia"
        ],
        "status": 0,
        "total": 23
    }

### [GET] /api/dns/v1/regions/countries/

Get available countries

**Example request**

    curl -X GET https://cloudns.ru/api/dns/v1/regions/countries/ -u {EMAIL}:{SECRET}

Response

    {
        "countries": [
            {"code": "AF", "name": "Afghanistan"},
            ...
            {"code": "ZW", "name": "Zimbabwe"}
        ],
        "message": "ok",
        "status": 0,
        "total": 249
    }
