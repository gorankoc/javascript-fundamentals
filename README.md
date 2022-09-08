# DEEP JS FOUNDATIONS

# Terminology


        - **Abstract Equality Comparison** = means just double equals **==**
        - **Strict Equality Comparison** - means triple equals **===** 
        - **null** - is the type value set to null is it just been defined without value
        - **undefined** - is the value empty is it ……
        - Literal
        - Variable declaration
        - Variable Declarator
        - Function Declaration
        - Function Expression
        - Anonymous Function Expression
        - Named Function Expression
        - Expression Statement
        - Identifier
        - Member Expression
        - red marble : in global enclosure scope
        - blue marble: own scope
        - L**exical scoping:** even though JavaScript looks like it should have block scope because it uses curly braces { }, a new scope is created only when you create a new function


    "use strict"; - expresssion statement just literal
    
    var teacher = "Kyle"; - variable declaration
    - identifier: teacher
    - VariableDeclarator: teacher = "Kyle";
    - Literal: "Kyle";


​    

    function otherClass(){ 
      var teacher = "Suzy"
      
      function ask(question){ - function declaration
        console.log(teacher, question) - ExpressionStatement
      - console.log: MemberExpression, console: Identifier, log: Idendtifier, arguments are also Identifiers
        
      }
      ask("why?") - ExpressionStatement
    }
    
    otherClass()  - ExpressionStatement
    ask("???")

# Introduction

Why do we learn JS … trend is in Typescript Closure Go, nobody ships their JS they wrote they ship they code that 14 layers of Babel transformations. 


## PLUS Operator ++

![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1648917160430_image.png)


****

If u have ++ in postfix position does that mean that the value returns untouched and made what ever increments it updated ?   




![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1648917763358_image.png)


Question becomes: What happens when with string representation and u do something fundamentally mathematic. Like incrementing it. 

Thinking **x++** as **x = x + 1** it will **return** the **string 5** and then it will coarse that string 5 it to number 5 and update it to 6.

Seems like it ***coarses it to number first y++ → 5   !***


12.4.4.1 Specification:


    Runtime Semantics:Evaluation
    
    UpdateExpression : LeftHandSideExpression ++
    
    1. lhs = result of eval LeftHandSideExpression
    2. Let oldValue be ? ToNumber (? GetValue(lhs))
    3. Letr newValue be the result of adding the value 1 to oldValue, using same rules as for the + operator
    4. Perform ? PutValue(lhs, newValue)
    5. Return oldValue


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1648918757164_image.png)

# Types


## Primitive Types

“In JavaScript everything is an object” that statement is false. Most of values in JS can act as object but here belongs **boxing, autoboxing, unboxing**. Spec says this is not a fact.

Boxing is wrapping a primitive value in an Object. When you treat a primitive type like if it were an object, e.g., calling to the toLowerCase function, JavaScript would wrap the primitive type into the corresponding object. This new object is then linked to the related built-in <.prototype>, so you can use prototype methods on primitive types. Methods like toLowerCase(), substring() … and concider better to let implicitly boxing because browsers are optimized.



- **undefined**
- **null**
- **boolean**
- **string**
- **symbol** (es6)
- **number**
- **object**


    **undeclared ?**  
    **null ?** **historical bug !**

******    **function ?**  ( sub type of object type )
    **array ?**  sub type of obj type, various methods, special type with indexing, length property.
    **bigint ?** 


    Unlike languages like C++ Java, JS variables don’t have types, values do.


## TypeOf Operator

**Returning string** - typeof always return a string. Saying here is some clue that u can expect to be able to do with values of this particular kind ( type ).

******

    var v; 
    typeof v; // "undefined"
    v = "1"   
    typeof v; // "string"
    v = 2;
    typeof v; // "number" 
    v = true;
    typeof v; // "boolean"
    v = {}; 
    typeof v; // "object"
    v = Symbol();
    typeof v; // "symbol"


## Undefined  

Many people think that it doesn’t not currently have a value, but it is that its value is not set, meaning that in past the value is set to undefined. Switching state.


    typeof doesntExist; // "undefined" 
    
    var v = null;
    typeof v;     // "object" OOPS!
    
    v = function(){}; 
    typeof v;     // "function" hmmm ?
    
    v = [1,2,3];
    typeof v;     // "object" hmmm ? utilities like Array.isArray

v = null, we get “object”, historical fact of JS, spec. is from es1, which essentially indicates to developers if u want to unset a regular value like a number u would use undefined, but if u want to unset object reference u would use null. That's why the typeof null returns object. But the truth is that its just a bug in JS.

*Unfortunately it returns “object” u have to make sure when u are doing a type check and it returns “object” make sure its not accidentally null! Because then u are not gonna get an object but a null value!* 

Undefined vs undeclared : these words are think of as synonyms they seem to make the same thing. And in English its probably true. 

I can get “undefined” for something that even does not exists, JS trys to pretend the absense of declaration is not that big of a problem that u can work around it. In retrospective they should have just made it to return “undeclared”. 

Typeof operator is the only operator in existence that is able to reference a thing that doesn’t exist  and not throw an error. 

Uninitiaized: variable that is never been initialized throws TDZ error.

Within Primitive Types there are Special Values:


## NaN 

( “~~not a number~~” ) … spec. special value that says sentinal value that indicates invalid number. How do we arrive to things that are NaN:


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1648927942794_image.png)


Number(“n/a”) “not applicable”, setting number to 0 is not absence of numeric value. Num 0 has substance in math. Its not a good placeholder! 


    myage - "my son's age" ... turns string into NaN so return is NaN

**NaN and triple operator** NaN is only value that does not have identity property meaning it is not equal to itself. Undefined is equal to itself. It doesn't do any coercion for us.
Typeof **NaN** is number its just invalid number, its better think of it as invalid number. Some people suggest they should never done NaN it should return something else, well what else should it return *undefined ( thats not numeric ), null, false, -1 ( terrible idea )* its historical **indexOf** returns because in old C days it returns only numbers. IndexOf should return NaN. Even worse suggest 0 ( wich is a number ).


## Negative Zero

In math it doesn’t exists. Utility **Object.is** is only option. Can check NaNs also.


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1648992985505_image.png)


Mathematically is commend to reffer to two separate entitities characteristics two seperate in same numeric value, the absolute value 0 represents how fast something is moveing and sign wich direction is it moveing. Car on a map.  


![Math.sign u cant use for -0! There is a fix sign custom method.](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1648993356995_image.png)

![This is more semantically readable u want one value to have the movement or direction.](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1648993478925_image.png)

![](/static/img/pixel.gif)


**Excersize: Object.is Polyfill** 

To have bettter understanding how primitive type values and some special value work. We are gonna make Polyfill for Object.is(…) 


    # Polyfill for 'Object.is(...)
    
    # In this excersize, you will define polyfill
    # Instructions
    # 1. 'Object.Is(..)' should take 2 param
    # 2. It should return true if the passed in parameters are exactly the same value      ( not just '===' -- see below! ) or false
    # 3. For 'NaN' testing, you can use 'Number.isNaN(..), but first see if you can 
    #    find a way to test without usage of any utility
    # 4. For '-0' testing, no built-in utility exists, but there is a hint:
    #    '-Infinity'
    # 5. If the params are any other values, just test them for strict equality
    # 6. You cannot use the built-in 'Object.is(..)' -- thats cheating
    
    ## Polyfill Patters
    
    #**NOTE** Since your JS Enviroment probably already has 'Object.is(..), to test yo#ur polyfill you'll have to first unconditionally define it ( no 'if' guard), and #then add the 'if' guard when you're done.
    
    # U are only defining something that is not defined 
    
    if(!Object.is){
      Object.is = function ObjectIs(..) { .. }
    }
    # working in JS Enviroment if u wrap in if statement u are just gonna test against built in object. So the hack is disabeling that statement so that u are always defining one. U woudnt do that in your normal polyfill so just for the purpose of the excersize.
    
    if(!Object.is || true  )
    
    #TESTing
    (Object.is(42,42) === true);
    (Object.is("foo","bar") === true);
    (Object.is(false,false) === true);
    (Object.is(null,null) === true);
    (Object.is(undefined,undefined) === true);
    (Object.is(NaN,NaN) === true);
    (Object.is(-0,-0) === true);
    (Object.is(0,0) === true);
    
    (Object.is(-0,0) === false);
    (Object.is(0,-0) === false);
    (Object.is(0,NaN) === false);
    (Object.is(42,"42") === false);
    (Object.is("42",42) === false);
    (Object.is("foo","bar") === false);
    (Object.is(false,true) === false);
    (Object.is(null,undefined) === false);
    (Object.is(undefined,null) === false);
    
    # they all have to return 'true'


    #Solution
    
    # boolean coersion so the only way it gets defined is by funcion
    # || true makes the function run
    if(!Object.is || true){ 
        Object.is = function ObjectIs(x,y){
            # negative zero and NaN
            var xNegZero = isItNegZero(x);
            var yNegZero = isItNegZero(x);
    
            if(xNegZero || yNegZero){
                // .. if both are NaN
                // if one or both of them or one of them is -0 how
                // we know we should ret true or not
                return xNegZero && yNegZero;
            }
            else if (isItNaN(x) && isItNaN(y)){
                return true;
            }
            else{
                return x === y;
            }
    
            // helper f, what do we know about operations about 0
            // adding subtracting, division 1/0 -> Infinity 
            // 1/-0 -> -Infinity
            function isItNegZero(v){
                return x == 0 && (1/v) == -Infinity;
            }
    
            // NaN is only value in existance in JS thats not equal to itself
            function isItNaN(v){
                return v !== v;
            }
        };
    }


