# Smali Reverse Engineering Reference
[![Follow @lauriewired](https://img.shields.io/twitter/follow/lauriewired?style=social)](https://twitter.com/lauriewired)

# Description
Quickly reference Smali instructions and parameters for your Android Reverse Engineering.

Android decompilation failures commonly occur, forcing Reverse Engineers to read the smali code of an application. The below reference contains commonly-used smali instruction. It also defines their functionality and the order of arguments to provide a quick guide. For a full list of smali instructions, you can also visit the [Android Dalvik Bytecode Reference](https://source.android.com/docs/core/runtime/dalvik-bytecode).

## Common Smali Instructions

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

- **invoke-virtual {`<registers>`}, `<method>`**
  - **Description**: Invokes a virtual method on an object.
  - `<registers>`: A list of registers holding the method's arguments, with the first one being the object on which the method is invoked.
  - `<method>`: The method to invoke.

- **invoke-direct {`<registers>`}, `<method>`**
  - **Description**: Invokes a constructor or private method on an object.
  - `<registers>`: A list of registers holding the method's arguments, with the first one being the object on which the method is invoked.
  - `<method>`: The constructor or private method to invoke.

- **const-string `<register>`, `<string>`**
  - **Description**: Puts a string constant into a register.
  - `<register>`: The register where the string reference will be stored.
  - `<string>`: The string value.

- **new-instance `<register>`, `<type>`**
  - **Description**: Creates a new instance of a class but doesn't call its constructor.
  - `<register>`: The register where the reference to the new object will be stored.
  - `<type>`: The type of object to instantiate (but not initialize).

- **sput-object `<source>`, `<field>`**
  - **Description**: Stores an object from a register into a static field of a class.
  - `<source>`: The register holding the value you want to store.
  - `<field>`: The static field you want to update.

- **sget-object `<destination>`, `<field>`**
  - **Description**: Retrieves an object from a static field and stores it in a register.
  - `<destination>`: The register where the retrieved value will be stored.
  - `<field>`: The static field you want to retrieve.

- **return-void**
  - **Description**: Returns from a method that has a `void` return type.
  - No operands.

- **return-object `<register>`**
  - **Description**: Returns an object from a method.
  - `<register>`: The register holding the object to return from the method.

- **move-object `<destination>`, `<source>`**
  - **Description**: Moves an object reference from one register to another.
  - `<destination>`: The register where the value will be moved to.
  - `<source>`: The register holding the value you want to move.
