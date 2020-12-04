

# Databases

## Intro
Wordpress provided various databases for use by default,
but those do not match all of the site needs,
so multiple tables are added.


## Tables
It is recommeneded to put table names in a separate file,
because it is, though infrequently, to make changes to table names.

### care28_userprofile
this table is a supplement to the `{prefix}users` table
offered by wordpress. <br />
1-1-correspondence to care28_users

### care28_posts
exists in wordpress by default,
to filter out user created post,
try `WHERE post_status='publish' AND post_type='post'`

### care28_shops
It was created with 1-1-correspondence to users at first.


### care28_shop_products


### care28_appointments