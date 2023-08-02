## Classes in Python

Classes are custom user-defined types (types, meaning object types such as strings, ints, dicts/objs, etc...) that are common in many programming languages. In Python, classes usually take an object/dict format, which allows them to store key-value pairs, which can represent either "properties" or "functions".

## Defining a class

In Python, there are two ways to define a class: using the keyword `class` or the function `type()`.

### Defining with keyword "class"

When using the `class` keyword, we can open the declaration as follows, followed by the `__init__` function. 

Functions in classes must always have the first argument be `self`, or discarded with `_`. This allows any function within a class to access properties that have been set, by calling `self.insertPropertyName`. Other functions within the class can also be called this way, as `self.insertFunctionName(args)`. Additionally, all functions within a class can require other arguments as per normal function declaration.

The `__init__` function is used as a constructor, and contains the code to execute upon an instance^ of the class being created. This can set any properties that you want to create or set when the class is created. Any other arguments for the `__init__` function will check for arguments parsed when creating an instance of the class.

```py
class mathClass:
    def __init__(self, number1, number2):
        self.number1 = number1
        self.number2 = number2
    
    def sum(self):
        return self.number1 + self.number2
    
    def changeNumbers(self, newNumber1, newNumber2):
        self.number1 = newNumber1
        self.number2 = newNumber2
    #...
```

### Defining with function "type"

The `type()` function is useful for quickly defining classes, as it can create a class in one line. When using the `type()`^ function, 3 arguments are parsed: the name of the custom type, the type of the container, and the container. The name is a string that can be anything, and the container type is often set to `(object, )`, which encompasses all object types. The actual container contains the data of the class, and is most commonly typed as key-value pairs. Also note that the `type()` function returns the constructor, instead of making it universal. Therefore, you have to set a variable to the return of the function, to use it as a constructor.

```py
mathClass = type('mathClass', (object, ), {
    'number1': 0,
    'number2': 0,
    '__init__': lambda self, number1, number2: [
        setattr(self, "number1", number1),
        setattr(self, "number2", number2),
        None
    ][-1],
    
    'sum': lambda self: self.number1 + self.number2,

    'changeNumbers': lambda self, newnumber1, newnumber2: [
        setattr(self, "number1", newnumber1),
        setattr(self, "number2", newnumber2),
    ]
    #...
})
```
Notes: Since the functions are done inside lists in lambdas, we cannot explicitly declare the value of a property of self using `obj.property = value`. Walrus operators also do not work for  this purpose, and as a result, we have to use the `setattr()` function, which accepts the object, property name, and value (`setattr(obj, property, value)`). Also, the value/function for every key in the dictionary of functions and properties must either be a function callback or lambda. Lambdas can be defined on the fly and in one line, whereas functions must be declared seperately and have their callback set. Additionally, the `__init__` function cannot return a value, which is why the last index of the array of functions is set to `None`, and the last item index `[-1]` is called, to ensure that the return of the lambda is `None`. Also, (though you do not need to know this,) when an instance of the class is created, and the instance is parsed through the `type()`^ function to test for what type the object is, the value returned will not be the name of the variable, but instead the name (first argument) parsed into the original `type()` function.

### Declaring & using classes

After defining a class using one of the above methods, an instance of the class can be created and assigned to a variable, using the same syntax as calling a function.
```py
mathInstance = mathClass(3, 4)
```
Note that any arguments parsed into the function must be handled in the `__init__` function of the class, after `self` (however, `self` does not need to be parsed into the constructor, as it is parsed automatically).

To retrieve a classes properties and to set them, we can call the property as we did inside the class declaration, except replace `self` with the name of the instance we created.
```py
mathInstance = mathClass(3, 4)

#Retrieve and print property "number1"
print(mathInstance.number1)

#Set property "number1" to 2
mathInstance.number1 = 2
#Alternatively (works inside expressions)
setattr(mathInstance, "number1", 2)
```

To use functions from a class, we can call them similar to properties, but instead as a function (with brackets and arguments). Note that `self` is once again parsed automatically, and the only arguments we need to include are the ones that follow after `self`.

```py
mathInstance = mathClass(3, 4)
mathInstance.changeNumbers(1, 2)
```

### References

instance^: a subset of a type. `text = "sometext"` in that example, the `text` variable is an instance of a string, essentially meaning that the object's type is a string. Therefore, "instance" can also sometimes be used interchangably with "type"

`type()`^: The type function has two uses: creating new types and detecting the type of an object.
