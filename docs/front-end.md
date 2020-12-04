
<style>
  .wrap-break-all.wrap-break-all {
    white-space: break-spaces;
    word-break: break-all;
  }
</style>

# Front-end

To understand how the front-end in this website works,
it is need to understand how is each request altered
by wordpress hooks.

## wordpress [`parse_request`](https://developer.wordpress.org/reference/hooks/parse_request/#user-contributed-notes) (clickable link)
Hope the following snippet could explain what is actually going on
in `reroute_path.php`:

<pre><code class="wrap-break-all">
&lt;?php
/**
 * If done correctly, this function will run once
 * for each and every process made to the server
 */
function process_request($wp){
  // these two variables is self-explanatory
  $method = $_SERVER["REQUEST_METHOD"];
  $path = parse_url($wp->request, PHP_URL_PATH);

  if($method == "GET"){
    switch($path){
    case "posts/hello-world-post":
?&gt;&lt;html&gt;&lt;body&gt;
Hello world
&lt;/body&gt;&lt;/html&gt;&lt;?php
      exit; // notice server response ends here
    case "posts/about-post":
?&gt;&lt;html&gt;&lt;body&gt;
this is a complete normal php response flow
&lt;/body&gt;&lt;/html&gt;&lt;?php
      exit; // notice server response ends here
    case "another-path":
      echo "echo also works too, it's just php";
      exit;
    }
  }

  // falling back to wordpress default behavior
  return $wp;
}

/**
 * registering the 'parse_request' wordpress hook.
 * run only once during server process, therefore,
 * the 'reroute_path.php' file is, and should be
 * imported in 'functions.php'
 */
add_action("parse_request", process_request);
</code></pre>

with this script, when user navigates
`<server ip or url>/posts/hello-world-post`,
browser would receive
`<html><body>\nHello world\n</body></html>`<br />
similarly, broswer would receive
`echo also works too, it's just php`
when user navigates `<server ip or url>/another-path`<br />
(technically broswer receives a http response which includes
http headers, the text showing about is just the response payload,
but let's skip the [specifics](https://tools.ietf.org/html/rfc7231))

## Javascript front-end framework
Most front-end framework (name any, Angular, React, Vue), when it is not non-SSR (server side rendered) requires you to include one to many scripts
in the result html, like the following
<pre><code class="wrap-break-all">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;script src=<!-- 
-->"&lt;runtime library script from some cdn&gt;"&gt;&lt;/script&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;div id="app"&gt;&lt;/div&gt;
    &lt;script src=<!-- 
-->"&lt;your bundled script from framework&gt;"&gt;<!-- 
 -->&lt;/script&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>

Combining this with `parse_request` above allow us to have
javascript front-end framework running in a wordpress server.

## Svelte
### [what is Svelte?](https://svelte.dev/)
### Why Svelte?
Among these frameworks, Angular, React, Svelte and Vue,
Svelte has least boilerplate, and the learning curve is
not as steep. Most things work intuitively in the sense
of normal javascript other than the fact that Svelte
introduces some weird C-like syntax for template
flow control (for example `{#if condition}div{/if}`)
Precompile runtime script may not be that much beneficial
as they claimed but it is better than none.

## Current State of the server program
As mentioned, `parse_request` plays a major role in connecting
javascript front-end framework and php in wordpress.
In case you still have not realized by now,
each user-navigatable-page from each specific path
is produced with one javascript bundle, as if:

Home page accessible from `<server ip>/` is defined with `Home.js` <br />
About page accessible from `<server ip>/about` is `About.js` <br />
Profile page accessible from `<server ip>/profile` is `Profile.js`
and so on.

The js file is compiled with svelte compiler from corresponding
source file.

`src/pages/Home.svelte` => `public/pages/Home.js` <br />
`src/pages/About.svelte` => `public/pages/About.js` <br />
`src/pages/profile/index.svelte` => `public/pages/Profile.js`

For details how it works, please refer to [`rollup.config.js`](
  https://github.com/valen214/care28_pages/blob/master/rollup.config.js
) (clickable link) <br />
In short, the rollup config file will find either <br />
1. `<page name>.svelte` files under `src/pages` <br />
or <br />
2. `index.svelte` files under `src/pages/<page name>/` <br />
and treat each as a separate page. <br />
Each page would produce one `public/pages/<page name>.js` file as
main entry to be included in the html. All you need
is route each path to their own page in the server, for example

when users access `/home`, return (in `parse_request`):
<pre><code class="wrap-break-all">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;body&gt;
    &lt;script src="/pages/Home.js"&gt;&lt;/script&gt;
  &lt;/body&gt;
&lt;/html&gt; 
</code></pre>


or when users access `/profile`, return (in `parse_request`):
<pre><code class="wrap-break-all">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;body&gt;
    &lt;script src="/pages/Profile.js"&gt;&lt;/script&gt;
  &lt;/body&gt;
&lt;/html&gt; 
</code></pre>

the rest will be done automatically.

Note: the above is just the simplification of the output html,
details please refer to `showSveltePage()` in [`util/svelte_util.php`](
  https://github.com/valen214/care28/blob/master/wp-content/themes/twentytwenty/util/svelte_util.php
)