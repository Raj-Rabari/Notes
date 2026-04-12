This is an essential question. The difference between **Overloading** and **Overriding** is one of the most common traps in C++ interviews and system design. Because they sound so similar, developers often mix up their rules.

Here is the absolute, definitive guide to what you can and cannot change in both scenarios.

---

### 1. Method Overloading (Same Class)

**Concept:** Creating multiple completely new functions that happen to share the same name. This is resolved at **Compile-Time** (Early Binding).

To overload a function, the compiler must be able to tell them apart just by looking at the arguments you pass in. This combination of the function's name and its parameters is called the **Function Signature**.

- **ALLOWED to change:**
  - **Number of parameters:** `void draw()` vs `void draw(int x, int y)`
  - **Type of parameters:** `void print(int data)` vs `void print(std::string data)`
  - **Order of parameters:** `void set(int x, float y)` vs `void set(float y, int x)`
- **NOT ALLOWED to change (on its own):**
  - **Return type:** You cannot have `int getValue()` and `float getValue()`. If you call `getValue()`, the compiler has no idea which one you want because the arguments are identical. It will throw an error.
- **The Senior Secret (`const` Overloading):**
  - You actually _can_ overload based entirely on the `const` qualifier at the end of the method!
  - `int& getData()` and `const int& getData() const` are considered two completely different functions. The compiler will automatically call the `const` version if the object itself is `const`. This is how `std::vector` safely handles `vector[0]`.

### 2. Method Overriding (Child Class replacing Parent)

**Concept:** Replacing a `virtual` function from a Base Class using the V-Table. This is resolved at **Run-Time** (Late Binding).

When you override, you are fulfilling a strict contract. The whole point of Polymorphism is that the caller doesn't know what the exact object is, so the inputs and outputs must perfectly match the Base Class promise.

- **NOT ALLOWED to change:**
  - **Number of parameters:** Must be exactly the same.
  - **Type of parameters:** Must be exactly the same.
  - **`const` qualifier:** If the base is `update() const`, the child must be `update() const`.
  - _(Note: If you change any of these, the compiler thinks you are trying to Overload, not Override. This is exactly why we use the `override` keyword—to force the compiler to throw an error if we accidentally change one of these rules)._
- **ALLOWED to change (The Exception):**
  - **Access Specifiers:** You can technically override a `public` base method and make it `private` in the child class (though this is usually terrible architecture).
- **The Senior Secret (Covariant Return Types):**
  - There is exactly ONE scenario where you are allowed to change the return type when overriding. If the Base class returns a pointer (or reference) to a Base class, the Child class is allowed to return a pointer (or reference) to a Child class.
  - **Example:**

    ```cpp
    class Entity {
    public:
        virtual Entity* clone() { return new Entity(); }
    };

    class Player : public Entity {
    public:
        // This is perfectly legal and brilliant!
        // We changed the return type from Entity* to Player*
        Player* clone() override { return new Player(); }
    };
    ```

    This is incredibly useful for the "Prototype Pattern" in game development, allowing you to duplicate objects while keeping their specific data types intact.

---

**Summary Checklist:**

- **Overloading (Same Class):** You MUST change the inputs. You CANNOT change only the output.
- **Overriding (Child Class):** You CANNOT change the inputs. You CAN change the output (but only if returning a more specific pointer/reference).
