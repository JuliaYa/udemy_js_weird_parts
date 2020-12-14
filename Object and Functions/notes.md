## Objects and the Dot

### Object

- Primitive "property"
- Object "property
- Function "method"

Object (core object) will have some sort of adress in computer's memory. And it will have references to these different properties and methods (they adresses in memory. Now they may be related to the adress of that base object concept, or thay may not.

 ```javascript
  var person = new Object();    // not the best way to create object

  // '[]' operator that find or create property
  person["firstname"] = "Tony";   
  person["lastname"] = "Alicea";

  var firstNameProperty = "firstname";

  console.log(person);
  console.log(person[firstNameProperty]);

  console.log(person.firstname);
  console.log(person.lastname);

  // '.' operator that find or create property
  person.address = new Object();
  person.address.street = "111 Main St."; 
  person.address.city = "New York";
  person.address.state = "NY";

  console.log(person.address.street);
  console.log(person.address.city);
  console.log(person["address"]["state"]);
 ```
 '.' operator preferable to use, because it's very clean and it's also easier to debug and find problems.