## Fundamental Objects

New terminology recently intruduced to the spec so they are so called:


- aka: *Build-In Objects*
- aka: *Native Functions* ( historically )

Whatever terminology is ok. 
**Are they types, sort of ?** 

Java like mutation of JavaScript, Object representations with similar behavior. In Java when u wanna make a streing u call **new String …** we have this in JS, maybe its not good idea to use them, but it needs to be understood.


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649023018505_image.png)


String etc. coarse any value to that respective type:


    var x = 10; 
    String(x)     '10'
    Number(x)      10
    Boolean(x)     true

 *NOTE:* *JavaScript literals:*

**

- *Numeric Literal*
- *Floating-Point Literal*
- *Boolean Literal*
- *String Literal*
- *Array Literal*
- *Regular Expression Literal*
- *Object Literal*


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649023756822_image.png)


Ex. Date … new Date to construct Date object, because there is no Date literal. String for example JSON can be just called with String function converts.


# Abstract Operation 

Mentioned known **ToNumber( ) abstract operation.** … abstract operation is  fundamental building block how we deal with type conversion. 

- In JavaScript we refer to Type Conversion as coercion.
- So when u think of conversion and coercion u should think of it as interchangeable ( apparently identical; very similar alike ) as what JS is concern.


![Spec](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649024446086_image.png)


**ToPrimitive(hint)** *(7.1.1.)*


- abstract operation, if we have something  non primitive like object type  array function and we need to make it into primitive this is the abstract operation that will do the job. 
- abstract operation is not like a function that can be called they are actual method in Js engine, so when we call it abstract they are conceptual operation. 
- if we need to make something a primitive, conceptually what we need to do is set of algorithmic steps and that’s called “*ToPrimitive(hint)*” or a function that can be evoked.
  ![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649186228426_image.png)


Hint is optional type hint, what kind of type u like it to be if u want a *“number”* operation and invokes ToPrimitive, hint would send “i would like to have a number”, its more like the place im using this i like it to be a number. 

String, what hint is gonna send in, its gonna send in *“string”.*

“*I like it to be a number string or im not gonna tell u all just gimme any primitive u can.”*

*Its good to understand that algorithms in JS are inherintly recursive, wich means ex. they define something like ToPrimitive so if return result is not primitive is like an object for ex. then its gonna invoke again recursevly until we get an acctual primitive or some cases error.*

There are two methods that can be available on any ***non primitive*** any object function array, any non primitive ***valueOf()*** and ***toString()*** function. 


## Abstract Operations: *ToPrimitive(hint)*


                                *Hint:* *“number”*
                                
        This algorithm says if u told me that hint is “number” then im first  gonna try to invoke valueOf if its there and see what it gives me if it gives me primitive then done, if it doesn’t give it then we try toString() and we get an primitive or not. If both of those doesn’t give primitive generally that’s gonna resulting an error. 


                                 hint: “string” 
                                
        If the hint was “string” the order is just reverses first its toString() then ValueOf() function. 

Just keep in mind if u gonna use something that is not a primitive in some place that need to primitive like math or concatination in your mind u should realize it is going to end up **coercing** it through this two primitive algorithms ***toString*** and ***valueOf.***

**ToString** *(7.1.12 ES2018)*

Abstract operation, it takes any value and gives us the representation of that value in string form. Examples:


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649187460158_image.png)


                                     -0 toString operation lies and produces 0


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649187614387_image.png)


If we call ToString(object) its goning to invoke the ToPrimitive(string) and thats gonna end up calling toString() / valueOf(). Its gonna look like: 

![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649187631987_image.png)



- if its an array, what hasppens is a *serialization an representation of array to a “”* 
- its strange because they are leaving off the brackets. 
- They are a bunch of things that serializes to string so how we are suppose to know if it was like an empty array.
- Even wierder ***null, undefined*** why ? return **“,” bad inconsistency**

**ToString(object)**

The default toString on the object or prototype is “[object Object]”. If you override the toString u can make it return what ever u want. If i want to know and understand whats in a object u can define it as a getter so dinamically like to JSON information about object. 

![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649188165531_image.png)


**ToNumber** 

Some of them are well formed, some of them are strange. Empty string “” is 0, problem is that in thinking: empty string means i don’t have a value and 0 is a value in many senses ( math ) …    *instead returning* ***NaN***   **

![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649188419438_image.png)


Numerification of string is fine but has bit strange behaviour, suprisingly it handles very well the ***hexDec*** value :)

What about dealing with this primitives:

![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649188714329_image.png)



- Historically false and true 0/1 is a logical thing, but thinking later on  it should be NaN  … greater programming is what ppl expect. 
- undefined becomes ***NaN*** ?! here they decided to put NaN but didnt use it with ***null.***

**ToNumber(Array/Object)** 


- When we use ToNumber to a non primitive invokes ToPrimitive(with number hint) aka: valueOf/toString 
- what does that look like:
  ![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649196227493_image.png)



    First consults value then tostring. For any array or object by default meaning u have not overriten this valueOf return this, wich has the the effect of ignoreing the value it just go directly toString(), doesnt even matter of number it just go to string, u can think of numberfication of an object as esentilally stringification, thats a perplexing  choice, wich is gonna produce string, but when u  expect a number u get string, 

**Coercion: ToNumber(Array)**

![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649196525120_image.png)



- wierd if [null] or [undefined] returns 0, because  ***first they become empty string and then they become 0*** ****
- empty string becoming 0 is the root of all evil 

 

 


**Coercion: ToNumber (Object )** 

![Coercion: ToNumber(Object)](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649196753490_image.png)


If u have a object its toString returns the object. Stringification of an object by default is [object Object] *overridable* thing. And here is definitly not a representation of a number, so we get NaN thats acctually reasonable, but u can ovverid valueOf() to return 3 for ex.  

**ToBoolean ( abstract operations )** 

Falsy will return false when coerced to boolean.  Truthy list is what falsy does not return, and its a very long list … 

![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649196976309_image.png)


ToBoolean(Array) there is not abstract operations no algorithm its just is it there or not so return will be true.  Is it on the list or not. 


     … memorize the falsy list otherwise its true … 


# Coercion


## String concatination: number to string

Most underlooked and undervalued part of JS. ***You claim to avoid coercion because it’s evil … “i just use triple === “*** 

ES6 the template literal strings. This feature for console.log and dropping stuff like numbers in there: 


    var num = 16;
    console.log(
      'There are ${num} students'
    ); // There are 16 students

This number is getting coerced. What's happening here: 


    var msg1 = "There are ";
    var num = 16;
    var msg2 = " students";
    console.log(msg1 + num + msg2); 

Why is this getting coerced,  operator overloading 

    This operator is normally though to doingwith numeric operations.
        But the spec says if u use + operator with “string”. 
             Whats happening with + ${num + “”} 


                Spec says If one of them is a “string” it preffers “string” concatenation. 
                
                Wich means if one of them is  “string” its gonna call toString () abstract operation on it! With all wierdnesses and caviats 

 Think remeber u are using coersion, lets do == insted of === 


## Coercion number to string


    var num = 16;
    console.log( 
      'there are ${[num].join("")} students'
    );

 

