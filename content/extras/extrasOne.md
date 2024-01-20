+++
title = 'extrasOne'
date = 2024-01-14T18:56:27+05:30
draft = false
+++

### Lorem ipsum dolor

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus tempor in lacus Lorem ipsum, dolor sit amet consectetur adipisicing elit. Ipsa modi, est ullam repellat quis temporibus distinctio minima consectetur incidunt beatae itaque? Asperiores saepe dicta, sint incidunt exercitationem debitis itaque quos? Lorem ipsum dolor sit, amet consectetur adipisicing elit. Mollitia, aut quis. Fuga dolor omnis illum debitis dolorem eaque, quod iusto, nesciunt error assumenda ab dolorum? Repudiandae provident quibusdam sapiente necessitatibus


```go
package main

import "fmt"

// calculateSquares calculates the sum of the squares of the digits of the given number
// and sends the result to the squareop channel.
func calculateSquares(number int, squareop chan int) {
	sum := 0
	for number != 0 {
		digit := number % 10
		sum += digit * digit
		number /= 10
	}
	squareop <- sum
}

// calculateCubes calculates the sum of the cubes of the digits of the given number
// and sends the result to the cubeop channel.
func calculateCubes(number int, cubeop chan int) {
	sum := 0
	for number != 0 {
		digit := number % 10
		sum += digit * digit * digit
		number /= 10
	}
	cubeop <- sum
}

func main() {
	number := 589
	sqrch := make(chan int)
	cubech := make(chan int)

	// Start two goroutines to calculate the sum of squares and cubes of the digits.
	go calculateSquares(number, sqrch)
	go calculateCubes(number, cubech)

	// Receive the results from the channels and add them.
	squares, cubes := <-sqrch, <-cubech
	fmt.Println("Final result", squares+cubes)
}

```
