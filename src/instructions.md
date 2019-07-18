### Build & Style The UI

#### Step 1

*  Style the BODY element with a white background color

*  Create a DIV and give it a `data-cart-info` attribute. Inside the DIV, create a HEADING with `mdc-typography--headline4"` as its CSS class

*  The HEADING should have 2 SPAN elements. The First displays a shopping cart by setting its class to `material-icons` and setting its content to shopping_cart. The second SPAN has an attribute of `data-bill` and will be used to display the total figure the user is trying to pay on the app

*  After the `data-cart-info` DIV, create another DIV, give it an attribute of `data-credit-card` and set its class to  `mdc-card` and `mdc-card--outlined` Within the `data-credit-card` DIV, create a new DIV with a class of `mdc-card__primary-action` These elements will be styled with the look and feel of an actual credit card!

*  Within the `.mdc-card__primary-action` DIV, create an IMAGE with an attribute of `data-card-type` and set its SRC to http://placehold.it/120x60.png?text=Card. This IMAGE will be used to display the credit card type, based on the series of numbers entered by the user

*  Right after the IMAGE, create a DIV with an attribute of `data-cc-digits`. It should contain four INPUT text fields, each with a `size` of `4` and a placeholder of ---- (4 dashes). These fields will be used to collect the credit numbers

*  Create a DIV with an attribute of `data-cc-info` as a sibling to the `data-cc-digits` DIV. This new DIV should have two INPUT text fields, one for entering the card holder's name while the other will be for the card's expiry date. The first field should have a `size` of `20` and a `placeholder` of `Name Surname`. The expiry date field should have a `size` of `6` and a `placeholder` of `MM/YY` - indicating the expiry date format.

> We are now done with the structure of the credit card component. Let's make a button to allow the user make payment with the card details

*  Create a BUTTON as a sibling to the `data-credit-card` DIV. Set the BUTTON's class to `mdc-button` and give it a `data-pay-btn` attribute. It should have `Pay & Checkout Now` as its display text. After the user enters details of the card and clicks on this button, the app will strike-though the card numbers to indicate that they are in-valid.

#### Step 2

> While we might have the right structure in place, the app visually tells a different story. Time to make the app look good and usable. 

*  SPAN elements within the `data-cart-info` DIV should be displayed as inline block elements, and `vertical-align` set to `middle`. The `.material-icons` SPAN should have a `150` pixels size of font.

*  Give the `data-credit-card` DIV `435px` width, `240px` minimum height, `10px` rounded borders, and a `#5d6874` background colour.

*  Display the `data-card-type` IMAGE as a block element. Give it a `120px` width and a `60px` height.

*  The `data-cc-digits` DIV should have a `2em` top margin.

*  INPUT elements in the `data-cc-digits` DIV should have a white color, `2em` font size and line height, no border or background, and a right margin of `0.5em`;

*  The `data-cc-info` DIV should have a `1em` top margin.

*  INPUT elements in the `data-cc-info` DIV should have a white color, `1.2em` font size, no border and no background. The second input should also have a right padding of `10px` and be floated to the right of the viewport.

*  The `data-pay-btn` BUTTON should have a fixed position, `90%` width, solid border of `1px` and positioned `20px` from the `bottom` of the viewport.

> Your app should look functional at this point. 

### Get The Bill

