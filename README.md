# Drupal-8-Rest

Users
Nodes
Comments
Vocabularies
Terms


Users

	Login:
	Radi, csfr token se nabavi preko curl-a
	zatim csrf_token se stavi u headers.

	Logout:
	Pokusao sam ali mi izbacuje razne errore- vraticu se 

	Retrieve user: 
	Radi
	http://192.168.160.6/user/1?_format=json

	Register user: 
	Pokusao sam ali mi izbacuje razne errore- vraticu se 


Nodes

	Create radi 
	http://192.168.160.6/entity/node?Content-type=application/json
	potreban je basic auth 
	X-CSRF-Token takodje, mozemo ga naci na rest/session/token

	Get radi 
	http://192.168.160.6/node/54
	ne treba ni auth ni token ni content type

	Patch
	Nisam uspeo patch - needs more research 

	Delete
	uspeo - potreban je basic auth 
	X-CSRF-Token takodje, mozemo ga naci na rest/session/token
	i accept: application/json


Comments

	Get 
	uspesno - bez authentifikacije

	Post
	uspesno - auth, token

	Delete - uspesno: auth, token


Vocabularies
In D8, vocabularies are "Configuration Entities" and are not yet supported by core's REST. For starters, some folks are working towards GET as a minimum: #2300677: [PP-1] POST/PATCH/DELETE config entities via REST for config entity types that support validation




curl \
  --header "Content-type: application/json" \
  --request POST "http://drupal.d8/user/logout?_format=json"



  curl --header "Content-type: application/json" --request POST   --data '{"name":"admin", "pass":"admin"}' http://192.168.160.6/user/login?_format=json
  curl --header "Content-type: application/json" --request POST   --data '{"name":"admin", "pass":"admin"}' http://192.168.160.6/user/logout?_format=json


  