Throw a value into array and call .join and that acctually stringify it … there is no string concatination. The spec for .join first turns into a “string”. Don't do this its terrible idea, but if u want to be super explicit about it. 


    At least do:


    'there are ${(num).toString()}


    There is a little weirdness here, how are u calling method on primitive value, primitive values don’t have methods. So u acctually doing implicit coercion.


        So if u don’t want any implicit coercion at all, only option Is to use that fundamental object without a new keyword string, and this is my preferred way of explicitly coercing that number to a string, the capital S string function is gonna do that for you.


            Not sure if this is the great idea in all cases but that at least a way of being explicit.


                 ‘There are ${String(num)} students’ 
                        *there this is the way to be explicit about it …*

So string to, number to string but what about the other way around? 


    function addStudent(numStudents){
        return numStudents + 1;
    }
    addStudent(studentImputElem.value); // "161" oops

You're already doing that too. Dealing with web applications, which means you're dealing with user input from things like form elements and doing numeric stuff with it. 

Plus operation … string concatenation … 

Plus unary operator / force to be a number … Unary plus operator, invokes the toNumber abstract operation. Thats all it does. But if its empty string … its gonna become 0:


    function addStudent(numStudents){
        return numStudents + 1;
    }
    addStudent(+studentImputElem.value);  

Or use fundemental Number function, subj. *preffered way:*


    addStudent( Number(studentInputElem.value )); // 17


## Coerction: string to number

**Minus operator ( - )**

It is only meant to be to deal and its only defined to work with numbers, its not overloaded for concatenation with strings. So - operator is gonna invoke ToNumber abstract operation.



    function kickStudentOut(numStudents){
      return numStudents - 1;
    }
    kickStudentOut( studentInputElem.value ); // 15


## Coersion: ___to boolean

Never write if statements that use non-Booleans in the if class. Any of you use like checking to see if a string is non-empty to see whether it's truthy or not? Extremely common practice, guess what that's called coercion. Okay, and guess what? All of the weird corner cases of coercion Booleans are in a fact, even with your little simple if statements they're in a fact.


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649201674385_image.png)


Matter of fact, I would say there are more corner cases with boolean, maybe than any other premier type or kinds of wearnesses that we're gonna get into here as we go So that empty string, if students input that value as an empty string that's gonna be **falsy,** alright?

But what if that string has just a bunch of white space in it? Now it's gonna be **truthy**, It's not a valid string that you care about because it's got a bunch of white space in it but **all of a sudden it's going to be truthy**. Corner cases even with our Boolean.

People love to use the numeric coercion of a number to either a zero or a non zero for truthy or falsy, right? So if my length is zero then it becomes false and if my length is anything non zero then it becomes true. Because it's not one of the zeros, will have to rely up on that.

Except what happens when it's NaN.

As a matter of fact, implicitness can be very useful. It just simply means we have to be very careful and intentional. 


## Turn into explicit booleans


- Use double negate that becomes boolean
- Use fundamental Boolean - preffer like String and Number
- With numbers its better to use < > its semantic
- Use explicitnesin places where explicitnes is more comunicative


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649211076456_image.png)




![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649211287588_image.png)

- Boolean of empty string is false
- Boolean of non empty string is true.


## Boolean on undefined / null

It is good to treat undefined and null as indistinguishable values ( *same alike similiar* ). Where ever possible, coersion is helful for that. If the test is has this thing is set or not to an object or is it unset, its reasanble implicit Boolean coercion, only coersion thats okay. Implicit to Boolean conversion either for object or null and underfined. But for number and strings … 


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649211439040_image.png)




## Primitive to object coercion

**Boxing**

Accessing properties on primitive values, length on string, or length on number. How do we access .length, it is form of implicit conversion in spirit. Its not a object but u treat it like an object. 


    if( studentNameElem.value.length > 50 ) { ... }


## Coercion: Corner cases 


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649212134763_image.png)

- empty string, root of all evil
- null / undefined
- essentially lot of falsy values becoming numbers those are where alot of corner cases are.
- we could have eliminated if empty string is not 0
- Boolean ( new Boolean(false ) ) it is a falsy object. Never use those particular fundamentals with new keyword.


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649212351562_image.png)


Not only that empty string becomes zero,  but string full of whitespace alse becomes 0, because toNumber() operation strips all of all whitespace before it does conversion. Would be nice if it would become NaN.

**Other corner cases**


![You don’t deal with these type conversion corner cases by avoiding coercions. Instead adopt a codeing style that  makes value types plain and obvious.](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649212572871_image.png)


Corner cases thata are not as obvious because we are not dealing with typcial operation, the numberification to numbering a boolean 1 and 0 are bad idea.

**1 < 2 true**
1 < 2 < 3 … true, JS is accidentally 1 < 2 gets eval first and because u have non numberic been used with less than operator its gonna try to turn it into a number 1 and u accidentally get that 1 is less than 3 !!!

3 > 2 > 1 … OOPS fails !!! 3 > 2 is true … true > 1 is 1 > 1 wich is false !!! Its terrible idea for booleans that implicitly coarse themselves to numbers. Should be NaN.


                                A quality JS program embraces coercion, making sure the types involved in every operation are clear. Thus, corner cases are safely managed. That means that u shouldn't do all this polymorphic functions that could do 50 different things based on value. U are asking for coercion problems when u do that, why not design a function that only takes 1 number, or a f() that takes string, or num and string and its clear to take care of corner cases we have to worry about. We can choose to be more obvious how we manage our types, how polymorphic (ability to call the same method on different JavaScript object) we make our code. 


                ***JavaScript's dynamic typing is not a weakness, it’s one of its strong qualities***. 
        
                First truly multi paradigm language and big reason and its ability to survive multiparadigm is because of its type system. This is one of the best parts of JS.


                *‘a* ***paradigm*** *is a* ***distinct set of concepts*** *or thought patterns, including theories, research methods, postulates, and standards for what constitutes legitimate contributions to a field.’*


                *‘a multi paradigm is* ***allow the most suitable programming style for a task”*** 


## Implicit coercing


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649243331081_image.png)

         Most dev think implicit coercions is magical, and we tend to think Implicit is Bad. This anti-coercion perspective exists because ppl think its a downfall, where they point C++ type castnig or Java and say the Java does this automatic stuff and thats a weakness in JavaScript because its *magical and bad*. 


        Maybe best to think its either of those things ***we should think about implicitness as an abstraction***.  Not all abstractions are good but some are necessary. 


        In functional programming u use abstraction all over the place and it turns out that declaritive style of codeing is actually more implicit. So implicitness is not bad just the proper use of abstraction.

![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649243737189_image.png)

![if im wrinting String to make it super obvious that im gonna make this thing a string, i think im just gonna trop a number because i checked that its not one of those corner cases.](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649243836542_image.png)


Check **numStudents** before -**0/NaN** … So if I have if statements to check this i would skip String to make it more readable.


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649243857697_image.png)


The less then operator, we mentioned how it coarces to a number, somethimes u want to make sure they both are a “number” because if one of them are “string” it doesn’t turn both of them to numbers, the less then does the alpha numeric comparison. 

**Buuut  … if** i have checked before that one of those values is a number before in program maybe i dont need to force you to read that those should and are a return of **Number**(). 

It is good to think like this to train, make it obvious, if u communicate that intent its not gonna trip out other readers of the code.


                                **Doug Crockford**, famously said: “***If a feature is sometimes useful and sometimes dangerous and if there is a better option then always use the better option***” — *The good parts*
                                
            - This perspective we throw this principle around and we don’t even say what we mean by this words. 
            - What is usefull and what is dangerous ( what Doug things ? ) 
            - How do we define better option, is there universal description of what is better here
            - This statement is not usefull in abstract sense, its used in abstract sense but not usefull
            - This says ***Better*** option is don’t learn and understand types.


1. Usefull: when the reader is focused on what’s important
2. Dangerous: when the reader can’t tell what will happen
3. Better: when the reader understands the code


## Coercion exercise

**Working with coercion**

You will define some validation functions that check user inputs ( such as DOM elements ). You’ll need to properly handle the coercions of the various value types.

**Instructions:** 


1. Define an ‘isValidName(..)’ validator that takes one parameter ‘name’. The validador returns ‘true’ if all the following match the parameter ( ‘false’ otherwise ):


        - must be a string
        - must be non-empty
        - must contain non-whitespace of at least 3 characters


