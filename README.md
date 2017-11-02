# SCIM REST WEB SERVICE - Executing through Curl Command
Repository contains OIM related information

For executing the Rest Webservice through curl command follow below steps-
*********************************************************************************

1. Copy the file on any location on OIM server e.g. /app/oracle/SCIMWebservice/

2. Copy the text file for the required operation like below on location- /app/oracle/SCIMWebservice/
   a) Create User Operation - createuser.txt
   b) Modify User Operation - modifyuser.txt
   c) Enable User Operation - enableuser.txt
   d) Disable User Operation - disableuser.txt
   e) Lock User Operation - lockuser.txt
   f) Unlock User Operation - unlockuser.txt

3. Run the Curl command on same location- /app/oracle/SCIMWebservice/
  
Note: For Search User and Delete User Input file not required. For these operation directly run the curl command with user Key or User ID.

Search User Operation- 
--------------------------------------------------------------------------------------------------------------------------
Curl command for Search User Operation-

curl -i -X 'GET' -k -u adminuser:Admin@password -H "Content-Type:application/scim+json" "http://oimhost:oimport/idaas/im/scim/v1/Users?filter=userName eq Userlogin"

For Searching User Key only then run below command-

curl -i -X 'GET' -k -u adminuser:Admin@password -H "Content-Type:application/scim+json"  "http://oimhost:oimport/idaas/im/scim/v1/Users?attributes=id&filter=(userName co A0001999)"    --Here is id User Key

Delete User Operation-
--------------------------------------------------------------------------------------------------------------------------
Curl Command-

curl -i -X 'DELETE' -k -u adminuser:password -H "Content-Type:application/scim+json" http://oimhost:oimport/idaas/im/scim/v1/User/133777       --here 133777 is User Key

Create User Operation:
--------------------------------------------------------------------------------------------------------------------------
curl command-

curl -i -X 'POST' -d @createuser.txt -k -u adminuser:password -H "Content-Type:application/scim+json" http://oimhost:oimport/idaas/im/scim/v1/Users

Input File createuser.txt content-

{
  "schemas":
  [
    "urn:ietf:params:scim:schemas:core:2.0:User",
    "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User",
    "urn:ietf:params:scim:schemas:extension:oracle:2.0:OIG:User"
  ],
  "name": {
    "familyName": "user01",
    "givenName": "test01",
    "middleName": "tu01",
  },
  "displayName": "Babs Jensen",
  "emails":
  [
    {
      "value": "test01@test.com",
      "type": "work"
    }
  ],
  "addresses": [
    {
      "type": "work",
      "streetAddress": "100 Universal City Plaza",
      "locality": "Hollywood",
      "region": "CA",
      "postalCode": "91608",
      "country": "USA"
    },
    {
      "type": "home",
      "formatted": "456 Hollywood Blvd\nHollywood, CA 91608 USA"
    }
  ],
  "phoneNumbers": [
    {
      "value": "555-555-5555",
      "type": "work"
    },
    {
      "value": "555-555-4444",
      "type": "mobile"
    }
  ],
  "userType": "Contractor",
  "title": "Tour Guide",
  "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User":
  {
    "employeeNumber": "701984",
    "costCenter": "4130",
    "division": "Theme Park",
    "department": "Tour Operations",
    "manager":
    {
      "value": "1",
      "$ref": "http://HOST_NAME:PORT/idaas/im/scim/v1/Users/1"
    }
  },
  "urn:ietf:params:scim:schemas:extension:oracle:2.0:OIG:User":
  {
    "homeOrganization":
    {
      "value": "1",
      "$ref": "http://HOST_NAME:PORT/idaas/im/scim/v1/Organizations/1"
    }
  }
}

Modify User Operation-
--------------------------------------------------------------------------------------------------------------------------
Curl Command-
curl -i -X 'PATCH' -d @modifyuser.txt -k -u adminusername:password -H "Content-Type:application/scim+json" http://oimhost:oimport/idaas/im/scim/v1/Users/13497

Input File modifyuser.txt Content-

{"schemas":   
  [     
    "urn:ietf:params:scim:api:messages:2.0:PatchOp"   
  ],   
  "Operations":   
  [     
    { 
      "op":"replace",
      "path":"urn:ietf:params:scim:schemas:core:2.0:User:name.givenName",
      "value":"testwebnew01_Chnage01"
    },

 {
       "op":"replace",
       "value":
       {
         "emails":
         [
           {
             "value":"testwennew01@test.com",
             "type":"work",
             "primary": true
           }
         ]
      }
     },
  {
       "op": "replace",
    "path": "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager",
       "value":
       {
   "value": "13318",
         "$ref": "http://oimhost:oimport/idaas/im/scim/v1/Users/13318"
       } 
     },
 {         
      "op":"replace",
      "path":"urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber",
      "value":"5000003"
    },
 
 { 
      "op":"replace",      
      "path":"urn:ietf:params:scim:schemas:extension:oracle:2.0:OIG:User:Division",
      "value":"CORPORATE"
    },

  ]
}