> Write all Javascript strictly with ES6. This means use arrow functions instead of the function keyword. Declare variables and functions with `const` or `let`. Use `const` by default, and only use `let` if you are sure you need to re-assign values to the said variable. Use the Selector API instead of the *getElementBy...* or *getElementsBy...*  APIs. See https://developer.mozilla.org/en-US/docs/Web/API/Document_object_model/Locating_DOM_elements_using_selectors
---
> Install the JSON Viewer Chrome extension (https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc?hl=en), open a new tab and go to this URL (https://randomapi.com/api/006b08a801d82d0c9824dcfdfdfa3b3c). You will be making HTTP requests to that API endpoint, so spend some time looking at the structure of the response data.

#### Step 1
*  Create an `appState` variable and assign it an empty Object literal. This variable will hold data for the app.

* Create a `formatAsMoney` function. It should take in an `amount` and a `buyerCountry` parameter. It will use these parameters to format the user's bill as a proper currency.

* Create `detectCardType`, `validateCardExpiryDate`, and `validateCardHolderName` functions. Each should take in a parameter and use *object de-structuring* to obtain the `target` property of the parameter.

*  Create a `uiCanInteract` function. It will be called to setup the UI like adding event handlers to enable interactions with the app.

*  Create a `displayCartTotal` function. It should expect a parameter and should use *object de-structuring* to obtain `results` property of the parameter. This function will be called with the data from an API call and it will display the total payment bill.

#### Step 2

*  Create a `fetchBill` function. It should assign `https://randomapi.com/api/006b08a801d82d0c9824dcfdfdfa3b3c` to an `api` variable. It should then use the browser's `fetch` function to make a HTTP request to `api`. Using an arrow function in a `.then` call to the `fetch` function, return the response after converting it to JSON. Using an arrow function in another `.then` call to the first one,  take the converted JSON data in a `data` parameter and call `displayCartTotal`with it. Make sure to handle errors that may occur, e.g by showing a warning message in the console.

*  Call the `fetchBill` function from inside `startApp`.

#### Step 3

*  In `displayCartTotal`, de-structure the first item in the `results` array into a `data` variable. Next, use object de-structuring to obtain the `itemsInCart` and `buyerCountry` properties of `data`.

* Set `appState.items` to `itemsInCart` and set `appState.country` to buyerCountry

*  Use the Array `.reduce` function to calculate the total bill from `itemsInCart` Note that each item has a `qty` property indicating how many of that item the user bought. Assign the calculated bill to `appState.bill`

*  Go back to the `formatAsMoney` function. Use the `.toLocaleString` function on its `amount` and `buyerCountry` to format `amount` as a currency with the currency symbol of `buyerCountry`. The countries and their currency symbols are in the `countries` array you got in your starter code. If the `buyerCountry` is not in `countries`, then use `United States` and the country and format the currency accordingly.

*  back to where you left off in `displayCartTotal`, use the `formatAsMoney` function to set `appState.billFormatted` to the formatted total bill. The already assigned `appState.bill` and `appState.country` should come be handy now!

*  Set the text content of the `data-bill` SPAN to the formatted bill set in `appState.billFormatted`

*  Finally, call `uiCanInteract` to wrap up `displayCartTotal`

> Run the app (click the play button) and see if the correct formatted bill is displayed in the UI. Next, we will allow input and interaction so that users can provide payment information.

### Allow Payment

#### Step 0

* In your CSS, change the `.is-visa {...}` selector to `[data-credit-card].is-visa {...}` . Do same for `.is-mastercard {...}` change it to `[data-credit-card].is-mastercard {..}`

#### Step 1
*  Create a `flagIfInvalid` function just after `formatAsMoney` function. This function is used to mark an input entry as invalid (strike-though) nor not. It should take a `field` and `isValid` parameters. If `isValid` is *true*, it should remove the `is-invalid` class from `field`, otherwise it should add it to `field`. 

*  Just after `flagIfInvalid` function, create a `expiryDateFormatIsValid` function which takes a `target` parameter representing the card's expiry date field. It should return true if the field's value complies with the *MM/YY* format, otherwise it should return false.

*  With the above utility functions out of the way, go back to the `validateCardExpiryDate` function. It's de-structured `target` parameter will be the card's expiry date field. This function should return true if the value provided matches the `MM/YY` format (hint: delegate to *expiryDateFormatIsValid*) AND if the date is in the future. In either case, it should use the `flagIfInvalid` function to mark the field as valid or not. It then has to return true or false depending on if the validation requirements are met or not.

*  Now to the `validateCardHolderName` function. It's de-structured `target` parameter will be the card holder's name. Recall that its placeholder already suggests the required format, which is *Name Surname* (2 names separated by space). Each name should be at least 3 characters long. It should use the `flagIfInvalid` function to mark the field as valid or not and then return true or false depending on if the validation requirements are met or not.

#### Step 2

> The `uiCanInteract` function will wire up event handling for *PayCard*

In the `uiCanInteract` function

*  Set `detectCardType` as the `blur` event listener for the first INPUT element in the `data-cc-digits` DIV.

*  Set `validateCardHolderName` as the `blur` event listener for the first INPUT element (card holder's name) in the `data-cc-info` DIV. 

*  Set `validateCardExpiryDate` as the `blur` event listener for the second INPUT element (card expiry field) in the `data-cc-info` DIV. 

*	Set `validateCardNumber` as the click event listener for the `data-pay-btn` BUTTON

*  Give `focus` to the first INPUT element in the `data-cc-digits` DIV.

#### Step 3

> The `detectCardType` function displays a Visa or MasterCard logo depending on the card number entered by the user. For simplicity sake, our Visa card numbers begin with *4* and MasterCard numbers begin with *5*. These are the only supported credit cards in the *PayCard* app

``` 
Sample valid card numbers for your tests:
Visa:
4556372551434601
4916337563926287
4716361721613449
4539818898404311
4929416075118388

MasterCard:
5130752529459529
5250457226640843
5330664490375584
5241343263959571
5250445524664938
```

* Create a `validateCardNumber` function above the `uiCanInteract` function. 
	
* The `detectCardType` function has a de-structured `target` parameter which represents the first (of four) input field containing the first *4* digits of the card. If it detects a Visa card, it should add a `is-visa` CSS class to the `data-credit-card` DIV, else it should remove it to add a `is-mastercard` class instead, and vice versa. This gives the card a somewhat branded feel. To display the right card logo, `detectCardType` should set the `src` of the `data-card-type` IMAGE using the properties in the `supportedCards` object, which map to image data URLs for each type of card. Finally, `detectCardType` needs to return the `is-visa` or `is-mastercard` string value depending on the type of card detected

> Try filling in some details into the credit card UI and see if your validation code for the card holder's name and expiry date are working as stipulated. Does your `detectCardType` function also correctly set the right background color for the credit card component and display the right logo as well? 

### Validate Card Number

To have gotten this far, you are definitely a rockstar.  

![](https://media.giphy.com/media/xUA7bd4fc8NDP3Sh5C/giphy.gif)

> A number of changes and improvements were made to challenge specifications, and will require you to hard reload your browser to be on the latest build: *(a)* open Chrome developer tools *(b)* click and hold down the browser's refresh button to reveal a menu of 3 options *(c)* select the last menu option
---
> The progress indicator (numbered buttons on the left) might move you a previous step. Don't panic. We updated some aspects of the instructions and audits, so you'll have to modify your code a bit
---
> You will be implementing the *The Luhn Algorithm* to validate credit card numbers  (see https://en.wikipedia.org/wiki/Luhn_algorithm for more details), but follow the instructions below for simplicity.

1. Given a series of up to 16 digits, from the right to left, double every other digit starting with the second to last digit: 
```
1714
=> [1*, 7, 1*, 4]
=> [2, 7, 2, 4]
```

2. If a resulting doubled number is greater than 9, replace it with either the sum of its own digits, or 9 subtracted from it.
```
[8, 18*, 1] 
=> [8, (1+8), 1]
OR
=> [8, (18-9), 1]
Resulting in:
=> [8, 9, 1]
```

3. Sum all of the final digits: 
```
[8, 9, 1] 
=> 8+9+1 
=> 18
```

4. Finally, take that sum and divide it by *10*. If there is no remainder, the original credit card number is valid, else it is not valid.

> Time for you algorithm implementation. Recall that the `validateCardNumber` function is called when the user clicks on the *Pay & Checkout Now* button

#### Step 1

*  Create a `validateWithLuhn` function above the `validateCardNumber` function. It should take a `digits` parameter which will represent the credit card numbers as an array of *16 integers*. It should return true or false depending on if the *digits* are valid or not, including if it got more or less than 16 digits or a mixture of digits and invalid characters.

#### Step 2

* Implement  `validateCardNumber`  to validate the card numbers entered by the user. It delegates to the `validateWithLuhn` function for the actual validation and returns  the true or false value it gets from `validateWithLuhn`. Before returning the outcome of the validation, it should also indicate that the entries are invalid or valid by adding or removing the `is-invalid` class to the `data-cc-digits` DIV  respectively,  depending on the validity of the card number.  

#### Step 3

> You don't want the user paying the wrong bill because you've calculated it wrongly or presented it in the wrong currency

* Make sure what is set to `appState.bill` is correctly calculated by summing the prices of the items the user bought. Don't forget that each item has a quantity, which affects the price! 

* Make sure that  `appState.billFormatted`has the currency of the user's country and only uses the dollar currency if the user's country is not available within the provided list of countries.

> Try filling in some payment details into the PayCard app, then click the *Pay & Checkout Now* BUTTON to see if the entered card numbers are correctly marked as invalid or not.