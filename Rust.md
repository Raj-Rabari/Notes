=> variables are by default immutable in Rust. but you can mutate it using 'mut' keyword before variable name.
=> constants are different than immutable variables. first difference is that you can't use 'mut' on them. and the type must be annottated.

shadowing:

    you cannot mutate variable but you can shadow them by redeclaring it like below.
    let x = 5;
    let x = x + 2;
    let x = "abc";

    but you cannot do.

    let mut x = "abc";
    x = x.len(); // because you're changing type here. shadowing allows you to change the type like above.

dataTypes:

    Rust can infer the type from the value but when there can be multiple types possible, you must need to give type anottation otherwise you will get error.

    like let s = '42';
    let n = '42'.parse().expect("not a number"); // now parse() function can return u32 or u64 or anything else. so we must need to specify type like below.

    let n: u32 = ...

scalar types:

    scalar types represent a single value. rust has four scalar types: integers, floating point numbers, booleans and characters.

Integer type:

    Length	Signed	Unsigned
    8-bit	i8	    u8
    16-bit	i16	    u16
    32-bit	i32	    u32
    64-bit	i64	    u64
    128-bit	i128	u128
    Architecture-dependent	isize	usize

Floating point numbers:

    two types: f32 & f64(bydefault).

    let x = 2.0; // f64
    let x: f32 = 2.0 // f32

boolean

    true or false with size of one byte

char

    use single quote, 4 byte in size. can represent unicode scalar value which means it's lot more than ASCII values.

Compound Types:

    tuple: tuple is general way of grouping number of values of different types. It has fixed length, cannot change after declaration.

    Array: same type, fixed length. stored on stack like other primitive types. vector type provided by std library is like array but can grow or shrink as it's stored on heap.

        let arr: [i32;5] = [1,3,34,5,6];

        let arr2 = [3;5];

functions:

    fn another_function(value: i32, char1: char) {
        // statements or expressions
    }

what is difference beteween statements and expression.

    statements: statements are instruction that perform some actions and doesnot written any value.
    expressions: expression evaluates to a resultant value.

    expressions are that which you can assign it to some variable.

    like let a = 2; is statement because you cannot assign it to b like b = (let a = 2);

    expression can be part of statement like 2 in above statement is expression.

    let y = {
        let x = 3;
        x+1
    }

    here the block with curly braces is an expression as it gets evaluated and returns the x+1 value. note there isn't semicolon after the x+1, if you put semicolon it will become statement and doesn't return anything.

References:

    References are same as it in c++. you can have multiple immutable references at a time in one scope or one single mutable reference.  when reference variable goes out of scope. any code to free the memory it contains will not run because it's just a reference , not owns memory.

    when we pass normal variables, it transfers the ownership to that function and we need to return them to return the ownership back to the function. but when passing the reference , reference don't own the memory so the function will just borrow a reference so we don't need to return it.

The slice reference:

    slice type lets you reference the continues sequence of elements in collection.
