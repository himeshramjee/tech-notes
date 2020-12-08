# Typescript Crash Course

## Hello Type Script

1. Javascript + a type system :)
1. Development/compile time type checking, inference and interface enforcement
1. "Type annotation" driven where developer specifies types and interfaces that are enforced by TypeScript
1. Only operates during development; at runtime involves not TypeScript, just vanilla transpiled JS
1. Unlike other compilers, TypeScript doesn't attempt to make any performance optimizations
1. Generate JS by compiling .ts with TypeScript Compiler
   - e.g. `tsc index.ts` is transpiled into `index.js`.
   - Does not execute the code, only compiles.

## Setup

1. `npm install -g typescript ts-node`
   - `typescript` is the core module that understands user defined annotations and enforces them
   - `ts-node` module helps developer efficiency by understanding NodeJS.
   - e.g. `tsnode index.ts` compiles and then executes the generated NodeJS code.

## Types

1. Declaration syntax

   1. Variables
      1. `const x as number;`
      1. `const today = new Date();`
      1. `const x: number;`
      1. `let x: null = null;`
      1. `const colors: string[] = ['red', 'green'];`
      1. `let point: { x: number; y: number } = { x: 10, y: 20};`
      1. `const logNumber:(i: number) => void = (i: number) => { console.log(i); }`
      1. `const x: number | boolean;`
   1. Functions
      ```
      cont add = (a: number, b: number): number => {
          return a + b;
      }
      ```
      1. Only return values can be inferred
   1. Arrays
      ```
      const carMakers = ['ford', 'toyota', 'chevy'];
      const dates = [new Date(), new Date()];
      const carsByMake: string[][] = [
        ['f150', 'corrolla', 'camaro']
      ];
      ```
   1. Tuples

      ```
      // Object
      const drink = {
        color: 'brown',
        carbonated: true,
        sugar: 40
      };

      // Plain array without annotation
      const pepsi ['brown', true, 40];

      // Add type info to create a tuple that helps
      // enforce position/order of elements and expected types
      const pepsi: [string, boolean, number] = ['brown', true, 40];

      // Alterate to this declaration style is to use type aliases
      type Drink = [string, boolean, number];
      const pepsi: Drink = ['brown', true, 40];
      ```

   1. Interfaces add a new type, describing the property names and value types of an object.

      ```
      const oldCivic = {
        name: 'civic',
        year: 2000,
        broken: true
        // Imagine 5 more properties or methods/functions here :)
      };

      const printVehicle = (vehicle: { name: string; year: number; broken: boolean }): void => {
        console.log(`Name: ${vehicle.name}`);
        console.log(`Year: ${vehicle.year}`);
        console.log(`Broken: ${vehicle.broken}`);
      }

      printVehicle(oldCivic);

      // Consolidates long type annotations into single Interfact that can be reused
      interface Vehicle {
        name: string;
        year: number;
        broken: boolean;
      }

      const printVehicle = (vehicle: Vehicle): void => {
        console.log(`Name: ${vehicle.name}`);
        console.log(`Year: ${vehicle.year}`);
        console.log(`Broken: ${vehicle.broken}`);
      }

      printVehicle(oldCivic);
      ```

   1. Classes are blueprints to create an object with some fields/properties and methods/functions that represent some thing.

   ```
   class Vehicle {

     constructer(public color: string): void {
       // 'public' in the parameter is a shorthand to
       // actually declaring a public class property
     }

     drive(): void {
       console.log("chugga chugga");
     }

     honk(): void {
       console.log("Beep");
     }
   }

   class Car extends Vehicle {
     constructor(public wheels: number, color: string) {
       // Adding the scope qualifier 'public' to color would
       // declare a new class property.
       super(color);
     }

     public drive(): void {
       console.log("vroom!");
     }
   }

   const vehicle = new Vehicle();
   vehicle.drive();
   vehicle.honk();

   const car = new Car(4, "red");
   car.drive();
   car.honk();
   ```

1. Primitive
   - void, undefined, symbol, null, string, number, boolean, Date, Object
1. Object
   - User created
   - functions, arrarys, classes, objects, any
1. Type Definition Files - `*.d.ts`
   - Help integrate JS Libraries into TypeScript projects by (even) retrofitting the type annotations to a JS Library.
   - Install like any other module: `npm install @types/faker`
