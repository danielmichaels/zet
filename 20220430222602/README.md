# pfSense-api v1.4.0

Some excellent news, `pfsense-api` has been updated to `v1.4.0` which brings 
several fantastic changes.

Highlights:

- Support for pfSense+ (this could be a catalyst for many new customers)
- Basic Auth instead of sending in the body* (see notes)
- OpenAPI swagger endpoint (previously it was a markdown doc)
- API IP white listing (might make HTTP access more palatable)


**Notes**

* ***Basic Auth*** is better than munging a body to pass authentication but I
cannot switch completely for backward compatibility reasons. 

Tags:

    #pfsense #mudmap