2. Define and ‘hoursAttended(..)’ validator that takes two parameters, ‘attended’ and ‘length’. The validator returns ‘true’ if all following match the two parameters (‘false’ otherwise): 


        - either parameter may only be a string or number
        - both parameters should be treated as numbers
        - both numbers must be 0 or higher
        - both numbers must be whole numbers
        - ‘attended’ must be less than or equal to ‘length’


    console.log(..) : 
    
    isValidName("Frank") === true
    hoursAttended(6,10) === true
    hoursAttended(6,"10") === true
    hoursAttended("6",10) === true
    hoursAttended("6","10") === true
    
    isValidName(false) === false
    isValidName(null) === false
    isValidName(undefined) === false
    isValidName("") === false
    isValidName("   \t\n") === false
    isValidName("X") === false
    
    hoursAttended("",6) === false
    hoursAttended(6,"") === false
    hoursAttended("","") === false
    hoursAttended("foo",6) === false
    hoursAttended(6,"foo") === false
    hoursAttended("foo","bar") === false
    hoursAttended(null,null) === false
    hoursAttended(null,undefined) === false
    hoursAttended(undefined,null) === false
    hoursAttended(undefined,undefined) === false
    hoursAttended(false,false) === false
    hoursAttended(false,true) === false
    hoursAttended(true,false) === false
    hoursAttended(10,6) === false
    hoursAttended(10,"6") === false
    hoursAttended("10","6") === false
    hoursAttended(6,10.1) === false
    hoursAttended(6.1,10) === false
    hoursAttended(6,"10.1") === false
    hoursAttended("6.1",10) === false
    hoursAttended("6.1","10.1") === false 
    
    // all should print true


**Solution:**



    function isValidName(name){
        // typeof operator always retrun non empty string, we are safely 
        // out of corner cases
        // trim () remove whitespace characters
    
        if( typeof name == "string" && 
            name.trim().length >= 3
          ){
            return true;
        }
        return false;
    }
    
    function hoursAttended(attended, length){
        // either string or num and treat as num
        if ( 
            typeof attended == "string" &&
            attended.trim() != ""
          ){
            attended = Number(attended)
        }
    
        if ( 
            typeof length == "string" &&
            length.trim() != ""
          ){
            length = Number(length)
        }
    
        // still we need to check if it a number 
    
        if ( typeof attended == "number" &&
             typeof length == "nubmer &&
             attended >=0 &%
             length >=0 &&
             Number.isInteger(attended) &&
             Number.isInteger(length) &&
             attended <= length
            ){
                return true;
            }
            return true;
    }


# 5. Double and triple equality == vs ===


## 

**Loose Equality vs Strict Equality:** Unfortunately even if this sounds good its not exactly the case. The difference really changes our perspective on the purpose of these two mechanisms. If you’re trying to understand your code, it’s critical you learn to think like JS.  One of the big coercion problem seem to be around equality check. 



    **==   checks value ( loose )** 
    === checks value and type ( strict )


## Spec: == Abstract Equality Comparison *( 7.2.14 )*


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1652955597757_image.png)



            **Abstract Equality Comparison means double equals ==**
            
            If double equals only checks the value, and triple equals checks value and the type then why on the very top of the algorithm in spec the are the types x and y checked, **double also checks the type**  **but just that one does something different with that information than the other “===”.**
            
            For ex. if I have string assigned to one variable and on line 2 i made a copy, and in line 7 and 8 I ask if those two are equal. Because it turns out when the types match then they do the ===.  


            The double equals == and the triple equals === are exactly the same when the types are equal in this case string. The specs says when the types match do the triple === even if u set the double equals == !!! 
            
            U should try to have the value types obvious and ideally u should try to have them matching as much as possible.


![ES6 tmpl. `${student1}`; not ‘’](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649278583969_image.png)



## Spec: === Strict Equality Comparison  *( 7.2.15 )*


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1652956556730_image.png)


Triple equals checks the types and if they are not the same returns ***false.*** 
If the types are same: 

        - return false if they are **NaN (** its suppose to lie about NaNs **)**
        - return true if they are **-0** **(** suppose to lie about -0 **)**

