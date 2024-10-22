# PostmanForMe
# NewMan
https://github.com/postmanlabs/newman
    It’s a CLI for running postman collections in a terminal which helps further for CICD.
    Dependencis : Node.js and NPM
# Intall NewMan
	1. Npm install -g newman
# Run a collection using newman CLI
	1. Newman run <<link to the collection>> // we can get the link by right clicking on collections in postman -->share collection -->collection link-->collection link 
 
	Ex: newman run https://www.getpostman.com/collections/f81a23f887c2e42e610e
	
	Note: If any changes are done to the collection in postman, the link should be updated in order for us to see the appropriate results in Newman as per the changes. 

	2. The above process of getting updated link is not suggested when you are working in a team. Best way is to export the collection and run it with collection name.
		a. Right click on collection and export the collection as <<test.json>>
		b. Go to cmd and go to folder where collection is present and run the below command
		c. Newman run test.json
	3. Generate API Key
		a. Click on user -->Acccount Settings -->Postman API Keys-->Generate API key or directly access using below.
		b. https://web.postman.co/settings/me/api-keys\
	4. Get the List of collections
		a. Run the below command.Follow this link to create below link -
		Generate an API key
		From <https://github.com/postmanlabs/newman#using-newman-with-the-postman-api> 
		
	newman run https://api.getpostman.com/collections/6503bbaf-0bf2-ecd4-9a26-02e95f4ab915?apikey=<replace>
	Note: This process is auto synced to postman profile hence no need of exporting after any changes etc 
# 5. Using Newman with postman
	1 Generate an API key
	2 Fetch a list of your collections from: https://api.getpostman.com/collections?apikey=$apiKey
	3 Get the collection link via it's uid: https://api.getpostman.com/collections/$uid?apikey=$apiKey
	4 Obtain the environment URI from: https://api.getpostman.com/environments?apikey=$apiKey
	5 Using the collection and environment URIs acquired in steps 3 and 4, run the collection as follows:
	$ newman run "https://api.getpostman.com/collections/$uid?apikey=$apiKey" \
	    --environment "https://api.getpostman.com/environments/$uid?apikey=$apiKey"
	
	Note: It is uid that is to be replace in above command and not id
	
	newman run  "https://api.getpostman.com/collections/15403473-296ab3b8-9d13-407b-a3b4-9c10815e4c79?apikey=<replace>" \
	    --environment "https://api.getpostman.com/environments/15403473-d65a1a64-3fbc-4be6-bfb5-b9db561596ec?apikey=<replace>"
# 6. Run the report to generate HTML Extra Report
	newman run  "https://api.getpostman.com/collections/15403473-6503bbaf-0bf2-ecd4-9a26-02e95f4ab915?apikey=<replace>" \
	    --environment "https://api.getpostman.com/environments/15403473-d65a1a64-3fbc-4be6-bfb5-b9db561596ec?apikey=<replace>"  -r htmlextra

	newman run  "https://api.getpostman.com/collections/15403473-6503bbaf-0bf2-ecd4-9a26-02e95f4ab915?apikey=<replace>" \
	    --environment "https://api.getpostman.com/environments/15403473-d65a1a64-3fbc-4be6-bfb5-b9db561596ec?apikey=<replace>"  --reporters cli, htmlextra
# 7. Setting runtime environment variables
	var jsonData = pm.response.json();
	postman.setEnvironmentVariable("authtoken","Token "+jsonData.user.token)

 ## Newman to run collection locally and generate htmlextra report

1. Install Node.js:
   - Download and install Node.js from https://nodejs.org/
   - Verify installation by running `node --version` in your command prompt

2. Install Newman globally:
   ```
   npm install -g newman
   ```

3. Install newman-reporter-htmlextra globally:
   ```
   npm install -g newman-reporter-htmlextra
   ```

4. Export your Postman collection:
   - Open Postman
   - Select your collection
   - Click "..." next to the collection name
   - Choose "Export"
   - Save the JSON file to your desired location

5. (Optional) Export your environment file if you're using one:
   - Go to your environments in Postman
   - Click the download icon next to the environment name
   - Save the JSON file

6. Run Newman with htmlextra reporter:
   ```
   newman run path/to/your/collection.json -e path/to/your/environment.json -r htmlextra,cli --reporter-htmlextra-export path/to/output/report.html
   ```
   Replace the paths with your actual file locations.

7. View the report:
   - Navigate to the output location you specified
   - Open the HTML file in a web browser

Additional tips:
- Use `--reporter-htmlextra-darkTheme` for a dark-themed report
- Use `--reporter-htmlextra-title "Your Report Title"` to set a custom report title
- Use `--reporter-htmlextra-logs` to include console logs in the report

