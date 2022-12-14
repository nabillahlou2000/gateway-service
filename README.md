# gateway-service
Gateway web service (4/6).
Ce fichier readme.md résume l'entiereté des étapes allant de la création des différents web services,à la création de la gateway,du service de registre Eureka et la partie front-end avec Angular.

#Partie 1 : Création des web services:
  #Web service customer:
  
 - Création de la classe 'Customer' qui sera la classe dédiée au client et représenté par son id,nom et mot de passe:
  ![Capture d’écran (113)](https://user-images.githubusercontent.com/111126484/207467540-3c5a7cc5-fedf-4499-aea1-863bb803b6db.png)
  - Création de Customer Repository:
  ![Capture d’écran (114)](https://user-images.githubusercontent.com/111126484/207467923-74ce63d9-96a1-4cc3-ace8-e23af728e28d.png)
  - Notre fichier 'CustomerServiceApplication' va nous permettre de créer quelques clients afin de tester notre partie backend et frontend:
  ![Capture d’écran (115)](https://user-images.githubusercontent.com/111126484/207468172-659ff8c2-e86f-43ed-97e5-7fa193770b0f.png)
  - Le fichier application.propreties va nous permettre d'allouer un port à notre web service (dans ce cas 8081),le nom du service,préciser la base de données et préciser si le web service doit s'authentifier ou non avec l'attribut 'spring.cloud.discovery.enabled'
  ![Capture d’écran (116)](https://user-images.githubusercontent.com/111126484/207468849-b045ac5b-5c90-43b8-a7d6-aca2a39fe1b8.png)
  
  #Web service inventory:
- Création de la classe 'Inventory' qui sera la classe dédiée au produit et représenté par son id,nom,prix et quantité:
![Capture d’écran (119)](https://user-images.githubusercontent.com/111126484/207469452-50142390-ee61-4bf9-b4a1-2f44851da176.png)
- Création de Product Repository:
![Capture d’écran (118)](https://user-images.githubusercontent.com/111126484/207469609-162cd150-51de-44f8-9d42-de096412bd9d.png)
- Notre fichier 'InventoryServiceApplication' va nous permettre de créer quelques produits afin de tester notre partie backend et frontend:
![Capture d’écran (121)](https://user-images.githubusercontent.com/111126484/207469362-9f6e9b11-d6f4-4e4f-94d2-e5a991cb3203.png)
- Le fichier application.propreties va nous permettre d'allouer un port à notre web service (dans ce cas 8082),le nom du service,préciser la base de données et préciser si le web service doit s'authentifier ou non avec l'attribut 'spring.cloud.discovery.enabled'
![Capture d’écran (120)](https://user-images.githubusercontent.com/111126484/207469722-082f0635-5382-499c-942b-4ccc378fbe77.png)

  #Web service Billing:
- Création de la classe 'Bill' qui sera la classe dédiée à la facture et représenté par son id,sa date de création,la liste des produits commandés,l'id du client ainsi que le client:
![Capture d’écran (124)](https://user-images.githubusercontent.com/111126484/207471330-5bfff71c-fca6-4d1a-b53f-a6447e0b7d89.png)
- Création de la classe 'ProduitItem' qui sera la classe dédiée au produit et représenté par son id,sa quantité,son prix,l'id du produit ainsi que la facture du produit:
![Capture d’écran (125)](https://user-images.githubusercontent.com/111126484/207471524-528df6e8-47f2-448b-9852-c534158bac24.png)
- Création de Bill Repository:
![Capture d’écran (131)](https://user-images.githubusercontent.com/111126484/207472097-384362f8-9253-4e49-bac8-e2233236d180.png)
- Création de ProductItem Repository:
![Capture d’écran (132)](https://user-images.githubusercontent.com/111126484/207472204-32dd4c98-0e0b-4ef7-9d71-b8f704c28e15.png)
- Création de 'CustomerRESTClient' et 'ProductItemRESTClient' avec OpenFeign qui va nous permettre de communiquer avec les micro services via REST:
![Capture d’écran (127)](https://user-images.githubusercontent.com/111126484/207472514-f66d0b3c-e7bc-4ce1-918a-88993fbb446d.png)
![Capture d’écran (128)](https://user-images.githubusercontent.com/111126484/207472624-2cd8dbf1-c911-40bb-9354-340d58f0b8a4.png)
- Création du Rest Controller : 
![Capture d’écran (134)](https://user-images.githubusercontent.com/111126484/207472711-c126c338-4a84-46d6-b0c0-c0f4f1cad0d8.png)
- Notre fichier 'BillingServiceApplication' va nous permettre de créer quelques factures afin de tester notre partie backend et frontend:
![Capture d’écran (135)](https://user-images.githubusercontent.com/111126484/207472828-0218700a-aa77-436b-b51c-218ffdcf5616.png)
- Le fichier application.propreties va nous permettre d'allouer un port à notre web service (dans ce cas 8083),le nom du service,préciser la base de données et préciser si le web service doit s'authentifier ou non avec l'attribut 'spring.cloud.discovery.enabled'
![Capture d’écran (136)](https://user-images.githubusercontent.com/111126484/207472896-b6a08eca-402f-4f3b-945c-ad58fff0132f.png)

  #Création de la gateway et du service d'authentification Eureka
 - Gateway : Configuration des micro services,des ports ainsi que résolution du problème CORS:
   - Notre fichier 'GatewayServiceApplication' va nous permettre de configurer dynamiquement les routes:
    ![Capture d’écran (137)](https://user-images.githubusercontent.com/111126484/207473792-66db6032-9377-40ca-a196-748cde8d94a6.png)
   - Notre fichier de configuration 'app.yml' va servir à définir pour chaque route son id,son uri ainsi que son path:
   ![Capture d’écran (138)](https://user-images.githubusercontent.com/111126484/207473995-3ffca7d4-2f97-4525-a74a-8e03074f497c.png)
   - Le fichier application.propreties va nous permettre d'allouer un port à notre web service (dans ce cas 8085),le nom du service et préciser si le web service doit s'authentifier ou non avec l'attribut 'spring.cloud.discovery.enabled'
   ![Capture d’écran (139)](https://user-images.githubusercontent.com/111126484/207474141-28fdeeed-8863-4c3b-a66c-9f44aa10b417.png)
   - Notre fichier de configuration 'application.yml' va servir pour résoudre le problème de CORS et ainsi accepter les requetes venant de la partie front end à la partie backend afin qu'elle soient autorisées:
   ![Capture d’écran (140)](https://user-images.githubusercontent.com/111126484/207474219-654e7fc2-660c-4d9f-a4cc-29b18432c237.png)
  -Eureka : Service de registre et d'authentification des services:
  - Le fichier application.propreties va nous permettre d'allouer un port à notre web service (dans ce cas 8761) et de lui indiquer que ce n'est pas la peine de s'auto authentifier:
  ![Capture d’écran (141)](https://user-images.githubusercontent.com/111126484/207474671-484f6813-6a69-4236-be83-52181b0863ad.png)
  
#Partie 2 : Partie Front end avec Angular:
  -Partie produits:
  ![Capture d’écran (142)](https://user-images.githubusercontent.com/111126484/207475873-1e5cb35d-e302-4d39-b854-d56773794c0f.png)
  -Partie client:
  ![Capture d’écran (143)](https://user-images.githubusercontent.com/111126484/207475927-571232b2-80aa-4613-a592-3f0ce67c0aec.png)
  -Partie facture:
  ![Capture d’écran (144)](https://user-images.githubusercontent.com/111126484/207475970-23327cb4-2234-4d24-8081-bd6131523cdd.png)
  -Partie informations facture:
  ![Capture d’écran (145)](https://user-images.githubusercontent.com/111126484/207476031-4860c4dd-ac60-483c-bc03-b87eeae49af9.png)
