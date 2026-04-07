---
{"dg-publish":true,"permalink":"/knowledge/type-script/","tags":["typescript","javascript","webdevelopement"]}
---

---

## Advantages of TS

 - Static Typing => code is more predictable and easier to debug
 - OOP => easier to organize code
 - Compilation => errors are caught before runtime

## Common Datatypes

- **Number** - All numeric values are represented by the number type, there aren't separate definitions for integers, floats or others.
- **String** - The text type, just like in vanilla [[Knowledge/JavaScript\|JS]] strings can be surrounded by 'single quotes' or "double quotes".
- **Boolean** - `true` or `false`, using 0 and 1 will cause a compilation error.
- **Any** - A variable with this type can have it's value set to a string, number, or ***any***thing else.
- **Arrays** - Has two possible syntaxes: `my_arr: number[];` or `my_arr: Array<number>`.
- **Void** - Used on function that don't return anything.

[TypeScript: Handbook - Basic Types](https://www.typescriptlang.org/docs/handbook/basic-types.html)

## Interfaces

Interfaces make sure an Object matches a specific structure. The order of the values does not matter.

```ts
interface Food {
    name: string;
    calories: number;
}

function speak(food: Food): void{
  console.log("Our " + food.name + " has " + food.calories + " calories.");
}

var ice_cream = {
  name: "ice cream", 
  calories: 200
}

speak(ice_cream);
```

[TypeScript: Handbook - Interfaces](http://www.typescriptlang.org/docs/handbook/interfaces.html)

## Classes

```ts
class Menu {
  items: Array<string>;
  pages: number;

  constructor(item_list: Array<string>, total_pages: number) {
    this.items = item_list;    
    this.pages = total_pages;
  }

  list(): void {
    console.log("Our menu for today:");
    for(var i=0; i<this.items.length; i++) {
      console.log(this.items[i]);
    }
  }
} 


// Inheritance

class HappyMeal extends Menu {
  constructor(item_list: Array<string>, total_pages: number) {
    super(item_list, total_pages);
  }

  list(): void{
    console.log("Our special menu for children:");
    for(var i=0; i<this.items.length; i++) {
      console.log(this.items[i]);
    }
  }
```

>[!note]
>There are also native [[Knowledge/JavaScript\|js]] classes, but they do not support static typing, access modifiers and more.

[TypeScript: Handbook - Classes](http://www.typescriptlang.org/docs/handbook/classes.html)

## Generics

Using generics instead of `any` makes sure the type of the input is preserved. With `any`, everything is converted to `any`

```ts
function genericFunc<T>(argument: T): T[] {    
  var arrayOfT: T[] = [];
  arrayOfT.push(argument);
  return arrayOfT;
}

var arrayFromString = genericFunc<string>("beep");
console.log(arrayFromString[0]);         // "beep"
console.log(typeof arrayFromString[0])   // String

var arrayFromNumber = genericFunc(42);
console.log(arrayFromNumber[0]);         // 42
console.log(typeof arrayFromNumber[0])   // number
```




