**My Messy TypeScript Learning Notes**

  Here will be first notes which i wrote by handwriting before. I will add them sooner.
  
**Some notes:**
  
  Javascript is Dynamically typed language. This means it has types, it is forgiving, great for web browser object model.
  Typescript is a superset of javascript. TS is rigid and promotes stability and maintainability. TS gets these advantages to javascript and extend javascript. Typescript checks errors on compiling time. But this is not break/stops the compilation. /ts file compiled and js file produced.
 
 
  
To install type script with using npm:
    
    // to install
    npm - install typescript
    // to initialize
    tcs --init 
    // to watch changes and compile 
    tsc -w
    
we can compile multiple `.ts` files into one `.js` file.
    
    tsc --outfile targetJSFile.js firstTSFile.ts secondTSFile.ts lastTSFile.ts

Also we can import other ts files into one main ts file, after that we only compile the main `.ts` file.

At the main ts file
    
    /// <reference path="firstTSFile.ts"> 
    /// <reference path="secondTSFile.ts">
    main ts file codes here
    
after that import process we can compile ``mainTSFile.ts``

    tsc mainTSFile.ts --outfile mainTSFile.js
 ---
 ---
 
 **Some headers form another course**
 - Understand basic types in TS
 - Function typing + annotations
 - Type definition files
 - Arrays in TS
 - Modules systems
 - Classes + Refresher on OOP
 - Projects
 ---
 
 **Types in TypeScript**
 - **Primitive Types**
   - number
   - boolean
   - void
   - undefined 
   - string
   - symbol
   - null
 - **ObjectTypes**
   - functions 
   - arrays
   - classes 
   - objects
  
**Type Annotations:** Developer tells TypeScript the type

**Type Inference:** TypeScript guesses the type
     
---
---
    

Sample types:

    let aracMarka : string    
    let userAge : number 
    let userPasif : boolean
    let dersAdlari: any[] // array that elements are in any type 
    let dersAdlari: string[] // array that elements are in string type 
    let dersPuan: number[] // array that elements are in number type 
    
**tuple types**

Tuples are list of vary types

    let address :[string, number]   // there are in order
    let myAddress: address = "Oreon street"; //no error
    let myAddress: address = 23; //no error
    
    


**enum types**

    enum Color {Gray, Red, Blue, Maroon}
    let myColor : Color = Color.Green // directly values used
    console.log(myColor) // returns 1
    
**Note:** If any default value given to enum ``enum Color {Gray, Red=101, Blue, Maroon}`` next item takes sequential value. This means 

     enum Color {Gray, Red=101, Blue, Maroon}
        let myColor : Color = Color.Blue 
        console.log(myColor) // returns 102

**void type**

Usually used on functions and means function doesn't return anything but can do some jobs.
    
    function sayHello():void {
        console.log('Hello!')
    }     

**object type**

    let userData: {name: string, age: number} = {name: "John", age: 23}

**type alias**

     type myTypes = {
                    data: number[],
                    output: (isValidName: boolean)=> number[]
                    } 
     
     let myObject: myTypes =  {
                               data: [3,8,2,12,9,67],
                               output: function(all:boolean):number[]{
                               return this.data;
                               }                               
                               }                        
 
**union types**

Using multiple types together as an option. Types separated with pipe (|).

    let myValue: number | string = "John"; // no error
    let myValue: number | string = 23; // no error
    
**never types**

If a function will never return anything an never exit by default (may exit by a thrown error), and not expected so.
    
    function neverReturns(): never {
        throw new Error('Error happens');
    }
**Nullable types**

First we should activate this ``strictNullChecks: true`` from  ``tsconfig.json``      
    this makes types only nullable if type is null. As same if type is not null (assigned as number for example) you can not assign null. If we use ``tuple`` or ``union`` so no error will be thrown.
    
    let myType: number = 23;
    myTpe = null; // error
    
    let thatType: number | null = 23 ;
    thatType = null; // no error
    
    

  
**ES6 in TypeScript**
  
**Namespaces**
Namespaces creates a space separated from global.
    
    namespace MyMaths{
                       export function(){
                                        } 
                        }

functions in namespaces should export, properties not. Every things in a namespace is special to it. Namespaces acting like objects.
We can use namespaces inside other namespaces, but inner ones need to be exported with ``export`` keyword!

While reaching namespaces properties etc. from outside we can use dot notation.

    nameSpaceName1.nameSpaceName2.property
  
If we want to use aliases for namespaces
 
 ``import allNameSpaces = nameSpaceName1.nameSpaceName2``  
  
