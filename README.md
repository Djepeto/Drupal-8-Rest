# Drupal-8-Rest

These are examples taken from:

https://www.drupal.org/docs/8/core/modules/rest/javascript-and-drupal-8-restful-web-services#nodes



-Users

-Nodes

-Comments

-Vocabularies

-Terms


With added some REST calls which may come in handy:

-Block (read-only)

-Contact message

-Contact form (read-only)

-Custom block

-Flag (read-only)

-Paragraph

-Role (read-only)

-Taxonomy term

-Taxonomy vocabulary (read-only)

-Webform submission



First we get our token at the next address:

https://example.com/rest/session/token

yv_kq6fwzL-zv1KKHSXFgpC4hmSbLogdQFPYX8iCu2Y

Or you can do it through the terminal: 

curl --header "Content-type: application/json" --request POST   --data '{"name":"admin", "pass":"admin"}' http://example.com/user/login?_format=json


- USERS

	Login 

	POST: https://example.com/user/login?_format=json
	Content-type: application/json

	We put ?_format=json, and x-csrf token to our url query parameters. 
	
	Headers: 
	Content-type: application/hal+json
	Accept: application/json

	Body: 

	{
		"name": "admin",
		"pass": "password"
	}

	Response:
	
	200 OK
	
	Additional links: 
	http://drupal.mywordpresstips.com/user-login-rest-format.html
	________________________________________________________________________
	
	Logout:
	
	I've tried different examples but can't find the way to logout at the moment. 
	Posted an issue to drupal.org.

	________________________________________________________________________
	
	Retrieve user: 
	GET: https://example.com/user/1?_format=json

	Headers:
	Basic authorization
	
	Response:
	
	200 OK
	________________________________________________________________________

	Register user: 
	I haven't been able to make it work.
	
	At /admin/people/permissions, enable the permission: 
	Access POST on User registration resource, for anonymous and authenticated user. 

	Additional links: 
	https://areatype.com/blog/register-user-drupal-8-rest-api

- NODES

	Create a node:
	POST : http://example.com/entity/node?_format=hal_json
	
	Headers: 
	Accept: application/hal+json 
	Basic auth
	Content-Type: application/hal+json
	X-CSRF-Token
	
	Body: 
	{
	"_links": {
		"type": {
		  "href": "http://example.com/rest/type/node/article"
				}
		},
		"title": [
		{
		  "value": "My first rest article"
		}
		],
		"type": [
		{
		  "value": "article"
		}
		]
	}

	Response: 
	
	201 Created
	
	Add an article and setting the value of an entity reference field - Body:
	{
	"_links": {
		"type": {
		  "href": "http://example.com/rest/type/node/article"
				}
		},
		"title": [
		{
		  "value": "My first rest article"
		}
		],
		"type": [
		{
		  "value": "article"
		}
		],
	"_embedded": {
	"http://example.com/rest/relation/node/article/my_entity_reference_field":
	  [{ 
	  "uuid":[{"value":"yourUUID-xxx-xxxx-xxxx-xxxxxxxxx"}]
	  }]
	 }
	}

	________________________________________________________________________

	Get a node: 
	GET: https://example.com/node/54
	
	No need for auth.
	________________________________________________________________________

	Patch
	I didn't manage to do a patch. 
	
	Additional links:
	https://www.drupal.org/docs/8/core/modules/rest/oauth-patch-example
	________________________________________________________________________

	Delete a node:
	DELETE: https://example.com/node/67?_format=json
	
	Headers: 
	Accept: application/hal+json 
	Basic auth
	X-CSRF-Token
	

- COMMENTS

	Get 
	No auth needed.

	Post
	
	Headers: 
	Basic auth
	X-CSRF-Token

	Delete 
	
	Headers: 
	Basic auth
	X-CSRF-Token

Vocabularies
In D8, vocabularies are "Configuration Entities" and are not yet supported by core's REST. For starters, some folks are working towards GET as a minimum: #2300677: [PP-1] POST/PATCH/DELETE config entities via REST for config entity types that support validation










  


