

<!--
mkdocs build && git add -A && git commit -m "update" && git push origin master
-->


[//]: # ( comment test  )



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
  "fields": [ // exhaustive
    "ID",

    // from wp_users
    "user_nicename",
    "display_name",

    // from wp_userprofile
    "usertype",
    "verified",
    "email_verified",
    "license_verified",
    "rating",
    "phone",
    "shop_ID",

    "avatar", // base64 format without prefix
    "license", // token is required

    // fake
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
  "fields": {  // exhaustive
    // from wp_users
    "user_nicename": "<name>",
    "display_name": "<name>",

    // from wp_userprofile
    "phone": "<phone>",

    "avatar": "<base64>",
    "license": "<base64>"
  
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
  "id": "asdf", (required)
  "fields": [
    // from table wp_shops
    "owner_ID",
    "description",
    "name",

    "abc",
  ],
  // from table wp_shop_products
  "products": [
    "ID", *optional*
    "name",
    "shop_ID",
    "description"
  ]
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
    },
    "products": {
      "<id>": {
        "ID": "<id>",
        "name": "ASD"
      }
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

    "products": {
      "<id>": {
        "description": "ds",
        "name": "asdf",

      }
    }
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