**Modules**
  
  *export default* -> if file imported with no referance but only path, all exported things imported
  functions, classes and properties can be export
  
  
  2 import types available
  
  - relative path, like: ``./path1/path2/filename``
  - absolute path, like: ``@path1/path2/filename`` // this points at node_modules folder by default

Like ES6 do
    
    import {exportedName1,exportedName2,...exportedNameN } from "./source/source/fileName"
    // above in paths .ts extension not required!

**Namespaces vs. Modules**
**Namespace**
- Organize application with JS Objects
- Can be split up over multiple files
- No module loader required
- Dependencies get difficult to manage in bigger applications

**Modules**
- Organize Applications with real Modules
- Can be split up over multiple files
- Module loader required
- Explicit dependency declaration

**Classes**

There is no this keyword. Constructor is not necessarily.
    
    class Person{
                Public | Private | Protected name: string
                //OR
                constructor (name:string) {
                                           this.name= "John" 
                                            }
                }

    Public   : Reached from every where, full access
    Private  : Just reached from inside this object (class)
    Protected: Reached from this object and its childs. Childs inherits everything
    
- **static**: Used for both property and methods of the classes. This keyword serves properties and methods to usage from outside without creating instances.  
  
- **abstract**: This keyword used with methods and classes. If used with classes these classes can not create instances. But can be extended to create new classes.
If used with methods these methods can not include any property or submethods. Extended classes should have this method. I not error thrown.

- **readonly**: Used with properties. We use this, if we want to read a property from outside but not to overwritten. 

        public readonly name:string
    
**Singleton Class**

The class that only have one instance at the same time.

    class OnlyOne{
        private static instance:OnlyOne;
        provate constructor(public name: string){
                                                }
        static getInstance(){
            if(!OnlyOne.instance){
                                   OnlyOne.instance = new OnlyOne('thatOne'); 
                                    }
                                 return OnlyOne.instance   
                             }                                        
    }    
    
    let wrong = new OnlyOne("New the one"); // throws an error
    let right = OnlyOne.getInstance(); // no error

**Interfaces**
Interface in TS is to standardize function inputs. They defines a custom type, describes the data, and the behaviour of the object to interacts with others. Interfaces used in compile time. They can't show up in compiled js file.

Sample code:

      interface NamedPerson {
        firstName: string;
        age?:number; // this question mark means age is optional
        [anyPropertyName: string]: any; // if we dont know incoming property(parameter) name and we don't now type of the value of this property.
        greet2(lastName: string)
      }
      
      function greet(person:NamedPerson) {
        console.log("Hello," +person.firstName);
      }
      
      function changeName(person: NamedPerson) {
        person.firstName = "Anna";
      }
      
      const person: NamedPerson = {
        name: "Max",
        age: 25,
        greet2(lastName: string){
            console.log("Hi, I am "+ this.firstName +" "+ lastName);
        }
      };
      
      greet(person);
      changeName(person);
      greet(person);
      person.greet2("Doe");
  
  // TS throws an error because interface guaranteed that input is as described. If not, on compile time error thrown. This is good to manage and standardize function inputs from one center.
  
  > We should correct person objects name property to firstName to compile properly.
  
  If we send object literal directly to function like:
  
    greet({name:"Anna", age:34})
    
  TS behave more strictly on this.
  We can add methods into interfaces. An interface could/should has all properties and methods function needs and also incoming argument/object has.
  
If a class want to implement this interface:

    class Person implements NamedPerson {
        firstName: string;
        greet3( lastName: string){
            console.log("Hi, I am "+ this.firstName +" "+ lastName);
        }
    }


**IMPORTANT:** Interfaces itself doesn't get compiled. They are just used for compiling time checks for development . So you cant see interfaces in compiled js files. :)

---

**Generics**
T and U generic names are used by convention. T is just the type of the parameter. And it is a kind of variable.

    function genericFuncion<T>(data: T) {
        return data;
     }
Generic functions tells TypeScript data will send with its type automatically or manually. This makes easy development while using this function.

    genericFunction<number>("just a string"); // TS thows an error here. Because we declared data is number type.
    // we should use number with <number> declaration

as we use generics TS warn us while using properties of data we sent. ```genericFunction("`this is text").length``` will give us 12 as same if we use ``` genericFunction(23).length ``` we will get an error from TS compiler.

We can use custom types with as like ``genericFunction<ACustomType>(data:ACustomType)``

**Built-in Generics**

- Arrays ```const testResults: Array<number> = [12.4,45.6,23]``` we can't push string into that array

**Arrays**

    function printAll<T>(args: T[]) {
    args.forEach( (element)=> console.log(element))
    }
    
    printAll<string>(["Apple","Banana"]);
    
These two usages are identical:
    var array: number[] = [1,2,3];
    var array2: Array<number> = [1,2,3];    
    
