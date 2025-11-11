<!---
{
  "id": "e7792ebe-224a-42c0-82ca-b1150127082c",
  "teaches": "Evaluating Complex Expressions with the Shell",
  "depends_on": ["862f9d0d-6ee1-4746-9988-e7cd0efc1c56"],
  "author": "Stephan Bökelmann",
  "first_used": "2025-04-01",
  "keywords": ["shell", "evaluation", "identifiers", "functions"]
}
--->

# Evaluating Complex Expressions with the Shell

## 1) Introduction

In the [Basic Evaluation Challenge](https://github.com/STEMgraph/ac584d6d-1397-49d9-8319-85e9fbd4b765), we learned how to evaluate simple expressions in the shell. This time, we aim to go further by introducing the concept of **identifiers** and showing how they can be used to construct **more complex expressions**.

An **identifier** is a name used to refer to a variable, function, type, or value. Identifiers can be **predefined** or **user-defined**. In the shell, using identifiers allows you to modularize and reuse code, following the software engineering principle of **divide and conquer**.

To evaluate expressions, the shell must interpret a combination of **operators and operands**, which can be reduced to a value — this process is called **evaluation**. When operands are replaced with variables, these expressions often take the form of **functions**.

In this exercise, you will:

- Set and use identifiers in the shell environment
- Combine them to form more complex expressions
- Investigate the scope and lifetime of identifiers

Let’s get started by learning how to bind values to identifiers.

## 2) Tasks

1. **Binding and Evaluating Simple Expressions**

    - Open a terminal emulator.
    - Bind a value to the identifier `x`:

      ```bash
      x=1
      echo $x
      ```

    - Bind a second value to `y` and use `echo` to print it.
    - Evaluate an expression using:

      ```bash
      expr $x + $y
      ```

2. **Binding Functions to Identifiers**

    - Define a simple function:

      ```bash
      function say_hello() { echo "Hello"; }
      say_hello
      ```

    - View the function definition:

      ```bash
      declare -f say_hello
      ```

    - Define a multi-line function:

      ```bash
      function say_multiple_things() {
        echo "Hello"
        echo "I"
        echo "say"
        echo "multiple"
        echo "things"
      }
      ```

3. **Passing Arguments to Functions**

    - Define a parameterized function:

      ```bash
      function costs() {
        cost_of_one_apple=3
        echo $(($1 * $cost_of_one_apple))
      }
      ```

    - Test with:

      ```bash
      costs 1
      ```

    - Modify the function to take two arguments (quantity and price).
    - Call the function with existing variables:

      ```bash
      costs $x $y
      ```

4. **Storing the Result of Expressions**

    - Store evaluation results in variables:

      ```bash
      d=$(expr 1 + 1)
      echo $d

      e=$(expr $x + $y)
      echo $e
      ```

    - (Optional/fix) Define a function `sum` and use it:

      ```bash
      function sum() { echo $(($1 + $2)); }
      apple_price_tag=$(sum $x $y)
      echo $apple_price_tag
      ```

5. **Calling Functions from Other Functions**

    - Define and call functions:

      ```bash
      function my_hello_function() { echo "Hello $1"; }
      function call_other_func() { my_hello_function "from another function"; }
      call_other_func
      ```

    - Define a third function before the function it calls and observe the behavior:

      ```bash
      function call_other_func2() { my_hello_function2 "world"; }
      function my_hello_function2() { echo "Hello $1"; }
      call_other_func2
      ```

6. **Local Identifiers and Intermediate Results**

    - Define a function that uses local variables:

      ```bash
      function squares() {
        local square1=$(( $1 * $1 ))
        local square2=$(( $2 * $2 ))
        echo $(($square1 + $square2))
      }
      ```

    - Try accessing `square1` from outside the function — what happens?
    - Redefine the function without `local` and compare behavior.
    - Define:

      ```bash
      function sum_of_squares() { echo $(( $1*$1 + $2*$2 )); }
      function product_of_squares() { echo $(( $1*$1 * $2*$2 )); }
      function compare_squares() {
        sum=$(sum_of_squares $1 $2)
        prod=$(product_of_squares $1 $2)
        if [ $sum -gt $prod ]; then echo 1; else echo 0; fi
      }
      ```

## 3) Questions

- What is the output of `echo $x`, `expr $x + $y`, `costs 1`, `echo $square1`?
- What happens when calling functions defined before or after each other?
- Why does `local` affect variable visibility?
- Why are positional parameters like `$1`, `$2` useful in function definitions?

## 4) Advice

- Use `declare -f` to inspect your functions.
- Use `local` in functions to avoid polluting the global namespace.
- Remember that arguments in Bash are **positional** — always keep `$1`, `$2`, etc., in mind.
- Use `$(command)` to evaluate and capture the output of a command into a variable.
- Shell scripting follows many programming principles — use naming and structure to your advantage.
- If unsure, echo intermediate values to debug your scripts.

