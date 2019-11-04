
Welcome to the developer_starter_pack wiki!

Here's some things that you need to know to code, according to our previous discussion on having a qualified code. Please read carefully and implement it in your code as well. 
If you have something to add according writing a qualified code or other developer starter pack, please kindly raise a discussion and update the wiki! Or, if you have question, please kindly ask the team. Have a fun day coding!


***




## If, Else If, Else Conditions Rules

### If - Else Conditions 

* IF conditions do not always have to use ELSE conditions
* ELSE conditions is needed when IF conditions are absolutely required and values ​​in IF conditions have different values.
* ELSE conditions is not needed when IF conditions are not required and values in IF conditions have not different values.
* Avoid if - else condition Deep Nesting. Too many levels of nesting can make code harder to read and follow.

### If - Else If conditions

* If you want to check conditions with IF conditions, you can use ELSE IF conditions when you must check any condition in one condition.
* If you want to check conditions with IF conditions, you can use IF conditions when you must check any condition with one step.

## Switch-Case Condition Rules

Syntax example :

    switch(expression) {
      case x:
        // x condition
        break;
      case y:
       // y condition
       break;
    default:
       // default condition
    }

1. Expression in switch is to know  the possible value to be gained from the expression 
1. Case x and case y is the possible value from the expression. The case can be more 2 value, at least need one case for minimum requirement of switch.
1. The default condition is running when no one case has been fulfilled
1. The condition is the next step when the case or default is fulfilled
1. Break will stop the execution of inside the block. 


## Null-Aware 
(if your language code support null-aware operator)

* If you don’t initiate when declaring a variable, on construction function, or on init function of class, please aware with the null value that will happen. If your language code support null aware operator “?.”, please always use this. If not, please use if(variable != null) to avoid Null pointer exception / related error. 
* Better you use null-aware `??` or `?:` instead of using “if (variable != null) else”

  Example:

     `string pageTitle = suppliedTitle ?? "Default Title";`

If your language doesn’t support using null aware like `??` or `?:`, just use conditional operator, inline if (iif), or ternary if. 

Example:

`string pageTitle = suppliedTitle != null ? supplied : "Default Title";`

Instead of use:


    if (suppliedTitle != null) {
      string pageTitle = suppliedTitle;
    } else {
      string pageTitle = "Default Title";
    }

## Try-catch condition
1. You MUST use Try-Catch when you call a risky function such as parse variable data type, or other strange libraries.
1. If in your try have an action (ex: change state), don’t forget to add handler on Catch. If not, your code may be stuck in one state.

## Parameter

Parameter is something that you pass and you receive between function or class. In some languages, parameters in function can be required or optional. 

1. If you have 5 or more required parameters, maybe that time for you to use a new model class as a parameter instead of using so many parameters.

2. Don’t use the optional parameters as a required parameters. For example in dart:

	`functionName({@Required DataType variable}){}`

   That code will only give a warning to the developer, not an error. Do:

	`functionName(DataType variable){}`


3. Don’t pass a new class as parameter if you can create that class on targeted call function / class, to simplify your function / constructor class. So, you can easily call that function / constructor class everywhere.
   For example, **don’t do** this: 

	`functionName(new ClassName());`

   Move create `new ClassName` inside of `functionName`. So you will call that function easier like below: 

	`functionName();`

   Another example, if we have a code like this:

	`new ClassName(new HelperClass(), new UtilClass());`

   If you move `new HelperClass()` and `new UtilClass()` to the inside of `ClassName`, same as above, so you will create that ClassName easier like below:

	`new ClassName();`

   This way will decrease much redundant codes (boilerplates) and esier to call many times anywhere in our project.

##  Private & public Variable

1. Use private variable if it is only used locally in a particular class. 
Do the same for function or method, for example in Dart : 

    String _customerName   ---> variable
    String _getCustomerName(){  ---> function
      ...
    }

2. Use public variable if it could be accessed by another class, globally in the app.

    String customerName
    String _getCustomerName(){ 
      ...
    }

## Length
 please avoid a function more than 80 lines.

## The Use of Helper
Put all reusable functions or methods on a helper to avoid redundant functions in one app. For example, functions to handle String capitalization,  handle Date Formatting,  handle converting date from unix time epoch, and so on. We can implement a Helper Class by creating a class that have function which would do the job we want.
i.e. :

    class UtilityHelper {
	String capitalizeEachWord(String wordToCapitalized){
		…
		return capitalizedString;
      }
    }

In Dart, extends a model for Helper that depends  on a model. I.e:

    class Payment{
       @JsonKey(name: "payment_type")
       String paymentType;
    }

We want to create a helper which needs access to the model. Instead of creating a Payment object, it is better to extend the model from the Helper. So, it would be like this:

    class PaymentHelper extends Payment {
	bool get isDirectPayment {
		return paymentType.toLowerCase() == “direct”;
	}
    }

Instead of this.

    class PaymentHelper extends Payment {
       Payment paymentModel;
       Payment(this.payment);
       bool get isDirectPayment {
	      return paymentModel.paymentType.toLowerCase() == “direct”;
       }
    }

## Indentation
We must decide to have a consistent indentation style. How about to use this https://en.wikipedia.org/wiki/Indentation_style#Allman_style_ ?

## Comment and Documentation
Commenting is good, but please be aware to avoid redundant comment. Just simply it in one line for each function.

Do:

    // display state selection for US users
    $country_code = get_country_code($_SERVER['REMOTE_ADDR']);
    if ($country_code == 'US') {
        echo form_input_state();
    }

Don't:

    // get the country code
    $country_code = get_country_code($_SERVER['REMOTE_ADDR']);

    // if country code is US
    if ($country_code == 'US') {
        // display the form input for state
        echo form_input_state();
    }

## Naming Convention

|                                                                       |                                 Do                                |                            Don’t                            |
|-----------------------------------------------------------------------|:-----------------------------------------------------------------:|:-----------------------------------------------------------:|
| Boolean : must have prefix like “is, has, can”.                       |                  isOpen = true; hasValue = false;                 |                 open = true; value = false;                 |
| Number/Double : add words that describe number like “max, min, total” |                minExtent = 100; totalAmount = 200;                |                 extent = 100; amount = 200;                 |
| Function : is good to use “verb + noun” format.                       |                             getUser();                            |                         userData();                         |
| Iterating Items : use the singular version of the array name.         | const getUsers = users.map(user => {,return doSomething(user);}); | const getUsers = users.map(x => {,return doSomething(x);}); |

## Folder Structure
Every programming language has different style for structuring the folder, so at the moment, I just give a specific example in dart. https://pub.dev/packages/flutter_clean_architecture

## Deliver a Good Things for the Next Devs
Always code as if the person who ends up maintaining your code will not blame you :)



