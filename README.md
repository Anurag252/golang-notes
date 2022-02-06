# golang-notes

 1. package-level isn't effected from the change inside the nested func
 2. imported names have file scope 
 3. func names have package scope
 4. we can import with different names :- 
 `package main

import "fmt"
import f "fmt"

func main() {
	fmt.Println("Hello!")
	f.Println("There!")
}`

5. we can import many times using different import names
6. This is because, for Go, it doesn't matter whether you use semicolons between the statements or not.
7. runtime.Version() and others in runtime
8. go doc -src runtime NumCPU prints documentation
9.fmt.Println(42, 8500, 344433, -2323) --> prints numbers
10. fmt.Println(0x10) -->  1 * 6 = 6 ,  16 * 9 = 144 = 150
11. var speed int // declaration . _ and unicode is allowed in declarations 
12. derclaration then use it
13. fmt.Printf("%q\n", brand) to print empty literal 
14. all types :- 
  Bool:          {Bool, IsBoolean, "bool"},
	Int:           {Int, IsInteger, "int"},
	Int8:          {Int8, IsInteger, "int8"},
	Int16:         {Int16, IsInteger, "int16"},
	Int32:         {Int32, IsInteger, "int32"},
	Int64:         {Int64, IsInteger, "int64"},
	Uint:          {Uint, IsInteger | IsUnsigned, "uint"},
	Uint8:         {Uint8, IsInteger | IsUnsigned, "uint8"},
	Uint16:        {Uint16, IsInteger | IsUnsigned, "uint16"},
	Uint32:        {Uint32, IsInteger | IsUnsigned, "uint32"},
	Uint64:        {Uint64, IsInteger | IsUnsigned, "uint64"},
	Uintptr:       {Uintptr, IsInteger | IsUnsigned, "uintptr"},
	Float32:       {Float32, IsFloat, "float32"},
	Float64:       {Float64, IsFloat, "float64"},
	Complex64:     {Complex64, IsComplex, "complex64"},
	Complex128:    {Complex128, IsComplex, "complex128"},
	String:        {String, IsString, "string"},
	UnsafePointer: {UnsafePointer, 0, "Pointer"},

	UntypedBool:    {UntypedBool, IsBoolean | IsUntyped, "untyped bool"},
	UntypedInt:     {UntypedInt, IsInteger | IsUntyped, "untyped int"},
	UntypedRune:    {UntypedRune, IsInteger | IsUntyped, "untyped rune"},
	UntypedFloat:   {UntypedFloat, IsFloat | IsUntyped, "untyped float"},
	UntypedComplex: {UntypedComplex, IsComplex | IsUntyped, "untyped complex"},
	UntypedString:  {UntypedString, IsString | IsUntyped, "untyped string"},
	UntypedNil:     {UntypedNil, IsUntyped, "untyped nil"},
  
  15. use _ if unused
  16. other ways to declare :-
  var (
	     speed int
	     velocity int
	   )
     
     var speed, velocity int
     
  17. MyAge, myAge, and MYAGE are different variables
  18. byte and rune are also numeric types
  19. var firstName, lastName string = "", "" //another way to decalare and assign
  20. we can have unused variables at package level
  21 . ops, ok, fail := 2350, 543, 433
  22.fmt.Printf(
		"total: %d - success: %d / %d\n",
		ops, ok, fail,
	)
  
  20. remiander operator can be used with only integers
  21 . fmt.Println(8 * -4.0) // returns float
  22. convert to float float64(myAge+yourAge) or others
  23. string literal s = `how are you?`
  24. strconv.FormatBool and strconv for library 
  25. len(str)
  26. utf8.RuneCountInString() count rune
  27. // byte is an integer number with 8 bits (1 byte)
	var b byte

	// all bits are empty or 0
	// this is the minimum number a byte can represent
	b = 0
	fmt.Printf("%08b = %d\n", b, b)

	// all bits are full or 1
	// this is the maximum number a byte can represent
	b = 255
	fmt.Printf("%08b = %d\n", b, b)
  28. math.MinInt8 , math.MinInt16 .. so on for maxvalue
  29. floats goes to infinity when overflowed
  30. small := uint8(300) // returns 255
  31. type (
		gram  float64 // float64 is the underlying type of gram
		ounce float64 // float64 is the underlying type of ounce
	)
  gram vs ounce is not interconvertible
  
  32 :- // Copyright © 2018 Inanc Gumus
// Learn Go Programming Course
// License: https://creativecommons.org/licenses/by-nc-sa/4.0/
//
// For more tutorials  : https://learngoprogramming.com
// In-person training  : https://www.linkedin.com/in/inancgumus/
// Follow me on twitter: https://twitter.com/inancgumus

package main

import (
	"fmt"

	"github.com/inancgumus/learngo/09-go-type-system/05-defined-types/03-underlying-types/weights"
)

type (
	// Gram underlying type is int
	Gram int

	// Kilogram underlying type is int
	Kilogram Gram

	// Ton underlying type is int
	Ton Kilogram
)

func main() {
	var (
		salt   Gram     = 100
		apples Kilogram = 5
		truck  Ton      = 10
	)

	// types with different names cannot be used together
	// salt = apples
	// apples = truck

	// since their underlying type is int
	// they can be converted to any type
	//   with an underlying type of int
	salt = Gram(apples)
	apples = Kilogram(truck)
	truck = Ton(Kilogram(Gram(int(apples))))

	fmt.Printf("salt: %d, apples: %d, truck: %d\n",
		salt, apples, truck)

	// -----------------------------------------------------
	// TYPES FROM DIFFERENT PACKAGES
	// -----------------------------------------------------

	// Gram and weights.Gram are different types

	// You cannot do this
	// salt = weights.Gram(100)

	// But, you can convert it back to Gram
	// Since, their underlying type is int
	salt = Gram(weights.Gram(100))

	fmt.Printf("Type of weights.Gram: %T\n", weights.Gram(1))
	fmt.Printf("Type of main.Gram   : %T\n", Gram(1))

	// You can declare a new type
	// from a type of an external package
	type myGram weights.Gram

	var pepper myGram = 20
	pepper = myGram(salt)

	fmt.Printf("Type of pepper      : %T\n", pepper)
}

33:- aliased types are the same types just with different names for readability and refactoring
34. // this declares an array with two byte elements
		// its length      : 2
		// its element type: byte
		ages [2]byte
35 . go compiler will catch error of index out of bounds in case a constant is used
36.. 
   
