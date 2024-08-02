---
 layout: post
 title: Case in Shell Scripting
--- 


### Basic `case` Statement

This example checks the value of a variable and prints a message accordingly:

```sh
#!/bin/bash

fruit="apple"

case $fruit in
  apple)
    echo "This is an apple."
    ;;
  banana)
    echo "This is a banana."
    ;;
  cherry)
    echo "This is a cherry."
    ;;
  *)
    echo "Unknown fruit."
    ;;
esac
```

### `case` Statement with Multiple Patterns

This example matches multiple patterns for the same action:

```sh
#!/bin/bash

day="Sunday"

case $day in
  Monday|Tuesday|Wednesday|Thursday|Friday)
    echo "It's a weekday."
    ;;
  Saturday|Sunday)
    echo "It's the weekend."
    ;;
  *)
    echo "Unknown day."
    ;;
esac
```

### Handling User Input

This example uses `case` to handle user input:

```sh
#!/bin/bash

echo "Enter a number between 1 and 3:"
read number

case $number in
  1)
    echo "You entered one."
    ;;
  2)
    echo "You entered two."
    ;;
  3)
    echo "You entered three."
    ;;
  *)
    echo "Invalid number."
    ;;
esac
```

### File Type Check

This example uses `case` to check the type of a file:

```sh
#!/bin/bash

file="example.txt"

case $file in
  *.txt)
    echo "This is a text file."
    ;;
  *.jpg|*.png)
    echo "This is an image file."
    ;;
  *.sh)
    echo "This is a shell script."
    ;;
  *)
    echo "Unknown file type."
    ;;
esac
```

### Case-Insensitive Matching

This example shows how to handle case-insensitive matching:

```sh
#!/bin/bash

read -p "Enter a letter: " letter

case ${letter,,} in
  a)
    echo "You entered A."
    ;;
  b)
    echo "You entered B."
    ;;
  c)
    echo "You entered C."
    ;;
  *)
    echo "Unknown letter."
    ;;
esac
```

### Practicing `case` Statement Exercises

Here are a few exercises to practice:

1. **Menu Selection:**
    ```sh
    echo "Select an option:"
    echo "1. Start"
    echo "2. Stop"
    echo "3. Restart"
    echo "4. Status"
    read option

    case $option in
      1)
        echo "Starting the service..."
        ;;
      2)
        echo "Stopping the service..."
        ;;
      3)
        echo "Restarting the service..."
        ;;
      4)
        echo "Checking the status of the service..."
        ;;
      *)
        echo "Invalid option."
        ;;
    esac
    ```

2. **Check if a number is positive, negative, or zero:**
    ```sh
    read -p "Enter a number: " num

    case $num in
      ''|*[!0-9]*)
        echo "Invalid input. Please enter a number."
        ;;
      *)
        case $num in
          0)
            echo "The number is zero."
            ;;
          -*)
            echo "The number is negative."
            ;;
          *)
            echo "The number is positive."
            ;;
        esac
        ;;
    esac
    ```

3. **File Permissions:**
    ```sh
    read -p "Enter a filename: " file

    case $file in
      ?*)
        if [ -e "$file" ]; then
          case $file in
            [dD]*) echo "This is a directory." ;;
            [fF]*) echo "This is a file." ;;
            *) echo "Unknown file type." ;;
          esac
        else
          echo "File does not exist."
        fi
        ;;
      *) echo "Invalid input." ;;
    esac
    ```

4. **Convert a string to uppercase or lowercase:**
    ```sh
    read -p "Enter a string: " str
    echo "Select an option:"
    echo "1. Convert to uppercase"
    echo "2. Convert to lowercase"
    read option

    case $option in
      1)
        echo "${str^^}"
        ;;
      2)
        echo "${str,,}"
        ;;
      *)
        echo "Invalid option."
        ;;
    esac
    ```

5. **Basic Calculator:**
    ```sh
    read -p "Enter first number: " num1
    read -p "Enter second number: " num2
    echo "Select an operation:"
    echo "1. Add"
    echo "2. Subtract"
    echo "3. Multiply"
    echo "4. Divide"
    read operation

    case $operation in
      1)
        echo "Result: $((num1 + num2))"
        ;;
      2)
        echo "Result: $((num1 - num2))"
        ;;
      3)
        echo "Result: $((num1 * num2))"
        ;;
      4)
        if [ $num2 -ne 0 ]; then
          echo "Result: $((num1 / num2))"
        else
          echo "Cannot divide by zero."
        fi
        ;;
      *)
        echo "Invalid operation."
        ;;
    esac
    ```

