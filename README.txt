Create a workspace for "Trello". Create a new collection with any name. 
Try this first request, https://api.trello.com/1/members/me.
The response will be an "invalid token" which means you don't have the authority to access this API.
So now you realize that you need to get your account credentials which will be sent with every request so the server will
detect who you are and execute your request if you have permission to make this request.
To get your account credentials, go to this website https://developer.atlassian.com/cloud/trello/,
and log in with the same account you're using to log in to Trello. 
After login, open the same URL, https://developer.atlassian.com/cloud/trello/, 
and make sure you're selecting "Guides" at the top of the page.
On the left side click on the option

"TRELLO'S REST API" and click on "Authorization" under it, if you get lost, navigate directly to this URL, https://developer.atlassian.com/cloud/trello/guides/rest-api/authorization/,
but make sure first you're already logged in. Remember we need to get account credentials and know how to use them inside the request
(for e.x should we send it with query parameters or headers, etc),
in this page, you will realize that those credentials consist of two things
key=value token=value You will also realize that those two should be used as query parameters (you will find this info under this section
"Authorization via Query Parameters" on this page at the end). 
So now we already know how Authorization works but we need to know how to get those key, token values for your account,
click on this link shown on the page, https://trello.com/app-key/, you will find it at the beginning of the page under the section "Authorizing A Client". 
It should direct you to another page that contains your credentials, key, and token. Let's try this request again on postman after adding credentials in query parameters like this,
https://api.trello.com/1/members/me?boards=open&key= &token= Note: this request returns all opened boards, that's why we are using boards=open in the query parameters. Go to this link, 
https://developer.atlassian.com/cloud/trello/rest/api-group-actions/, where you could find all Trello's APIs. On the left side under "Boards", select this API "Create a Board". 
Notes: There are a lot of query parameters but you only need to add the REQUIRED ones. You will find an Example on the URL that will be used at the end of each request. 
Example: curl --request POST--url 'https://api.trello.com/1/boards/?name={name}' Don't forget to add key & token in your query parameters as well. 
Write test cases on Postman to verify the most important parameters and confirm its default values like closed is false. 
permissionLevel = private canBePublic is true canInvite is true Make the following request is number 2 in the collection after "Create a Board" curl --request GET--url 'https://api.trello.com/1/members/me?boards=open' 
Write a test case to verify that number of boards in the response is above 
1. Create Variables (as you wish Global or Environment) to get the following values. FirstBoardID LastBoardID 
Note: To get the LastBoardID you need to write a code to count the number of boards and get the last board ID in the array. 
So don't depend on that the number of boards is always 2 Boards. Run the whole collection from this option "Run Collection" to make sure that the 2 requests are running fine together. 
Notes: It's better to increase the Delay time to around 1000 ms and no need to change any other options. Before running collection, you should make sure all your requests tabs are saved (no orange dot on any request). 
Go to this link again https://developer.atlassian.com/cloud/trello/rest/api-group-actions/, on the left side under "Boards", select this API "Delete a Board". Please make this request number 3 in the collection.
Write test cases to verify: The status code is 200.
Response Body should contain a meaningful message like "board is removed successfully". 
Run the whole collection again to check, don't forget the notes mentioned before. Under "Lists", select this API "Create a List", this should be request number 4 in the collection. 
Write test cases on Postman to: Verify the following keys exist in the response regardless of what the value is (just confirm the key, not the value) id name idBoard Verify the most important parameters and confirm their default values 
like: closed is false. limits are empty object {}. 
Run the whole collection again to check, don't forget the notes mentioned before. Under "Boards", select this API "Get Lists on a Board", this should be request number 5 in the collection. 
Write a test case to verify that the number of lists in the response is 3 [default lists are To Do, Doing, Done]. Create Variables (as you wish Global or Environment) to get the following values. 
FirstListID LastListID Note: To get the LastListID you need to write a code to count the number of lists as we mentioned before with Boards. 
Run the whole collection again to check, don't forget the notes mentioned before. 
Under "Lists", select this API "Archive or un-archive a list", this should be request number 6 in the collection. 
Note: There's a query parameter called "value" that should be mandatory even if it's not mentioned. value=true means Archive value=false means un-archive. 
Write test cases to verify: Status code is 200. In Response Body, "closed" is true if the value=true (in the query parameter) and vice versa. Response Headers include a key called "Set-Cookie" and its value contains the text "isEnterpriseAdmin%3Dfalse". 
Run the whole collection again to check, don't forget the notes mentioned before. After running you will find the "Export Results" button on the top right, 
use it to export your test results in JSON format. Also export your collection, your environment variables, and global variables if found   