Remember to run these commands from the directory where your collection and environment files are located, or provide the full path to these files in the command.


# 8. Scope of variables 
	

# 9. Pm.variables.get("key") // This is a scoped getter.This will get the value from the narrowed scope that postman determines as good as {{accessToken}}.
# 10. Pm.globals.get("Key") //This will fetch the value from global scope
# 11. Pm.environments.get("key") //This will fetch the value from environment scope.
# 12. To send a request from pre-request step generate the required code by clicking code beside cookies under send button in postman and select node.js-Request
# 13. Import a request from a curl command.
		a. Go to angular.realworld.io
		b. Create an article
		c. Check the network tab of developer tool and see XHR call
		d. Right click on the command and copy as curl(bash)
		e. Import as raw text in postman
# 14. Generate a java script equivalent code in pre-request script
		a.  Beside save button click on the code </> icon and select node-js request from drop down and the code is avaialble to copy paste and use.
		b. Generate a send request code from snippet and it will work
		
# 15. General Troubleshooting
		a. Check if the service is up and running in browser
		b. Check if right protocol is used (http/https)
		c. Check that the url is correctly spelled
		d. Disable SSL certificates as applicable
# 16. Path Params are defined like http://example.com/:id
		a. Here :id is path param. Multiple path params are separated  by "/" :id makes its editable in postman params
		b. Any thing following "?" is a query param. Multiple query params are separated by "&"
# 17. Basic Work Flow in postman
		a. Postman.setNextRequest("Request 3") //this will ensure the next request3 is executed after the current request.
		b. Postman.setNextRequest(null) //this will stop the execution further after current request.
		c. If postman.setNextRequest(null) is not present in the redirected requests, it will continue its natural flow and might endup in endless loop
		d. To overcome the above loop we can use if condition with a global variable to track howmany times it ran.
# 18. Request Name as String
```bash
Pm.info.requestName //this will return the request name as String
```
# 19. Id of Request as string
```bash
Pm.info.requestid //this will return the id of the request as a string.
```
# 20. External Data Retrieval
```bash
Pm.iterationData.get("<<name of the variable>>") // this can be used for assertions in tests with external data
 ```
# 21. Parsing Response
		a. pm.respone.json()  //get the json response body
		b. xml2Json(responseBody) // get xml response body as json
		c. cheerio(pm.response.text()) // get html response body
		d. pm.response.text() //get plain-text response body
		e. csv-parse/lib/sync //get csv response body
# 22. Chai Assertion Library
		a. https://www.chaijs.com/api/bdd/
			i. Ex: expect({a: 1, b: 2}).to.not.have.any.keys('c', 'd');
		b. Pm.expect(a).to.eql(b) //this will check if the object values are equal
		c. Pm.expect(a).to.equal(b) //this will check if both objects (references) are same
		d. Pm.expect(a).to.not.eql(b) //this will check if the object values are equal
		e. Pm.expect(true).to.be.true
# 23. Papa Parse for CSV parsing
	24. For Loop
	For(let filter of jsondata.filters){
	Console.log(filter)
	}
# 25. If the json property itself is some random value like 5sdferwer34sdfe then use the below syntax to retrieve its vlaue
		a.  json['5sdferwer34sdfe '] //this will work
		b. Json.5sdferwer34sdfe  //this will fail
# 26. Fetching a dynamic propery
		a. Use .hasOwnProperty with a conditional statement to identify 
# 27. Alternate way to find an item instead of looping
		a. Const person = response.find(item=>item.name==="jane")
