**My Messy TypeScript Learning Notes**

  Here will be first notes which i wrote by handwriting before. I will add them sooner.
  
  **ES6 in TypeScript**
  
  **Namespaces**
  
  
  
  **Modules**
  
  *export default* -> if file imported with no referance but only path, all expoerted things imported
  functions, classes and properties can be export
  
  
  2 import types available
  
  - relative path, like: ``./path1/path2/filename``
  - absolute path, like: ``@path1/path2/filename`` // this points at node_modules folder by default


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


**Interfces**
Interface in TS is to standardize function inputs. 

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

    function genericFuncion<T>(data: T) {
        return data;
     }
Generic functions tells TypeScript data will send with its type automatically or manually. This makes easy development while using this function.

    genericFunction<number>("just a string"); // TS thows an error here. Because we declared data is number type.
    // we should use number with <number> declaration

as we use generics TS warn us while using properties of data we sent. ```genericFunction("`this is text").length``` will give us 12 as same if we use ``` genericFunction(23).length ``` we will get an error from TS compiler.

**Built-in Generics**

- Arrays ```const testResults: Array<number> = [12.4,45.6,23]``` we can't push string into that array

**Arrays**

    function printAll<T>(args: T[]) {
    args.forEach( (element)=> console.log(element))
    }
    
    printAll<string>(["Apple","Banana"]);
    
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
T is a kind of argument of generic class. All instantiations which typed like ``new SimpleMath<TYPE>`` TYPE may be number, string, boolean etc., which type sent to the class, will be applied where T letter used.


**Decorators**

Decorators are functions.
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
The ``@`` sign gives a reference to class contructor. 

This code prints on to the console like that:
    
    function Person() {
        console.log("Hi!");
    }
    
**Factory**

 A decorator function which returns another function as a decorator.
 
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
  Instead of this, we are using declaration type script files with extension of ``.d.ts`` . These files automatically included compilation process by typescript. They are not compiled, they just used for tellinf TS to handle js libraries. You can find ready to use ``.d.ts`` files on the internet. 
  TypeScripts read .d.ts files and learn how to use target js library.
  
  - Other alternative typings library
  
  - But more practical way is to install @types/jquery library with npm. And use jquery with any configuration needed.
  You can install other js libraries with same method. After installation just ``import "jQuery";`` in your ``.ts`` file. 
  
   

