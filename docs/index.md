<!--
mkdocs build && git add -A && git commit -m "update" && git push origin master
-->

[//]: # " comment test "
[//]: # "  "

entry point: `wp-json/api/v1/info`

<style>
  .row {
    width: 100%;
    margin: 0;
    display: flex;
  }

  .w50 {
    width: 50%;
  }

  .wrap-break-all {
    white-space: break-spaces;
    word-break: break-all;
  }
</style>

## Example Usage

<div class="row">
  <div class="w50"><pre><code class="wrap-break-all language-json">
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
  </code></pre></div><div class="w50"><pre><code class="wrap-break-all language-json">
empty
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
  </code></pre></div>
</div>

## payload: `query_user`

request

<div class="row">
  <div style="width:50%">
    <pre><code class="wrap-break-all language-json">{
  "type": "query_user",
  "ID": 1,
  "fields": [
    "user_nicename",
    "display_name",
    "usertype",
    "verified",
    "email_verified",
    "license_verified",
    "rating",
    "phone",
    "shop_ID",
    "avatar",
    "license"
  ]
}
    </code></pre>
  </div>
  <div style="width:50%">
    <pre><code class="wrap-break-all language-json">
{
"type": "query_user",
"token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC8xOC4xNjMuNTYuNjUiLCJpYXQiOjE2MDIyMTM3NzQsIm5iZiI6MTYwMjIxMzc3NCwiZXhwIjoxNjAyODE4NTc0LCJkYXRhIjp7InVzZXIiOnsiaWQiOiI1In19fQ.t-8IeKnOAVznpPRh56VZJ1WOnPOXnza1bNE8DqoYU7w" || "ID"/"id": number/string, 
"fields": [
"user_nicename",
"display_name",
"usertype",
"verified",
"email_verified",
"license_verified",
"rating",
"phone",
"shop_ID",
"avatar",
"license"
]
}
</code></pre>

  </div>
</div>

response

```
{
  "body": {
    "user_nicename":"aaabc",
    "display_name":"aaabc",
    "usertype":"agent",
    "verified":0,
    "email_verified":0,
    "license_verified":0,
    "rating":null,
    "phone":"aaabc",
    "shop_ID":1,
    "avatar":"xmBsUbPSP8-avatar1.png",
    "license":"QDb4HBPAbt-license.png"
}

}
```

## payload: `edit_user`

request

<div class="row">
  <div class="w50">
    <pre><code class="wrap-break-all language-json">
    {
      "type": "edit_user",
      "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC8xOC4xNjMuNTYuNjUiLCJpYXQiOjE2MDIyMTM3NzQsIm5iZiI6MTYwMjIxMzc3NCwiZXhwIjoxNjAyODE4NTc0LCJkYXRhIjp7InVzZXIiOnsiaWQiOiI1In19fQ.t-8IeKnOAVznpPRh56VZJ1WOnPOXnza1bNE8DqoYU7w",
      "fields": {
        "user_nicename": "test",
        "display_name": "test",
        "phone": "test",
        "area": "test",
        "avatar": {
          "name": "test.png",
          "format": "png",
          "data": "<base64>"
        },
        "license": {
          "name": "test.png",
          "format": "png",
          "data": "<base64>"
        }
      }
    }
</code></pre>
  </div>
</div>
response
```
{
  "body":"Update success"
}
```

## payload: `query_shop`

request

```
{
  "type": "query_shop",
  "shop_ID":1,
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC8xOC4xNjMuNTYuNjUiLCJpYXQiOjE2MDIyMTM3NzQsIm5iZiI6MTYwMjIxMzc3NCwiZXhwIjoxNjAyODE4NTc0LCJkYXRhIjp7InVzZXIiOnsiaWQiOiI1In19fQ.t-8IeKnOAVznpPRh56VZJ1WOnPOXnza1bNE8DqoYU7w",
  "fields": [
    "owner_ID",
    "description",
    "name"
  ],
  "products": [
    "ID",
    "name",
    "shop_ID",
    "description",
    "thumbnail",
    "area",
    "estate",
    "price",
    "status",
    "lastUpdated"
  ]
}
```

response

```
{
  "body": {
    "owner_ID":24,
    "description":null,
    "name":"shop of agent aaaaaf",
    "products":{
      "6":{
        "ID":6,
        "name":"Product 1 of aaaaaf",
        "shop_ID":31,
        "description":"實積 533 呎",
        "thumbnail":"2020/10/modern-minimalist-bathroom-3115450_960_720.jpg",
        "area":"何文田",
        "estate":"御龍居",
        "price":"1280 萬",
        "status":"可睇",
        "lastUpdated":"2020.10.14"
        },
      "7":{...}
    }
  }
}
```

## payload: `edit_shop`

request

<div class="row">
  <div class="w50">
    <pre><code class="wrap-break-all language-json">
    {
      "type": "edit_shop",
      "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC8xOC4xNjMuNTYuNjUiLCJpYXQiOjE2MDMyNTE5MDUsIm5iZiI6MTYwMzI1MTkwNSwiZXhwIjoxNjAzODU2NzA1LCJkYXRhIjp7InVzZXIiOnsiaWQiOiI1In19fQ.pwB6L997kW_So5YWnXSj_WVdTUvdSOaj9SAfUEI514U",
      "id": 1,
      "fields": {
        "description": "ASFASFASFA",
        "name": "ASDASD"
      }
    }
    </code></pre>
  </div>
  <div class="w50">
    <pre><code class="wrap-break-all language-js">
    {
      "type": "edit_shop",
      "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC8xOC4xNjMuNTYuNjUiLCJpYXQiOjE2MDMyNTE5MDUsIm5iZiI6MTYwMzI1MTkwNSwiZXhwIjoxNjAzODU2NzA1LCJkYXRhIjp7InVzZXIiOnsiaWQiOiI1In19fQ.pwB6L997kW_So5YWnXSj_WVdTUvdSOaj9SAfUEI514U",
      "id": 1, //shop_ID
      "fields": {
        "description": "ASFASFASFA",
        "name": "ASDASD"
      }
    }
    </code></pre>
  </div>
</div>

response

```
{
  "body":"Update success"
}
```

## payload: `query_product`

request

<div class="row">
  <div class="w50">
    <pre><code class="wrap-break-all language-json">{
  type: query_product
  token: token
  "id": [1, 2]
  "fields": [
    "description",
    "name"
  ]
}
    </code></pre>
  </div>
  <div class="w50">
    <pre><code class="wrap-break-all language-js">{
  type: "query_product"
  token: string
  "id": number or number[]
  "fields": [
    "description",
    "name"
  ]
}
    </code></pre>
  </div>
</div>

response

```
{
  "body": {
    "products": {
      "123": {
        name: "asdf"
        description: "asdf"
      },
      "51342": {
        name: "asdaaf"
        description: "asdaaf"
      }
    }
  }
}
```

## payload: `edit_product`

request

<div class="row">
  <div class="w50">
    <pre><code class="wrap-break-all language-json">
    {
      "type": "edit_product",
      "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC8xOC4xNjMuNTYuNjUiLCJpYXQiOjE2MDMyNjM1MzcsIm5iZiI6MTYwMzI2MzUzNywiZXhwIjoxNjAzODY4MzM3LCJkYXRhIjp7InVzZXIiOnsiaWQiOiI1In19fQ.wXDNGlemU4JWdNPFl0xlkyJw6iQsyw9w8xIf069qAw0",
      "id": 53,
      "fields": {
        "name":"test",
        "description":"test",
        "area":"test",
        "estate":"test",
        "price":"test",
        "status":"test",
        "lastUpdated":"test"
        "images":[{
          "name":"test",
          "format":"test",
          "data": "<base64>"
        },
        {...}]
      }
    }
    </code></pre>
  </div>
  <div class="w50">
    <pre><code class="language-json">
    {
      "type": "edit_product",
      "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC8xOC4xNjMuNTYuNjUiLCJpYXQiOjE2MDMyNjM1MzcsIm5iZiI6MTYwMzI2MzUzNywiZXhwIjoxNjAzODY4MzM3LCJkYXRhIjp7InVzZXIiOnsiaWQiOiI1In19fQ.wXDNGlemU4JWdNPFl0xlkyJw6iQsyw9w8xIf069qAw0",
      "id": 53, //product_ID
      "fields": {
        "name":"test",
        "description":"test",
        "area":"test",
        "estate":"test",
        "price":"test",
        "status":"test",
        "lastUpdated":"test"
        "images":[{
          "name":"test",
          "format":"test",
          "data": "<base64>"
        },
        {...}] // So far only accept one image
      }
    }
    </code></pre>
  </div>
</div>
response
```
{
  "body":"Update success"
}
```

## payload: `add_product`

request

```
{
  "type": "add_product",
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC8xOC4xNjMuNTYuNjUiLCJpYXQiOjE2MDI1NzA5NDgsIm5iZiI6MTYwMjU3MDk0OCwiZXhwIjoxNjAzMTc1NzQ4LCJkYXRhIjp7InVzZXIiOnsiaWQiOiI1In19fQ.puM5R6sxCwDp8Q3ujXWdJhZZL1wsjpiP4TpwFFqRh7Y",
  "fields": {
    "name": "ASDASD",
   "description": "ASFASFASFA",
    "area":"Kowloon",
    "estate":"Home",
    "price":"$100",
    "status":"on sale",
    "lastUpdated":"1111",
     "images": [{
        "name": "image1.png",
        "format": "png",
        "data": "iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVR42mNk+M9QDwADhgGAWjR9awAAAABJRU5ErkJggg=="
      }]
  }
}
```

response

```
{
  "body":"Insert success"
}
```

## payload: `del_product`

request

```
{
  "type": "del_product",
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC8xOC4xNjMuNTYuNjUiLCJpYXQiOjE2MDMxNzk1MDUsIm5iZiI6MTYwMzE3OTUwNSwiZXhwIjoxNjAzNzg0MzA1LCJkYXRhIjp7InVzZXIiOnsiaWQiOiI1In19fQ.B1oPUGinQIlu95-COKy_gDogLaGHVPakMXp_4gLvx38",
  "ID": 20
}
```

response

```
{
  "body":"Delete success"
}
```

## payload: `make_appointment`

request

```
{
  "type": "make_appointment",
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC8xOC4xNjMuNTYuNjUiLCJpYXQiOjE2MDMxNzk1MDUsIm5iZiI6MTYwMzE3OTUwNSwiZXhwIjoxNjAzNzg0MzA1LCJkYXRhIjp7InVzZXIiOnsiaWQiOiI1In19fQ.B1oPUGinQIlu95-COKy_gDogLaGHVPakMXp_4gLvx38",
  "ID": 20,
  "fields":{
    "requested_date": "2020-10-20 04:17:50"
  }
}
```

response

```
{
  "body":"Appointment Insert success"
}
```

## datatype: image

<pre><code class="language-json">
{
  "name": "&lt;string>",
  "format": "jpg",
  "data": "base64"
}</code></pre>
