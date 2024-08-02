---
 layout: post
 title: Key-value-array
---

### Basic Array Declaration and Access

This example shows how to declare an array and access its elements:

```sh
#!/bin/bash

# Declare an array
fruits=("apple" "banana" "cherry")

# Access elements
echo "First fruit: ${fruits[0]}"
echo "Second fruit: ${fruits[1]}"
echo "Third fruit: ${fruits[2]}"
```

### Loop Through an Array

This example iterates over the elements of an array:

```sh
#!/bin/bash

# Declare an array
fruits=("apple" "banana" "cherry")

# Loop through array elements
for fruit in "${fruits[@]}"
do
  echo "Fruit: $fruit"
done
```

### Adding Elements to an Array

This example shows how to add elements to an array:

```sh
#!/bin/bash

# Declare an array
fruits=("apple" "banana")

# Add elements
fruits+=("cherry")
fruits+=("date")

# Loop through array elements
for fruit in "${fruits[@]}"
do
  echo "Fruit: $fruit"
done
```

### Array Length

This example shows how to get the length of an array:

```sh
#!/bin/bash

# Declare an array
fruits=("apple" "banana" "cherry")

# Get array length
length=${#fruits[@]}

echo "Number of fruits: $length"
```

### Removing Elements from an Array

This example shows how to remove elements from an array:

```sh
#!/bin/bash

# Declare an array
fruits=("apple" "banana" "cherry")

# Remove the second element
unset fruits[1]

# Loop through array elements
for fruit in "${fruits[@]}"
do
  echo "Fruit: $fruit"
done
```

### Array Slicing

This example shows how to get a slice of an array:

```sh
#!/bin/bash

# Declare an array
fruits=("apple" "banana" "cherry" "date" "elderberry")

# Get a slice of the array (from index 1 to 3)
slice=("${fruits[@]:1:3}")

# Loop through the slice
for fruit in "${slice[@]}"
do
  echo "Fruit: $fruit"
done
```

### Associative Arrays (Requires Bash 4.0+)

This example shows how to use associative arrays (key-value pairs):

```sh
#!/bin/bash

# Declare an associative array
declare -A fruit_colors

# Add key-value pairs
fruit_colors[apple]="red"
fruit_colors[banana]="yellow"
fruit_colors[cherry]="red"

# Access elements
echo "Apple color: ${fruit_colors[apple]}"
echo "Banana color: ${fruit_colors[banana]}"
echo "Cherry color: ${fruit_colors[cherry]}"

# Loop through associative array
for fruit in "${!fruit_colors[@]}"
do
  echo "$fruit color: ${fruit_colors[$fruit]}"
done
```

### Practicing Array Exercises

Here are a few exercises to practice:

1. **Create an array of numbers from 1 to 10 and print each number:**
    ```sh
    numbers=({1..10})

    for number in "${numbers[@]}"
    do
      echo "Number: $number"
    done
    ```

2. **Create an array of filenames in the current directory and print each filename:**
    ```sh
    files=(*)

    for file in "${files[@]}"
    do
      echo "File: $file"
    done
    ```

3. **Create an array of your favorite colors and print the number of colors:**
    ```sh
    colors=("red" "blue" "green" "yellow")

    echo "Number of colors: ${#colors[@]}"
    ```

4. **Create an array of your favorite movies and remove one movie from the list:**
    ```sh
    movies=("Inception" "The Matrix" "Interstellar" "The Dark Knight")

    # Remove "Interstellar"
    unset movies[2]

    for movie in "${movies[@]}"
    do
      echo "Movie: $movie"
    done
    ```

5. **Create an associative array of country-capital pairs and print each pair:**
    ```sh
    declare -A country_capitals

    country_capitals[USA]="Washington D.C."
    country_capitals[France]="Paris"
    country_capitals[Japan]="Tokyo"

    for country in "${!country_capitals[@]}"
    do
      echo "The capital of $country is ${country_capitals[$country]}."
    done
    ```


