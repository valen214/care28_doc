


entry point: `wp-json/api/v1/info`

## Example Usage
```
fetch("//wp-json/api/v1/info", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({
        "type": "query_user",
        "token": "asdf",
        "fields": [
          "shop_description",
          "shop_name",
          "abc",
        ],
    })
}).then(res => res.json()).then(res => {
    console.log(res);
})
```


## payload: `query_user`
request
```
{
  "type": "query_user",
  "token": "asdf",
  "fields": [
    "ID",
    "usertype",
    "verified",
    "email_verified",
    "license_verified",
    "rating",
    "phone",
    "shop_ID",
    "abc"
  ],
}
```
response
```
{
  "body": {
    "fields: {
      "ID": 121,
      "usertype": "client",
      ...,
      "abc": null,
    }
  }
}
```



## payload: `edit_user`
request
```
{
  "type": "edit_user",
  "token": "asdf",
  "fields": {
    "shop_description": "ASFASFASFA",
    "shop_name": "ASDASD",
    "abc": "ASFASF",
  }
}
```
response
```
{
  "body": "ok"
}
```



## payload: `query_shop`
request
```
{
  "type": "query_shop",
  "token": "asdf",
  "fields": [
    "description",
    "name",
    "abc",
  ],
}
```
response
```
{
  "body": {
    "fields: {
      "description": "asdf",
      "name": "asdf",
      "abc": null,
    }
  }
}
```



## payload: `edit_shop`
request
```
{
  "type": "edit_shop",
  "token": "asdf",
  "id": *optional*
  "fields": {
    "description": "ASFASFASFA",
    "name": "ASDASD",
    "abc": "ASFASF",
  }
}
```
response
```
{
  "body": "ok"
}
```


## payload: `query_product`
request
```
{
  type: query_product
    token: token
    products: {
    "123": {
      fields: [
        name
        description
      ]
    },
    "51342": {
      fields: [ description ]
    }
  }
}
```

response
```
{
  "body": {
    "products": {
      "123": {
        fields: {
          name: "asdf"
        }
      },
      "51342": {
        fields: {
          description: "asdf"
        }
      }
    }
  }
}
```



## payload: `edit_product`
request
```
{
  "type": "edit_product",
  "token": "asdf",
  "id": 123,
  "fields": {
    "description": "ASFASFASFA",
    "name": "ASDASD",
    "abc": "ASFASF",
  }
}
```
response
```
{
  "body": "ok"
}
```


## payload: `add_product`
request
```
{
  "type": "add_product",
  "token": "asdf",
  "fields": {
    "description": "ASFASFASFA",
    "name": "ASDASD",
    "abc": "ASFASF",
  }
}
```
response
```
{
  "body": "ok"
}
```
