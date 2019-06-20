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
        firstName: string
      }
      
      function greet(person:NamedPerson) {
        console.log("Hello," +person.firstName);
      }
      
      function changeName(person: NamedPerson) {
        person.firstName = "Anna";
      }
      
      const person = {
        name: "Max",
        age: 25
      };
      
      greet(person);
      changeName(person);
      greet(person);
  
  // TS throws an error because interface guaranteed that input is as described. If not, on compile time error thrown. This is good to manage and standardize function inputs from one center.
  
  > We should correct person objects name property to firstName to compile properly.
  
  