Equality comparison does IDENTITY comparison, so it looks at two objects does not go deep into structure of the object, and in memory the addresses are different, in other words no deep structure comparison, they are different objects !!!


     var workshop1 = {
        name: "Deep JS"
    }
    var workshop2 = {
        name: "Deep JS"
    }
    if( workshop1 == workshop2 ) { // nope }
    if( workshop1 === workshop2 ) { // nope }
                        
                            in another words:

![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649279274162_image.png)



## Coercive equality

Spec 7.2.14 Abstract Equality Comparison says on line 2 and 3:


2. If x is null and y is undefined, return **true**
3. If x is undefined and y is null, return **true** 

end - return **false**  *// on end of algorithm* 

![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1649279471551_image.png)



- Maybe it is maybe it isn’t. Critical analysis it shifts the discussion == is bad an unpredictable, do I want to allow == or don’t. Is it more helpful, safe ? 
- In other words u need to be critical analytical thinker, and look at your code and decide what u can do with code. 

The decision of double and triple equals is trailing indicator that u actually understand your program.

Your choice to use === is just because some guy wrote in a book is to always use it, but the trailing indicator back to the fact that there is something unknown in program. Maybe is better to fix the root problem. Make types obvious.


    **If the types are null or undefined they are coercively equal to each other and it returns true. They are only coercive to each other.** 
    
    **Its is useful to JS because we don’t like to have 2 empty values, and since null is shorter type then undefined, we can pretend as much as possible that undefined does not exist, or at least that they are interchangeable** ***(*** *dinner and supper )* ! ****
    
    **JS does make some distinction between them such as default value algorithm.**  

******

                *But for the most part u have option to treat null or undefined as indistinguishable through coercive equality!*  
    
    U can do a check like this: 

**Coercive Equality: null == undefined**  

Use null because its same and its shorter to type.


    var workshop1 = { topic: null }
    var workshop2 = {}
    
    if( 
        ( workshop1.topic === null || workshop1.topic === undefined ) &&
        ( workshop2.topic === null || workshop2.topic === undefined ) &&
    ){
       //...
    }
    
    if(
        workshop1.topic == null &&
        workshop2.topic == null
      ){
        //...
      }


- U can been asking your self that **topic** **property** is ever been created 

- That it been reset back to **null** 

- Or its never been set at all and its been set its undefined

- Those are basically same condition

- U can try to distinguish between those two **but in almost in all cases that's not useful distinction.** 
            

      - Whether the property has ever been created, and has been reset back to null or reset back to undefined or whether it was never created at all those are basically same condition. 
      - One option is to use === and explicitly checks all those cases
              - Are you getting readability here as being **explicit line 5,6**
              - No there is no benefit here
      - **using double ==** on **12,13**  **is far more clear**. It says whether they are null or undefined, tell me if one of those two values are empty or not. And its less to type then **5,6 line.** 


        *ESLint tool and turn on rules to help to write better code.*


## Double equals == algorithm

If we are not talking about nulls and undefines, but strings numbers and booleans, this algorithm prefers to do numeric comparison. Just knowing in the back of your head that the double equals likes the ToNumber() - numeric comparison.

***Spec (7.2.14)*** **IsLooselyEqual ( x, y )**

***Coercive Equality: prefers numeric comparison***


    If we are not talking about nulls and undefined, but Strings and numbers and booleans, from 4 to 7. it prefers to do numeric comparison. But just by knowing that it helps you to predict the double equals algorithm. Instead of two strings are getting compared two numbers are getting compared. That one fact separates you for 99% javascript developers, cause they never read the spec. 



1. If **Type(x)** is the same as **Type(y)** then … return the result of performing **Strict Equality Comparison** **x === y**
2. If **x** is **null** and **y** is **undefined**, return **true**
3. if **x** is **undefined** and **y** is **null**, return **true** 
4. If **Type(x)** ****is **Number** and **Type(y)** is **String**, **return the result of comparison**  
   **x == !ToNumber(y)**
5. If **Type(x)** is **String** and **Type(y)** is **Number**, return the result of comparison **!ToNumber(x) == (y)**
6. If **Type(x)** is **Boolean**, return the result of comparison !**ToNumber(x) == y**
7. If **Type(y)** is **Boolean**, return the result of comparison **x == !ToNumber(y)**
8. If **Type**(x) is either **String**, **Number**, or **Symbol** and **Type(y)** is **Object**, return the result of the comparison **x == ToPrimitive(y).**
9. If **Type(x)** is **Object** and **Type(y)** is either **String**, **Number**, or **Symbol**, return the result of the comparison **ToPrimitive(x) == y.** 
10. **return false**


( toPrimitive tries to call the `[toString](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)` method. If the `toString` property does not exist, it tries to call the `[valueOf](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf)` method and if the `valueOf` does not exist either, `[@@toPrimitive]()` throws a `[TypeError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypeError)`)


 ***Example:***

If I had a tripe equals and different types its always gonna fail. So I have to make them numbers.  Line 4.

Or we could structure code that coercion is obvious and useful system rather then the magic most people feel.

If both of them were strings, it means they are the same type it does the triple equals. 

The double equals is going to allow the coercion when the types are different, if u are in a scenario when the types are not different then its not ever gonna invoke coercion.


    var workshopeEnrollment1 = 16;
    var workshopeEnrollmetn2 = workshopenrollment1.value;
     
    if( Number(workshopEnrollment1) === Number(workshopEnrollment2)){
        // If i have a number and a string 1 and 2 lines, if i do a triple 
        // equals of course i will have to forcibly make them numbers to do 
        // a comparison, they have to be the same type. 
    }
    
    // Ask what do we know about the types here? 
    if(workshopEnrollment1 == workshopeEnrollment2){
      //...
    }

 

Specs: clause 8 & 9: If u use == with something that’s not a Primitive, we invoke the ToPrimitive abstract operation ( that's the one that calls the valueOf() or toString() operation). The double equals only compares the Primitives. If its comparing to non Primitive its gonna turn it to a Primitive.  

The only time it does something useful with non Primitive with exact the same type its gonna use tripe equals === comparison.

Otherwise the only coercion step i care about now its getting you to be a Primitive, and then it will consider if the primitives are the same type or not. This algorithms are inherently recursive, the double equals == algorithm says “I need to get to the point where one of these spec. clauses matches, and if it doesn't match completely then im gonna rerun the algorithm over and over again until i get it done to two primitives of the same type or the two primitives that can be coercively equal to each other, and if i never get to that point, then clause 10. return false”. They are not equal. In other words we invoke the two primitives and we get back to the algorithm with our two primitives.


**Double equals walkthrough**



    var workshop1Count = 42;
    var workshop2Count = [42];
    
    if( workshop1Count == workshop2Count){
      // ... hmm
    }

What invoke the == algorithm to see what it’s actually doing under it’s covers:

This is an one of those example where coercion is bad for us


    if(workshop1Count == workshop2Count){
    if(42 == "42"){ // it first says ToPrimitive wich makse array an string
    if(42 === 42){  // and its acctidently working because thers is only one 
                    // item in array
    
    // now, we have two different types number and string, there is two options here, we can either make a number into a string and compare that, or make the string into a number and compare the numbers.
    
    // wich happens in the ALGORITHM it PREFFERS THE NUMBER, and now in number 4 line it does the triple equals because the types are the same.


    if(true){
      // hmm ... yep
    }

U should never fix this problem by using ===, prevents you to see a real problem which is to see you are making a terrible comparison in first place.


                        **Summary** 


                            Triple equals: 
                            If the types are the same: ===
                            If null or undefined: equal
                            If non-primitives: ToPrimitive
                            Prefer:ToNumber


## Corner Cases

**Double equals Corner Case** ***WAT!***


      [] == ![] // true WAT!
        // this is false construct u will never compare 
        // value to the negation of itself
      
    var workshop1Students = [];
    var workshop2Students = [];
    
    if(workshop1Students == !workshop2Students){
        // yep ... WAT!?
        // if ([] == false){ 
        // if( "" == false){
        // if( 0 == false){
           if(true){
              // yep ... WAT!?
           }
    }
    
    if(workshop1Students != workshop2Students){
        // yep ... WAT!?
        // if(!(workshop1Students != workshop2Students)){    
        // if(!(false)){    
        if (true){
          // yep ... WAT!?
        }
    }
    
    // 1.case - lines:  
    
    10. - reduce workshop1Students to array → []
        - negate workshop2Students array → wich is truthy and becomes false
    11. NOW we have nonprimitive compare to primitive -> "" 
        we have two primitivies but they are not the same type, the 
        algorithm prefers them to be the same type, so in line 
    12. string becomes wich 0 is shoudn't, but becomes number zero instead 
        of NaN, and false needs to become a number and it becomes a zero
    
    // 2.case:  
    
    // much more rational, if we look at the equivalent of not equals its basically
    // the negation of coercive equality ... so we can ask our selves does it 
    // make sense for workshop1Students to be coercievly compared to other 
    // workshop2Students well since they both arrays then what we are effectively 
    // doing is ASKING an IDENTITY QUESTION ! And it would would identitcally if
    // we would use === version of this

**Boolean Corner Case**

If u want to allow the boolean coercion of an array to be true, in other words u wanna say its ***TRUTHY*** construct.

One way: is with ***if statement*** ( line 3 ) allow the if statement to invoke the to boolean operation on the array, that says the array is not on the table there fore its true … [Abstract Equality Comparison Algorith](https://262.ecma-international.org/5.1/#sec-11.9.3)m


    [] == false; // convert false to Number
    [] == 0;     // convert [] to Primitive (toString/valueOf)
    "" == 0;     // convert "" to Number
    0  == 0;     // done 

Next, tricky, if its *TRUTHY* then i want to do a double equals with *== true.* And now it suddenly doesn’t work, and btw it wouldn't work with triple equals either, because a comparison of a boolean to an array is gonna go through bunch of those corner cases, and u are gonna get unintuitively *false*. U think this thing is truthy, its not double equals true but it is == false. 


                            So never do double equals with true or false


            ***Because there is not a scenario when u need to do == true or == false, when u could just do to boolean implicitly if(workshopStudents)***


    var workshopStudents = [];
    
    if(workshopStudents)
        // Yep
    
    if(workshopStudents == true)
        // Nope :(
    
    if(workshopStudents == false)
        // Yep :(


                        *Lets explain how == true fails, and == false does not*


    if(workshopStudents) {
    if(Boolean(workshopStudents)){
    if(true){
        // yep 
    }
    
    if(workshopStudents == true) { 
    // we have a non primitive wich has to become primitive 
    if("" == true){
    if(0 === 1){ // 0 should have become NaN
    if(false){
        // Nope :(
    }
    
    if(workshopStudents == false){
    if("" == false){
    if(0 === 0){
    if(true){
      // Yep :(
    }


                    *So, this is non sensical outcome to this scenario what was non sensical outcome, u don’t need == true, == false, so in this case implicit has a good outcome and explicit does not !*


                            *Implicit is sometimes better then explicit !*
                            
                    Scenario of this construct ( code ) is i wanna know if it is set or not, i know it can be unset or set to an array. If we didn’t know that if it is set or unset or set to other varieties of things array, object, string, then we would wanna do go into deeper checking scenarios then just to boolean conversion, then first check that is acctually set then the next check something about its identity. There is various ways to do that, u could use TypeOf() operator, u could do if the method is on it .lenght, u could do actual utillity Array.IsArray().


                    *“****Duck typing*** *is an application of the* [*duck test*](https://en.wikipedia.org/wiki/Duck_test)*—"If it walks like a duck and it quacks like a duck, then it must be a duck"— determine whether an* [*object*](https://en.wikipedia.org/wiki/Object_(computer_science)) *can be used for a particular purpose.”*


**Summary - Corner Cases Avoid**


- == with 0 or “” (or even “ “) 
- == with non-primitives, even with identity comparison. Only use it with coercion among the primitives
- == true or == false : allow Boolean() or use === ( essentially just allow Boolean ()to happen its better outcome, or if u really cant allow that, then use triple === ).

**The Case For Double Equals ( preferring == )**

U should prefer double equals in all cases, lets make a case where == is always better than ===. 


- Knowing types is always better than not knowing them. The uncertainty of your code makes it hard to read prone to errors. Some people respond to that problem by not knowing types by saying “I need to change my coding style to use static typing” like TypeScript and others.

      == is not about comparison with unknown types


                    == is about comparisons with known type(s). optionally
                                      where conversions are helpful 
                            
                            never use the == if u don't know the types. Only
                                      use the == when u know the types


                        **If you know the type(s) in a comparison:** 
                            If both types are the same. **==** is identical to **===**
                                Using **===** would be **unnecessary** ****so prefer the shorter **==**

- Static Types is not the only ( or even necessarily best) way to know your types


                    If u know the type(s) in  a comparison: and if the types are different, using === would be **broken.**


                    Summary: whether the types match or not, == is the 
                                        more sensible choice 


                    Not knowing the types means not fully understanding
                              that code, refactor if possible, comment, communicate
                                      the intent, make it obvious … === is the signal that 
                                              the type is unknown and its for *protection*


![equality is JavaScript](https://www.freecodecamp.org/news/content/images/2020/03/image-6.png)


**Equality Excercise**


    # Wrangling Equality
    
    In this exercise, you will define a `findAll(..)` 
    function that searches an array and returns an
     array with all coercive matches.
    
    ## Instructions
    
    1. The `findAll(..)` function takes a value and an array. 
    It returns an array.
    
    2. The coercive matching that is allowed:
    
      - exact matches (`Object.is(..)`)
      - strings (except "" or whitespace-only) can match numbers
      - numbers (except `NaN` and `+/- Infinity`) can match strings 
        (hint: watch out for `-0`!)  - `null` can match `undefined`, 
        and vice versa
      - booleans can only match booleans
      - objects only match the exact same object



    // -------------    SOLUTION: 




    function findAll(match,arr) {
      var ret = [];
      for (let v of arr) {
        if (Object.is(match,v)) {
          ret.push(v);
        }
        else if (match == null && v == null) {
          ret.push(v);
        }
        else if (typeof match == "boolean" && typeof v == "boolean") {
          if (match === v) {
            ret.push(v);
          }
        }
        else if (typeof match == "string" && match.trim() != "" && typeof v == "number" && !Object.is(-0,v)) {
          if (match == v) {
            ret.push(v);
          }
        }
        else if (typeof match == "number" && 
          !Object.is(match,-0) && 
          !Object.is(match,NaN) && 
          !Object.is(match,Infinity) && 
          !Object.is(match,-Infinity) && 
          typeof v == "string" && 
          v.trim() != ""
        ){
          if (match == v) {
            ret.push(v);
          }
        }
      }
            return ret;
    }


​    

    // tests:
    var myObj = { a: 2 };
    
    var values = [
            null, undefined, -0, 0, 13, 42, NaN, -Infinity, Infinity,
            "", "0", "42", "42hello", "true", "NaN", true, false, myObj
    ];
    
    console.log(setsMatch(findAll(null,values),[null,undefined]) === true);
    console.log(setsMatch(findAll(undefined,values),[null,undefined]) === true);
    console.log(setsMatch(findAll(0,values),[0,"0"]) === true);
    console.log(setsMatch(findAll(-0,values),[-0]) === true);
    console.log(setsMatch(findAll(13,values),[13]) === true);
    console.log(setsMatch(findAll(42,values),[42,"42"]) === true);
    console.log(setsMatch(findAll(NaN,values),[NaN]) === true);
    console.log(setsMatch(findAll(-Infinity,values),[-Infinity]) === true);
    console.log(setsMatch(findAll(Infinity,values),[Infinity]) === true);
    console.log(setsMatch(findAll("",values),[""]) === true);
    console.log(setsMatch(findAll("0",values),[0,"0"]) === true);
    console.log(setsMatch(findAll("42",values),[42,"42"]) === true);
    console.log(setsMatch(findAll("42hello",values),["42hello"]) === true);
    console.log(setsMatch(findAll("true",values),["true"]) === true);
    console.log(setsMatch(findAll(true,values),[true]) === true);
    console.log(setsMatch(findAll(false,values),[false]) === true);
    console.log(setsMatch(findAll(myObj,values),[myObj]) === true);
    
    console.log(setsMatch(findAll(null,values),[null,0]) === false);
    console.log(setsMatch(findAll(undefined,values),[NaN,0]) === false);
    console.log(setsMatch(findAll(0,values),[0,-0]) === false);
    console.log(setsMatch(findAll(42,values),[42,"42hello"]) === false);
    console.log(setsMatch(findAll(25,values),[25]) === false);
    console.log(setsMatch(findAll(Infinity,values),[Infinity,-Infinity]) === false);
    console.log(setsMatch(findAll("",values),["",0]) === false);
    console.log(setsMatch(findAll("false",values),[false]) === false);
    console.log(setsMatch(findAll(true,values),[true,"true"]) === false);
    console.log(setsMatch(findAll(true,values),[true,1]) === false);
    console.log(setsMatch(findAll(false,values),[false,0]) === false);
    
    // ***************************
    
    function setsMatch(arr1,arr2) {
            if (Array.isArray(arr1) && Array.isArray(arr2) && arr1.length == arr2.length) {
                    for (let v of arr1) {
                            if (!arr2.includes(v)) return false;
                    }
                    return true;
            }
            return false;
    }


**MDN Comparison table == & ===**

*https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness*

| x                   | y                   | `==`      | `===`     | `Object.is` | `SameValueZero` |
| ------------------- | ------------------- | --------- | --------- | ----------- | --------------- |
| `undefined`         | `undefined`         | `✅ true`  | `✅ true`  | `✅ true`    | `✅ true`        |
| `null`              | `null`              | `✅ true`  | `✅ true`  | `✅ true`    | `✅ true`        |
| `true`              | `true`              | `✅ true`  | `✅ true`  | `✅ true`    | `✅ true`        |
| `false`             | `false`             | `✅ true`  | `✅ true`  | `✅ true`    | `✅ true`        |
| `'foo'`             | `'foo'`             | `✅ true`  | `✅ true`  | `✅ true`    | `✅ true`        |
| `0`                 | `0`                 | `✅ true`  | `✅ true`  | `✅ true`    | `✅ true`        |
| `+0`                | `-0`                | `✅ true`  | `✅ true`  | `❌ false`   | `✅ true`        |
| `+0`                | `0`                 | `✅ true`  | `✅ true`  | `✅ true`    | `✅ true`        |
| `-0`                | `0`                 | `✅ true`  | `✅ true`  | `❌ false`   | `✅ true`        |
| `0n`                | `-0n`               | `✅ true`  | `✅ true`  | `✅ true`    | `✅ true`        |
| `0`                 | `false`             | `✅ true`  | `❌ false` | `❌ false`   | `❌ false`       |
| `""`                | `false`             | `✅ true`  | `❌ false` | `❌ false`   | `❌ false`       |
| `""`                | `0`                 | `✅ true`  | `❌ false` | `❌ false`   | `❌ false`       |
| `'0'`               | `0`                 | `✅ true`  | `❌ false` | `❌ false`   | `❌ false`       |
| `'17'`              | `17`                | `✅ true`  | `❌ false` | `❌ false`   | `❌ false`       |
| `[1, 2]`            | `'1,2'`             | `✅ true`  | `❌ false` | `❌ false`   | `❌ false`       |
| `new String('foo')` | `'foo'`             | `✅ true`  | `❌ false` | `❌ false`   | `❌ false`       |
| `null`              | `undefined`         | `✅ true`  | `❌ false` | `❌ false`   | `❌ false`       |
| `null`              | `false`             | `❌ false` | `❌ false` | `❌ false`   | `❌ false`       |
| `undefined`         | `false`             | `❌ false` | `❌ false` | `❌ false`   | `❌ false`       |
| `{ foo: 'bar' }`    | `{ foo: 'bar' }`    | `❌ false` | `❌ false` | `❌ false`   | `❌ false`       |
| `new String('foo')` | `new String('foo')` | `❌ false` | `❌ false` | `❌ false`   | `❌ false`       |
| `0`                 | `null`              | `❌ false` | `❌ false` | `❌ false`   | `❌ false`       |
| `0`                 | `NaN`               | `❌ false` | `❌ false` | `❌ false`   | `❌ false`       |
| `'foo'`             | `NaN`               | `❌ false` | `❌ false` | `❌ false`   | `❌ false`       |
| `NaN`               | `NaN`               | `❌ false` | `❌ false` | `✅ true`    | `✅ true`        |



# Scope 


## JIT Compiler


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1655706222808_image.png)


Parses entire code into machine code and then executes right away after compalation. Two steps, when source code is compiled into machine code its doesn’t produce “portable file” and thats why that machine code needs to be executed imedietly to run the program.  


## JS Engine and compilation

We have to think of JavaScript and its compilation/parsing as a two pass system rather than one single pass. Its about thinking scope correctly. Lazy/eager.

First thing that  happen in JS enging is that JS code is parsed by the engine in code line by line and checkes if the syntax in the code is correct. 

Parsing simply means that engine reads the code line by line, if there is not error the parser created the structure known as abstract syntax tree (AST). It splits the code into meaningful blocks and place them into their own spots in memory in a structured way and this is used by the JIT machine code. This is how AST looks like.

![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1655707005417_image.png)


Next step is compalation and it uses JIT compiler, this machine code gets executed right away. Execution happens with JS call stack. Even though the program is executign modern engines optimizes have compliation strategies, the clear the unoptimized version of machine code and in background this code is optimized and recompiled and this can be done multiple times.  


![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1655707497856_image.png)



## Lexical Scope

**Lexical scope** is the ability for a function scope to access variables from the parent scope. We call the child function to be lexically bound by that of the parent function. The diagram below outlines the supposed hierarchy that the lexical scope maintains in JavaScript.

We need to understand lexical scope, to understand closure so we can understand the module pattern. Scope is where to look for things. What it is what we are looking for. 

Where those buckets comes from, to identifies or the marbles, the buckets are units of scope, JavaScript organizes scope with *functions* and *blocks.* 


    var teacher = "Kyle";
    
    function otherClass(){
      var teacher = "Susy";
      console.log("welcome");
    }
    
    function ask(){
      var question = "why";
      console.log(question);
    }
    
      otherClass();  // Welcome
      ask();         // Why

Compiler, and scope manager which makes the buckets and puts marbles in them. 

We should not think of JS as interpreter language step by step one line at the time rather we think  of it as two pass compiler. First pass processing parsing/compilation, through entire code, main thing that that happen is scope is planned and memory is organized all id and references, second pass is eval. First pass, compilation ( scope manager ), second pass execution.


      var name = "moje ime"
      console.log("executed")
      
      function vrati (){
        console.log (name);
      }
      return vrati;  
    }
    
    var n = nekaj();
    n();
    executed'
    'moje ime'



    function doAddition(x){
      return function(y){
        return x + y;
      }
    }
    var add5 = doAddition(4)
    add5(5);
    doAddition(5)(5)

![](https://paper-attachments.dropbox.com/s_09A48F14AA95F65EF9FA2C5ED493B645E7007F12C8D944F4FCC8B997FE7ECE70_1655710475659_image.png)


Another ex:


    var a = 10; // variable a assigned to 10
    var func = function (){ // outermost function
        var b = 20;
        console.log("a and b is accessible (outer):", a, b);
        var innerFunc= function (){ // innermost function
            var c = 30;
            console.log("a and b and c is accessible (innner):", a, b, c);
        }
        innerFunc();
        return;
    }
    func(); // invoke function func 
    console.log("only a is accessible (global):", a);


    Output
    0.87s
    a and b is accessible (outer): 10 20
    a and b and c is accessible (innner): 10 20 30
    only a is accessible (global): 10


​    

In the above code, the value of variable `a` is accessible by all function scopes since it is in the global scope. Meanwhile, variable `b` is not accessible outside the function assigned to `func`. This is because the variable is of local scope for the function assigned to variable `func`. Another thing to note is that the function assigned to the `innerFunc` variable *can* access variable `b` and `c`. This is because the inner functions are lexically bound by the outer functions.


> **NOTE:** JavaScript uses a scope chain to find variables accessible in a certain scope. When a variable is referred to, JavaScript will look for it in the current scope and continue to parent scopes until it reaches the global scope. This chain of traversed scopes is called the **scope chain**.

**Compilation Review**

*Example no. 1*


    1. var teacher  = "Kyle";
    
    2. function otherClass(){
       4.  teacher = "Susy
       5.  topic = "React"
       6.  console.log("welcome")
    }
    
    3. otherClass()   // welcome
    
    teacher;       // 
    topic;         // 

**Corner cases:** process begins by compiler talking to scope manager,  and compiler says on line 1. hey scope manager hey global scope I have a reference ( i have a formal declaration ), in execution it will be a target reference, so during my compilation i have a formal declaration for teacher did u hear of it before … NO, this is is in compilation stage, so put it in memory address #1, now … we have formal declaration on line 3 … hey global scope we have formal declaration for identifier called otherClass ever heard of it … NO … so we need to put it in memory #2, so global scope thats  a function, make a space in memory #1 and now we step into that scope and we process its plan. 

So where is next formal declaration we find ? From the perspective of the compiler we don’t have a formal declaration. We step out to the global scope. So now it executes it scope there are no more formal declarations but executable statements!

Line 1 is executable statement and so we are the engine, and global scope identifies what kind of reference? Target reference for **teacher** did I ever identified it and the answer is yes! Here is your space. 

So we are gonna move from the function to the next execution code which would be **line 9.** How does line 9 execute ? Global scope searches and searches for what kind of reference here ? **Source reference**  ( we have a source reference for **otherClass()**. Now it creates the space for it, so what do we  find in that space ? A **reference to the function** with we call the otherClass(), so we find that function and we execute it on line 9, and execution moves to the line 4, we find a what kind of **reference? A target reference** because it is receiving an **assignment** ***teacher = “something”;***, now the global scope searches for this assignment, so we are reassigning it wasn’t shadow because we didn’t assign to another function.


In  *Example No.1.* **what happens with topic ( line 5 ), so the scope of otherClass() we have a … ( what kind of reference ? ) = target reference for the identifier **topic,** now the scope searches for it, and next global scope searches for the **topic** so **NOW the answer should be NO! but this is the historical BAD PARTS … this program is not running in strict mode.**

Even though we declared a ***auto global variable*** **topic** is assign to global object in compile time and runtime there are differeneces ( perfomance ), but mechanically they are two global var at this point. 

Never declare auto globals like that, always declare var u are gonna use in what ever scope u need them in. 

The reason that happens is that this program is not running in **strict mode**. 

**Line 11**, execution of this line: global scope is looking for teacher **AFTER executing otherClass**(), looks up for ***source reference*** to a var called teacher, and returns value string suzy.  Another example:


Another same example without strict:


    var topic = "topic"
    function fun(){
      toGlobal = "in window"
      console.log(toGlobal)
    }
    fun()
    topic;
    toGlobal;
    
    //'in window'
    //'topic'
    //'in window'

**Strict Mode** 

If now we flip to “use strict” mode, when it comes to line 7 in *Example No.1* , and compiler asks “hey scope of” otherClass() i have this target reference **topic “**ever heard of it? ” …  ReferernceError ( it is different then the TypeError; “*its when u find the variable and the value that it is holding is not legal to what u trying to do, exec a fun, access a property, undefined null … ”* ). A ReferenceError is I cant find the var.

If u using Babel, its possible or certain that it is gonna use strict mode automatically.

*Example with strict:*


    "use strict";
    
    var topic = "topic"
    function fun(){
      toGlobal = "in window"
      console.log(toGlobal)
    }
    fun()
    topic;
    toGlobal;
    
    //ReferenceError: toGlobal is not defined

**Nested Scope**

*Example no.1*


    var teacher = "Kyle";
    
    function otherClass(){
      var teacher = "Suzy"
      
      function ask(question){
        console.log(teacher, question)
      }
      ask("why?")
    }
    
    otherClass()
    ask("???") - reference error  
    
    // 'Suzy' 'why?'

Line 6 is declaration that creates another scope in otherClass, function declaration make their indentifier in inclosing scope.



**Dynamic Global Variables**


            In JavaScript, dynamic variable names can be achieved by using 2 methods/ways: 


1. **eval()**


        for(i = 1; i < 5; i++) {
            eval('var ' + k + i + '= ' + i + ';');
        }


2. **window[‘value’  + i]**


     for(i = 1; i < 5; i++) {
            window['value'+i] = + i;
        }




> **Shadowing:** Now, when a variable is declared in a certain scope having the same name defined on its outer scope and when we call the variable from the inner scope, the value assigned to the variable in the inner scope is the value that will be stored in the variable in the memory space

    function func() {
        let a = 'Geeks';
          
        if (true) {
            let a = 'GeeksforGeeks';  // New value assigned
            console.log(a); 
        }
        console.log(a); 
    func();
    // output:
    GeeksforGeeks
    Geeks

# Function Expressions and Scope

Talking about functions in compilation  faze adding their identifier as colored marble in the enclosing scope 


    - red marble: in global enclosure scope
    - blue marble: own scope
    
    *Line 1.* *function declaration*
    *Line 3.* *function expression*  **


    function teacher(){} :red marble
    
    var myTeacher = function anotherTeacher(){ :blue marble  
        console.log(anotherTeacher)
    }
    
    console.log(teacher) 
    console.log(myTeacher)
    console.log(anotherTeacher) // global scope: RefferenceError!


- Function declaration: if the word function is literally the first thing in the statement.
- Function expression: no name so we call this anonymous function expression 


    *Key differences: function declarations / function expressions;* *declarations* *add their name to the* *enclosing* *scope, where* *function expressions put their identifier into their own scope.* 


**Named Function Expressions** 


    var clickHndlr = function(){}
    var keyHandler = function keyHandler(){}


        Anonymous function expressions are vastly more common, more popular. Always use named function expressions. Name produces reliable self reference inside of itself, that is useful for recursion, if the function is event handler ( needs to reference itself to bind and unbind itself ), its useful if u need to access any properties on that object, such as name, length or some of that sort. 


        More debuggable stack traces, it shows up in stack trace. Handle user click its gonna display it. 


        More self-documenting code. If the func. is anonymous i have to read the function body, and where it has been passed to get the purpose of the code. 


        Passing a anonymous function expression in callbacks, .map .then 99.9% cases, they pass them inline directly to other functions, but there is no way to conclude any name from it, so u don’t get that benefit of name reference. 


        If u are gonna pass the function expression “inline”, put a name on it like u would have if it was a function declaration. Don’t be lazy to come up with the name.
    
        If u cannot find a name for it, ***“it means”*** u don’t understand the function, or it needs to be fragmented into smaller pieces, its a leading indicator of more problematic code. 


        But function **declarations** are absolutely necessary, if the function has 3 lines of code then inline is fine, but **expression** if it needs to be called multiple times even if it is one line. 

**Arrow functions**


    var ids = people.map(person => person.id);
    
    var ids = people.map(function getId(person){
      return person.id;
    });

**Function Types Hierarchy**

*(Named) Function Declaration* 

    *> Named Function Expression* 
            *> Anonymous Function Expression*

**Function Expression EX.**

**Note:** The spirit of this exercise is to use functions wherever possible and appropriate, so consider usage of array utilities `map(..)`, `filter(..)`, `find(..)`, `sort(..)`, and `forEach(..)`.


- Instructions (Part 1)

**Note:** In Part 1, use only function declarations or named function expressions.
You are provided three functions stubs -- `printRecords(..)`, `paidStudentsToEnroll()`, and `remindUnpaid(..)` -- which you must define.
At the bottom of the file you will see these functions called, and a code comment indicating what the console output should be.

1. `printRecords(..)` should:
   - take a list of student Ids
   - retrieve each student record by its student Id (hint: array `find(..)`)
   - sort by student name, ascending (hint: array `sort(..)`)
   - print each record to the console, including `name`, `id`, and `"Paid"` or `"Not Paid"` based on their paid status
2. `paidStudentsToEnroll()` should:
   - look through all the student records, checking to see which ones are paid but **not yet enrolled**
   - collect these student Ids
   - return a new array including the previously enrolled student Ids as well as the to-be-enrolled student Ids (hint: spread `...`)
3. `remindUnpaid(..)` should:
   - take a list of student Ids
   - filter this list of student Ids to only those whose records are in unpaid status
   - pass the filtered list to `printRecords(..)` to print the unpaid reminders


- Instructions (Part 2)

Now that you've completed Part 1, refactor to use **only** `=>` arrow functions.
For `printRecords(..)`, `paidStudentsToEnroll()`, and `remindUnpaid(..)`, assign these arrow functions to variables of such names, so that the execution still works.
As the appeal of `=>` arrow functions is their conciseness, wherever possible try to use only expression bodies (`x => x.id`) instead of full function bodies (`x => { return x.id; }`).


**
    function getStudentFromId(studentId) {
            return studentRecords.find(function matchId(record){
                    return (record.id == studentId);
            });
    }
    

    function printRecords(recordIds) {
            var records = recordIds.map(getStudentFromId);
    
            records.sort(function sortByNameAsc(record1,record2){
                    if (record1.name < record2.name) return -1;
                    else if (record1.name > record2.name) return 1;
                    else return 0;
            });
    
            records.forEach(function printRecord(record){
                    console.log(`${record.name} (${record.id}): ${record.paid ? "Paid" : "Not Paid"}`);
            });
    }
    
    function paidStudentsToEnroll() {
            var recordsToEnroll = studentRecords.filter(function needToEnroll(record){
                    return (record.paid && !currentEnrollment.includes(record.id));
            });
    
            var idsToEnroll = recordsToEnroll.map(function getStudentId(record){
                    return record.id;
            });
    
            return [ ...currentEnrollment, ...idsToEnroll ];
    }
    
    function remindUnpaid(recordIds) {
            var unpaidIds = recordIds.filter(function notYetPaid(studentId){
                    var record = getStudentFromId(studentId);
                    return !record.paid;
            });
    
            printRecords(unpaidIds);
    }


​    

    // ********************************
    
    var currentEnrollment = [ 410, 105, 664, 375 ];
    
    var studentRecords = [
            { id: 313, name: "Frank", paid: true, },
            { id: 410, name: "Suzy", paid: true, },
            { id: 709, name: "Brian", paid: false, },
            { id: 105, name: "Henry", paid: false, },
            { id: 502, name: "Mary", paid: true, },
            { id: 664, name: "Bob", paid: false, },
            { id: 250, name: "Peter", paid: true, },
            { id: 375, name: "Sarah", paid: true, },
            { id: 867, name: "Greg", paid: false, },
    ];
    
    printRecords(currentEnrollment);
    console.log("----");
    currentEnrollment = paidStudentsToEnroll();
    printRecords(currentEnrollment);
    console.log("----");
    remindUnpaid(currentEnrollment);


- Arrow functions version


    var getStudentFromId = studentId => studentRecords.find(record => record.id == studentId);
    
    var printRecords = recordIds =>
            recordIds.map(getStudentFromId)
                    .sort(
                            (record1,record2) => record1.name < record2.name ? -1 : record1.name > record2.name ? 1 : 0
                    )
                    .forEach(record =>
                            console.log(`${record.name} (${record.id}): ${record.paid ? "Paid" : "Not Paid"}`)
                    );
    
    var paidStudentsToEnroll = () =>
            [ ...currentEnrollment,
                    ...(
                            studentRecords.filter(record => (record.paid && !currentEnrollment.includes(record.id)))
                            .map(record => record.id)
                    )
            ];
    
    var remindUnpaid = recordIds =>
            printRecords(
                    recordIds.filter(studentId => !getStudentFromId(studentId).paid)
            );


​    

    // ********************************
    
    var currentEnrollment = [ 410, 105, 664, 375 ];


# Advanced Scope

Lexical scope: refer scopes nested within each other and idea of compiler is figuring out ahead of time before being executed that’s what we mean 
by the concept of lexical scope.

Lex shares the same root as stages, that stage of parsing the lexor. Its decided by compile not runtime.

**Lexical scope**

Sublime levels plugin - is levels (  analyse scope levels ) 


    var teacher = "Kyle";
    
    function otherClass() {
      var teacher = "Suzy";
    
      function ask ( question ){
        console.log(teacher, question);
      }
      ask("why"):
    }

except for function declaration: (bug)
var x = function(foo){ var y = foo; }

**Dynamic scope**


    var teacher = "Kyle";
    
    function ask ( question ){
        console.log(teacher, question);
      }
    
    function otherClass() {
      var teacher = "Suzy";
      ask("why"):
    }
    otherClass();

in ask function thinking in lexicaly scope way the var teacher should reach for line one via scope nesting. 

In dynamic language it wouldn’t even watch for lexical scope teacher, but  it would search where is ask called from. And it is called from otherClass() and it would assign that variable on line 8.

So in dynamical scope we are getting scope that is detement based on the conditions at runtime, where lexical is on author time. Even if JavaScript does not have dynamic scope. JavaScript does have mechanism that gives us that same kind of flexibility.

Fixed and predictable, and dynamic and flexible. 



https://dev.to/lydiahallie/javascript-visualized-scope-chain-13pd


**Function Scopeing**