**Generic Types**    

    const echo2: <T>(data: T) => T = betterEcho;
Here is a generic type of function ``<T>(data: T) => T`` is type.

**Generic Classes**

    class SimpleMath<T> {
        baseValue: T;
        multiplyValue: T;
        calculate():number {
            return +this.baseValue * +this.multiplyValue;
            }
    }
    
after this setup you can use class as usual with more explicit.

You can use Type of class with ``class SimpleMath<T extends number | string>``. By doing this  class can only be initiated with ``new SimpleMath<number>()`` or ``new SimpleMath<string>()`` . Without number and string type we've get an error (for example boolean).
  
We can describe a type with another character like ``U`` , so class will be 
      
      class SimpleMath<T extends number, U extends string, >() {
          name: U      
          baseValue: T;
          multiplyValue: T;
          calculate():number {
              return +this.baseValue * +this.multiplyValue;
              }
      }      

Usage is ``const simpleMath = new SimpleMath<string, number>();``

**What this T letter means**
T is a kind of argument of generic class. All instantiations which typed like ``new SimpleMath<TYPE>`` TYPE may be number, string, boolean. Date etc., which type sent to the class, will be applied where T letter used. You can use any letter or word combination. You can use multiple (usually developers use 1 or 2 but not limited) generic types.

**Samples**

    class KeyValuePair<TKey, TValue>{
        public key: TKey,
        public value: TValue
    }


> Sample with an explanation

    function totalHeight(x: { length: number}, y: {length: number}): number {
        let total: number = x.length + y.length;
        return total;
    }    
    
This function gets 2 parameters which each of them must be an object, which must have length property, which must be a number. And this function must return something, which must be a number.
    

**Decorators**

In tsconfig.json file ``"experimentalDecorators": true`` should set.
Decorators are functions with special signatures. Decorators can target classes, methods, properties and parameters.
If a decorator is going to be attached to a class, it will take only one argument.

    function logged(constructorFn: Function) {
        console.log(constructorFn);
    }
    
    @logged
    class Person {
        constructor() {
            console.log("Hi!")
        }
    
    }
The ``@`` sign gives a reference to class constructor. 
The ``constructorFn`` is the target, and it targets to the constructor of class which is ``Function`` above.
The class's constructor function is ``function Person() { console.log("Hi!"")}`` so ``@logged`` logs to the console this.
This code prints on to the console is:
    
    function Person() {
        console.log("Hi!");
    }

> Multiple decorators can be added to the targets (classes, properties, methods or parameters)  

    @ToDo
    @Validate
    @IsAlphaNumeric
    @RegEx
    class Person{
    //...
    }  
    
**Factory**

 A director function which returns another function as a decorator. 
 
    function logged(constructionFn: Function) {
        console.log(constructorFn)
        }
        
     @logged
     class Person {
        constructor() {
            console.log("Hi!")
        }
     }   
 
    // Factory
    function logging(value: boolean) {
        return value ? logged : null;  
    } 

    @logging(true)
    class Car{
        
    }

**Method Decorator**

 to edit or change a behavior of a method inside a class. These decorators works on method, not class.
 
**Property Decorator**
 
**Parameter Decorator**


**JS Libraries with TypeScript**

- Jquery 

    - in our ts file we can use ``declare var $: any;`` . This allows to use included jquery file inside html. But this is the bad way. Because typescript doesn't know anything about library.
  Instead of this, we are using declaration type script files with extension of ``.d.ts`` . These files automatically included compilation process by typescript. They are not compiled, they just used for telling TS to handle js libraries. You can find ready to use ``.d.ts`` files on the internet. 
  TypeScripts read .d.ts files and learn how to use target js library.
  
  - Other alternative typings library
  
  - But more practical way is to install @types/jquery library with npm. And use jquery with any configuration needed.
  You can install other js libraries with same method. After installation just ``import "jQuery";`` in your ``.ts`` file. 
  
   
**TypeScript WorkFlows**
 - Using tsc and tsconfig file
 - Gulp workflow
 - WebPack workflow
 - 

**Source Maps**
- tsconfig.json option ``"sourceMap : true"`` makes debug mode active in browser. Thus, we can debug ``.ts`` files directly from inside browser. Browser knows ehere the sourcemap file from at the bottom line of js file ``//sourceMappingURL=orijinalJSfile.js.map``
SourceMap file matches ts file to js file line to line via line number.
So there are 4 same named files with different extensions, 
    - ``fileName.ts`` TS file
    - ``fileName.d.ts`` Declaration files
    - ``fileName.js.map`` Source Maps file
    - ``fileName.js`` produced (compiled) js file


**system.js**
// system.js is old method for import-export things. We will cover this logic later. 