# 28. Headers
	This is how you retrieve a header from the response:
	pm.response.headers.get('X-Cache') 
	and in a test:
	Header exists: pm.response.to.have.header(X-Cache'); 
	Header has value: pm.expect(pm.response.headers.get('X-Cache')).to.eql('HIT'); 
# 29. Cookies
	In a similar fashion you can test cookies as well.
	Cookie exists:
	pm.expect(pm.cookies.has('sessionId')).to.be.true; 
	Cookie has value:
	pm.expect(pm.cookies.get('sessionId')).to.eql(’ad3se3ss8sg7sg3'); 
# 30. Authentication Types
		a. Basic Auth
			i. In Authorization tab select Type as Basic auth and enter username and password
			ii. In headers automatically Authorization : <base64 encoded string equivalent of Basic  username:password is generated>
				Ex: Basic postman:password get converted to Basic cG9zdG1hbjpwYXNzd29yZA== 
	Note: Encoding/Decoding can be checked at https://codebeautify.org/base64-decode
## Random Variables in postman
In the request body type {{$ you will see a list of pre-defined random variables that can be used.
## PUT Vs PATCH
PUT will replace the entire item, Patch will update certain properties of an item.
## HEAD
The HEAD method in HTTP is similar to the GET method, but it only requests the headers of the response, not the actual resource representation. When you make a HEAD request to a server, it will respond with the headers that would be returned if you made a GET request to the same resource. However, it won't include the body of the resource itself.


## Generate Timestamp
```javascript
// Function to generate a timestamp in the format: YYYY-MM-DDTHH:mm:ss-05:00
function generateTimestamp() {
    const date = new Date();
    const offset = -5 * 60; // Offset in minutes for -05:00 timezone
    const localISOTime = new Date(date.getTime() - (offset * 60000)).toISOString().slice(0, -1);
    const timezoneOffset = '-05:00';
    return `${localISOTime}${timezoneOffset}`;
}

// Generate the timestamp
const timestamp = generateTimestamp();

// Set the timestamp as an environment variable
pm.environment.set('generatedTimestamp', timestamp);

console.log('Generated Timestamp:', timestamp);
```
Or use this for the correct timezone

```javascript
function generateTimestamp() {
    const date = new Date();
    const year = date.getFullYear();
    const month = String(date.getMonth() + 1).padStart(2, '0');
    const day = String(date.getDate()).padStart(2, '0');
    const hours = String(date.getHours()).padStart(2, '0');
    const minutes = String(date.getMinutes()).padStart(2, '0');
    const seconds = String(date.getSeconds()).padStart(2, '0');
    const timezoneOffset = '-05:00';

    return `${year}-${month}-${day}T${hours}:${minutes}:${seconds}${timezoneOffset}`;
}

// Generate the timestamp
const timestamp = generateTimestamp();

// Set the timestamp as an environment variable
pm.environment.set('generatedTimestamp', timestamp);

console.log('Generated Timestamp:', timestamp);
```
##  Postman script to check if a resonse body contains a specific key value
```javascript
pm.test("Check if decline reasons contains reasonCode = 6005", function () {
    // Parse the response body as JSON
    var jsonData = pm.response.json();

    // Assume the array is in a property called 'data'
    var array = jsonData.somekey.otherkey;

    // Check if any object in the array has reasonCode = 6005
    var containsReasonCode = array.some(function (item) {
        return item.keytobechecked === "value";
    });

    // Assert that the array contains the reasonCode
    pm.expect(containsReasonCode).to.be.true;
});
```
# Gradle
    compile "com.smartcar.sdk:java-sdk:2.1.5" Maven: <dependency> <groupId>com.smartcar.sdk</groupId> <artifactId>java-sdk</artifactId> <version>2.1.5</version> </dependency>
# Important Resources
https://postman-quick-reference-guide.readthedocs.io/en/latest/cheatsheet.html
https://designer.mocky.io/design
https://www.chaijs.com/api/bdd/
https://requestbin.com/
https://learning.postman.com/docs/running-collections/using-newman-cli/command-line-integration-with-newman/#:~:text=The%20easiest%20way%20to%20run,to%20share%20as%20a%20file.&text=You%20can%20also%20pass%20a%20collection%20as%20a%20URL%20by%20sharing%20it.
https://github.com/postmanlabs/newman
https://swapi.dev/
https://learning.postman.com/docs/developer/echo-api/
https://codebeautify.org/base64-decode
https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.1
https://github.com/public-apis/public-apis

Newman connect ETIMEDOUT 198.105.244.23:80
Content-Type : aplication/xml; charset=utf-8
Postman sends 'Content-Length' and Newman sends 'content-length'. 
 Thanks for your reply. I have resolved it with "-k" in the command.(
1. Set the 'Connection' header for the (GET) request that is failing in Newman to the value 'keep-alive' in the Postman collection.
2. Re-export your collection for running in Newman
Working! The header is 'Connection', not 'Connect'.

From <https://github.com/postmanlabs/newman/issues/249> 

Citations:  
[1] https://learning.postman.com/docs/collections/using-newman-cli/installing-running-newman/  
[2] https://toolsqa.com/postman/install-newman-using-npm/  
[3] https://www.npmjs.com/package/newman  
[4] https://apidog.com/blog/how-to-install-newman-and-run-postman-collection/  
[5] https://www.youtube.com/watch?v=51PL_D6RINw  
[6] https://www.softwaretestinghelp.com/postman-newman/  
[7] https://www.youtube.com/watch?v=wyIC-FquhUk  
[8] https://www.npmjs.com/package/newman-reporter-htmlextra  
