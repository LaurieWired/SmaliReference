# Smali Reverse Engineering Reference
[![Follow @lauriewired](https://img.shields.io/twitter/follow/lauriewired?style=social)](https://twitter.com/lauriewired)

# Description
Quickly reference Smali instructions and parameters for your Android Reverse Engineering.

Android decompilation failures commonly occur, forcing Reverse Engineers to read the smali code of an application. The below reference contains commonly-used smali instruction. It also defines their functionality and the order of arguments to provide a quick guide. For a full list of smali instructions, you can also visit the [Android Dalvik Bytecode Reference](https://source.android.com/docs/core/runtime/dalvik-bytecode).

## Common Smali Instructions

### Initializing

- **const-string `<register>`, `<string>`**
  - **Description**: Puts a string constant into a register.
  - `<register>`: The register where the string reference will be stored.
  - `<string>`: The string value.

- **const\4 `<register>`, `<number>`**
  - **Description**: Puts a 4-bit number into a register
  - `<register>`: The register where the number be stored.
  - `<number>`: The number value, which has to be smaller than 16

- **const\16 `<register>`, `<number>`**
  - **Description**: Puts a 16-bit number into a register
  - `<register>`: The register where the number be stored.
  - `<number>`: The number value, which has to be smaller than 2^16
  
- **new-instance `<register>`, `<type>`**
  - **Description**: Creates a new instance of a class but doesn't call its constructor.
  - `<register>`: The register where the reference to the new object will be stored.
  - `<type>`: The type of object to instantiate (but not initialize).

- **move-object `<destination>`, `<source>`**
  - **Description**: Moves an object reference from one register to another.
  - `<destination>`: The register where the value will be moved to.
  - `<source>`: The register holding the value you want to move.


### Calling functions

- **invoke-virtual {`<registers>`}, `<method>`**
  - **Description**: Invokes a virtual method on an object.
  - `<registers>`: A list of registers holding the method's arguments, with the first one being the object on which the method is invoked.
  - `<method>`: The method to invoke.

- **invoke-direct {`<registers>`}, `<method>`**
  - **Description**: Invokes a constructor or private method on an object.
  - `<registers>`: A list of registers holding the method's arguments, with the first one being the object on which the method is invoked.
  - `<method>`: The constructor or private method to invoke.

- **invoke-static {`<registers>`}, `<method>`**
  - **Description**: Invokes a static method on an object.
  - `<registers>`: A list of registers holding the method's arguments. Because it is a static method, there is no special first argument for the object.
  - `<method>`: The static method to invoke.

- **return-void**
  - **Description**: Returns from a method that has a `void` return type.
  - No operands.

- **return-object `<register>`**
  - **Description**: Returns an object from a method.
  - `<register>`: The register holding the object to return from the method.

- **move-result `<destination>`**
  - **Description**: Moves the result of the previous method call into the given register. The method should return a simple type.
  - `<destination>`: The register where the value will be moved to.

- **move-result-object `<destination>`**
  - **Description**: Moves the result of the previous method call into the given register. The method should return an object type.
  - `<destination>`: The register where the value will be moved to.


### Working with properties
- **iput-object `<source>`, `<object>`, `<field>`**
  - **Description**: Stores an object from a register into an instance field of an object.
  - `<source>`: The register holding the value you want to store.
  - `<object>`: The register holding the object whose field you want to update.
  - `<field>`: The field you want to update.

- **iget-object `<destination>`, `<object>`, `<field>`**
  - **Description**: Retrieves an object from an instance field and stores it in a register.
  - `<destination>`: The register where the retrieved value will be stored.
  - `<object>`: The register holding the object from which you want to retrieve the field value.
  - `<field>`: The field you want to retrieve.

- **sput-object `<source>`, `<field>`**
  - **Description**: Stores an object from a register into a static field of a class.
  - `<source>`: The register holding the value you want to store.
  - `<field>`: The static field you want to update.

- **sget-object `<destination>`, `<field>`**
  - **Description**: Retrieves an object from a static field and stores it in a register.
  - `<destination>`: The register where the retrieved value will be stored.
  - `<field>`: The static field you want to retrieve.

### Application flow

- **if-lez `<register>`, `<label>`**
  - **Description**: Jumps to `<label>` if value stored in `<register>` is less than or equal to 0.
  - `<register>`: The register holding the value you want to compare to 0
  - `<label>`: The label to jump to if `<register>` <= 0. If `<register>` is larger than 0, the next instruction will be executed.

- **if-ge `<register>`, `<label>`**
  - **Description**: Jumps to `<label>` if value stored in `<register>` is greater than or equal to 0.
  - `<register>`: The register holding the value you want to compare to 0
  - `<label>`: The label to jump to if `<register>` is >= 0. If `<register>` < 0, the next instruction will be executed.

- **if-nez `<register>`, `<label>`**
  - **Description**: Jumps to `<label>` if value stored in `<register>` does not equal 0.
  - `<register>`: The register holding the value you want to compare to 0
  - `<label>`: The label to jump to if `<register>` != 0. If `<register>` = 0, the next instruction will be executed.

- **:`<labelname>`** (e.g. `:cond_0`)
  - **Description**: Defines a label to be used as a jump location
  - `<labelname>`: The name of the label.