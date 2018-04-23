# Thor-Ragnarok-Query

This is a documentation of my approach on the exercises .
It documents the approach for the Practical and the Theory exercise.

### [This is the link](https://www.getpostman.com/collections/b2ec0f61d5622bb00d65)  to the POSTMAN script

## 1. Practical Exercise

# Q1 & Q2
### Admin

* ```First Generate an API KEY from http://www.omdbapi.com/apikey.aspx```
*  ```Upon receiving the API KEY via e-mail, Activate the API KEY by clicking the link provided in the e-mail```
* ```I have decided to use the "By Search" Parameter('s') and the "by ID or Title" Parameter('i') so as not to exhaust testing```
##### And you are all set
----------------------------------------------------------------------------------------------------------------
### Scripting Using POSTMAN
* Positive Queries and possible Negative Queries were written with different test cases corresponding to each query.
* A collection(Thor:Ragnarok Collection Query) with two folders of Positive and Negative Queries was created with a global variable of http://www.omdbapi.com

# Q3

### Positive Query
1. A **_prerequisite_** to use the 'i'(ie id key) is to do the following:
* Make a GET request with the 's' (ie Search key) with its value(ie "Thor: Ragnarok") and the API KEY with it's value
* A JSON response should have the "imdbID", which is the 'i' or id value.
* Write a test case to check the status code of 200
	```JS
	pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);});
	```
* Write a Test Case to see if the JSON body contains the string "Thor Ragnarok".
	```JS
	pm.test("GET Thor: Ragnarok", function () {
    pm.expect(pm.response.text()).to.include("Thor: Ragnarok");});	
	```
	
2. Now from the JSON response in Query #1, the "imdbID" should be used as a parameter for querying "Thor: Ragnarok"
* Make a GET request with the 'i' (ie ID key) using the "imdbID" value and the API KEY with it's value
* Write 4 test cases to validate responses that: 
	* Return a Status code of 200
	```js
	pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
	```
	* Return the Title "Thor Ragnarok"
	```js
	pm.test("Title is Thor: Ragnarok", function () {
    pm.expect(pm.response.text()).to.include("Thor: Ragnarok");
	```
	* Return a "imdbID" of tt3501632
	```js
	pm.test("Response imdbID is tt3501632", function () {
    pm.expect(pm.response.text()).to.include("tt3501632");});
	```
	* Do not return a "imdbID" of "tt6611130"
	```js
	pm.test("Response imdbID is not tt6611130", function () {
    pm.expect(pm.response.text()).to.not.include("tt6611130");});
	```

# Q4
### Negative Query

1. Make a query with empty parameters
 * The test written is expecting a 200 status code and a response body with the html format
 ```js
 pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);});

pm.test("Expecting a Html resonse", function () {
    pm.expect(pm.response.text()).to.include("</html>");});
 ```
2. Query with only the API parameter and without the ID parameter
* This Test case expects a 200 status response and an error message since there is only an API KEY and value an no ID parameter
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);});

pm.test("Error message", function () {
    pm.expect(pm.response.text()).to.include("Error");});
```
3. Query with only ID parameter and without API KEY value
* The expected result is a 401 response and an appropriate error message
```js
pm.test("Status code is 401", function () {
    pm.response.to.have.status(401);});

pm.test("Error message", function () {
    pm.expect(pm.response.text()).to.include("Error");});
```
4. Query with an Incorrect/Invalid API KEY
* The expected result is a 401 response and an appropriate error message
```js
pm.test("Status code is 401", function () {
    pm.response.to.have.status(401);});

pm.test("Error message", function () {
    pm.expect(pm.response.text()).to.include("Error");});
```
# Q5

The below Automated test Scrips are the same as that in Q3.2 and they can be found [here](https://www.getpostman.com/collections/b2ec0f61d5622bb00d65)

* Write 4 test cases to validate responses that: 
	* Return a Status code of 200
	```js
	pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
	```
	* Return the Title "Thor Ragnarok"
	```js
	pm.test("Title is Thor: Ragnarok", function () {
    pm.expect(pm.response.text()).to.include("Thor: Ragnarok");
	```
	* Return a "imdbID" of tt3501632
	```js
	pm.test("Response imdbID is tt3501632", function () {
    pm.expect(pm.response.text()).to.include("tt3501632");});
	```
	* Do not return a "imdbID" of "tt6611130"
	```js
	pm.test("Response imdbID is not tt6611130", function () {
    pm.expect(pm.response.text()).to.not.include("tt6611130");});
	```

## 2. Theoretical Exercise

## Q1

 -|A Test Case        |A Use Case
--|-------------------|-----------------
Definition |A step taken to validate the functionality of a system based on expected results from a specific requirements|A series of steps taken to achieve an interactive task between a user/system and another user/system
Example |Filling an online form to validate the appearance of an error message/welcome message upon inputing incorrect or correct credentials respectively.| Filling an online form with credentials and receiving an appropriate page/message upon clicking submiting button.

## Q2
* In CI, execution fo Automatesd Tests would happen after a Build of the code base from developers. Automated Regression Tests are supposed to be executed after every code patch/commit on to the code base.

## Q3
* Testing in the API level is mainly integration testing since the function of an API is establishing a bridge between systems/services/applications etc, to see if they speak to each other. Security and Functional testing are as important for API testing.

## Q4
* This depends on the scale/size and structure of the company.
	* In a small sized company: a QE will be involved from the Planning stage up until the deployment.
	* In a large company, there could be a discrete structure such as domains only for developers, testers etc: In this case, the QE might only be involved after a build for the testing phase to begin and, during and after the deployment for maintenance purposes.
	
## Q5
* The expectation is a successful call: I would attribute 10% to Manual Testing since test cases had to be designed around changing parameter inputs; as a result Automation testing had to be 90%.
