

<!--
mkdocs build && git add -A && git commit -m "update" && git push origin master
-->


[//]: # ( comment test )

[//]: # (  )


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
  "token": "asdf",
  "fields": [
    "ID",

    
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
    "license",

    
    "abc"
  ],
}
    </code></pre>
  </div>
  <div style="width:50%">
    <pre><code class="wrap-break-all language-json">{
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
    </code></pre>
  </div>
</div>

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
<div class="row">
  <div class="w50">
    <pre><code class="wrap-break-all language-json">{
  "type": "edit_user",
  "token": "asdf",
  "fields": {
    &nbsp;
    "user_nicename": "&lt;name&gt;",
    "display_name": "&lt;name&gt;",
    &nbsp;
    &nbsp;
    "phone": "&lt;phone&gt;",
    &nbsp;
    "avatar": {
      "name": "abc.png",
      "format": "png",
      "data": "&lt;base64&gt;",
    },
    "license": {
      "name": "license.png",
      "format": "png",
      "data": "&lt;base64&gt;",
    }
    &nbsp;
  }
}</code></pre>
  </div>
  <div class="w50">
    <pre><code class="language-json">{
  "type": "edit_user",
  "token": "asdf",
  "fields": {  // exhaustive
    // from wp_users
    "user_nicename": "&lt;name&gt;",
    "display_name": "&lt;name&gt;",
    &nbsp;
    // from wp_userprofile
    "phone": "&lt;phone&gt;",
    &nbsp;
    "avatar": <a href="#datatype-image"><i>&lt;image&gt;</i></a>,
    "license": <a href="#datatype-image"><i>&lt;image&gt;</i></a>
    &nbsp;
  }
}</code></pre>
  </div>
</div>
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
    <pre><code class="wrap-break-all language-json">{
  "type": "edit_product",
  "token": "asdf",
  "id": 123,
  "fields": {
    "description": "ASFASFASFA",
    "name": "ASDASD",
    "images": [{
        "name": "image1.png",
        "format": "png",
        "data": "iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVR42mNk+M9QDwADhgGAWjR9awAAAABJRU5ErkJggg=="
      }, {
        "name": "image2.gif",
        "format": "gif",
        "data": "R0lGODlhAQABAIAAAP///wAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw=="
      }
    ]
    "abc": "ASFASF",
  }
}</code></pre>
  </div>
  <div class="w50">
    <pre><code class="language-json">{
  "type": "edit_product",
  "token": "asdf",
  "id": 123,
  "fields": {
    "description": "ASFASFASFA",
    "name": "ASDASD",
    "images": []
    "abc": "ASFASF",
  }
}</code></pre>
  </div>
</div>
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



## datatype: image
<pre><code class="language-json">
{
  "name": "&lt;string>",
  "format": "jpg",
  "data": "base64"
}</code></pre>