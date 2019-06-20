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



