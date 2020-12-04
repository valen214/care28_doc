<!--
mkdocs build && git add -A && git commit -m "update" && git push origin master
-->

## About the website

The website base project is wordpress,
which is running with php.
Due to the difficulty in routing paths to
different pages with wordpress,
most request (including serving HTML, backend rest api)
are being handled separately with
a custom php function, inside [`reroute_path.php`](https://github.com/valen214/care28/blob/master/wp-content/themes/twentytwenty/reroute_path.php#L5) (clickable link).
This file is included by `functions.php`.


This file registered a wordpress action hook [`parse_request`](https://developer.wordpress.org/reference/hooks/parse_request/).
Each and every request made to the wordpress server
would run through this function.
So if `exit` is encountered in the middle of the this function,
the respond to any request made will terminate.
If not, the function would return the parameter given, namely `$wp`,
and fall back to wordpress default behavior.

### Back-end
`v1` backend server is running with php on the same server process as wordpress,
`v2` is running with [ExpressJS](http://expressjs.com/) in a different, separated process,
all backend request are registered with [`register_rest_route`](https://developer.wordpress.org/reference/functions/register_rest_route/) in [`main.php`](https://github.com/valen214/care28/blob/master/wp-content/themes/twentytwenty/api/main.php),
which again is imported by `functions.php`.

### Front-end
[front-end](/front-end)

## About the mobile app
Keywords: React Native, Expo, Electron?

## About this Doc
Keywords: Mkdocs