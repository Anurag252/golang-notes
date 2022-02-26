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
35 . go compiler will catch error of index out of bounds in case a constant is used , but not if a variable is used
36. strconv.ParseInt(os.Args[1], 10, 8)
37. books := [4]string{
			"Kafka's Revenge",
			"Stay Golden",
			"Everythingship",
			"Kafka's Revenge 2nd Edition",
		} 
38. books := [...]string{
			"Kafka's Revenge",
			"Stay Golden",
			"Everythingship",
			"Kafka's Revenge 2nd Edition",
		}
39. const (
	winter = 1
	summer = 3
	yearly = winter + summer
)
40. fmt.Printf(books) // prints array
41. copy array from index 1 till end --> args := os.Args[1:]
42. blue == red // length , order, type , all elements
43. blue := [3]int{6, 9, 3}
	red := blue

	blue[0] = 10
	
44. for i, b := range prev {
		books[i] += b + " 2nd Ed."
	}
45. students := [...][3]float64{
		{5, 6, 1},
		{9, 8, 4},
	}

	var sum float64

	for _, grades := range students {
		for _, grade := range grades {
			sum += grade
		}
	}
multi dim array

46. another way for multi dim array :- 
		
		students := [2][3]float64{
	 	[3]float64{5, 6, 1},
	 	[3]float64{9, 8, 4},
	 }
	
 47. rates := [3]float64{
		0: 0.5, // index: 0
		1: 2.5, // index: 1
		2: 1.5, // index: 2
	}
	index array to element  --> valid declartion of array . Also elements caan be in any order , also a mixture of keyed and unkeyed elements also allowed
	
 48. slice declaration :- var nums []int , still nil unlike array which has value here
 49. difference between slice and array :- zero values are 0 and nil , len works for both of them , no pre defined length in case of slice
 50. for and if syntax  
 for i, game := range games {
		if game != newGames[i] {
			ok = "not "
			break
		}
		
		
51. for found := 0; found < max; {
52. array to slice nums[:] (from nums array to slices )
53. use append to add to slice , returns updated slice
54. append two slices append(nums, tens...)
55. print slices [start : length] 
56. 
57. []int(nil) convert nil to nil slice
58.  go is pass by copy
 only the slice header is copied: 3 integer fields (24 bytes)
 think of passing an array with millions of elements instead.
59. unsafe.Sizeof gives size of array or slices . slice size is fixed , only header , array size includes all elements
60. nil slice - []num , empty slice - []nums{}
61. nums = append(nums, nums[2:]...) nums + nums from 2nd index 
62. sliceable[0:3:3] --> a[low : high : max]
constructs a slice of the same type, and with the same length and elements as the simple slice expression a[low : high].
Additionally, it controls the resulting slice's capacity by setting it to max - low.

63. make([]int, 3) // 
64.upTasks = upTasks[:cap(upTasks)]
65. copy(dst, source) --> int numbers min(len(src), len(dst)) 
66. // #5: returns the # of copied elements
	// n := copy(data, []float64{10, 5, 15, 0, 20})
	// fmt.Printf("%d probabilities copied.\n", n)

	// #6: (sometimes) use append instead of copy
	// data = append(data[:0], []float64{10, 5, 15, 0, 20}...)
	
	saved := append([]float64(nil), data...)
	
67. append to multi dimesnion slice spendings := make([][]int, 0, 5)

	spendings = append(spendings, []int{200, 100})
68. stringd.split , fields 
69. maps  var dict map[string]string
70.  Cannot use non-comparable types as map key types , cant compare a slice except to a nil value 
71. var broken map[[]int]int // cant use this as key
72. initiate a dictionary dict := map[string]string{
		"good":    "kötü",
		"great":   "harika",
		"perfect": "mükemmel",
		// #4
		// 42: "forty two",
		// "forty two": 42,
	}
73. comma ok ;- if value, ok := dict[query]; ok {
		fmt.Printf("%q means %#v\n", query, value)
		return
	}
74. printing map gives ordered output 
75. we can compare maps as so :- map1 == map2
76. delete(dict, "notexisting") delete a key (exisitng / non exisiting)
77. in := bufio.NewScanner(os.Stdin) reads from  std input , in.Scan() , in.Text()
78. initialize a struct -- person1 := Person{Name: "Pablo", Lastname: "Picasso", Age: 91}
79. var (
		name, lastname string
		age            int

		name2, lastname2 string
		age2             int
	)

	name, lastname, age = "Pablo", "Picasso", 95
	name2, lastname2, age = "Sigmund", "Freud", 8
80. structs can be copied and compared as well . song1 = song2 , if song1 == song2 { --> compares all properties 
81.  you can't compare struct values that contains incomparable fields, you need to compare them manually
82.  song := rock.songs[0]
	song.title = "live forever"
here rock struct is not changed
83. Embedding :- embedding a struct inside another 
84. marshalling :- 
type user struct { // #1
	Name        string      `json:"username"`
	Password    string      `json:"-"` // not serialized
	Permissions permissions `json:"perms,omitempty"` // #6

	// name        string // #1
	// password    string // #1
	// permissions // #3
}
85. string int structs arrays etc are copy by value . maps slices functions are copy by reference
86. function always makes a copy of passed arguements
87. P := &counter
	V := **P 
88. from array to slices , use ...
89. func avg(nums ...int) int {
	return sum(nums) / len(nums)
}
90. strings.Map(unpunct , "" ) --> map takes a function and transforms the string
91. make() to create a data structure
92. defer function --> called at the end 
93. func main() {
	fmt.Printf("HasPrefix: %T\n", strings.HasPrefix)
	fmt.Printf("HasSuffix: %T\n", strings.HasSuffix)
	fmt.Println()

	var fn func(string, string) bool

	fn = strings.HasPrefix
	fn = strings.HasSuffix

	ok := fn("gopher", "go")

	fmt.Printf("ok       : %t\n", ok)
}
94. func spread(samples int, P int) (estimated float64) {
	counts := make(chan float64)

	for i := 0; i < P; i++ {
		go func() { counts <- estimate(samples / P) }()
	}

	for i := 0; i < P; i++ {
		estimated += <-counts
	}
	return estimated / float64(P)
}
95. package main

// file scope
import "fmt"

// package scope
const ok = true

// package scope
func main() { // block scope starts

96. we can have same variable in nested scope 
97. // Go supports Unicode characters in string literals
	// And also in source-code: KÖSTEBEK!
98. mobydick := book{
		title: "moby dick",
		price: 10,
	} initiaize interface
99.switch v := v.(type) {
	case int:
		// book{title: "moby dick", price: 10, published: 118281600},
		t = v
	case string:
		// book{title: "odyssey", price: 15, published: "733622400"},
		t, _ = strconv.Atoi(v)
	default:
		// book{title: "hobbit", price: 25},
		return "unknown"
	}
100. type book struct {
	// embed the product type into the book type.
	// all the fields and methods of the product will be
	// available in this book type.
	product
	published interface{}
}  --> a function inside product will execute on book type as if it was inside book itself

101. Stringers
One of the most ubiquitous interfaces is Stringer defined by the fmt package.

type Stringer interface {
    String() string
}
A Stringer is a type that can describe itself as a string. The fmt package (and many others) look for this interface to print values.

111.sort.Sort() can sort any type that implements the sort.Interface

- sort.Interface has three methods: Len(), Less(), Swap()
  - Len() returns the length of a collection.
  - Less(i, j) should return true when an element comes before another one.
  - Swap(i, j)s the elements when Less() returns true.

- sort.Reverse() can reverse sort a type that satisfies the sort.Interface.

112. You can customize the sorting:
  - Either by implementing the sort.Interface methods,
  - or by anonymously embedding a type that already satisfies the sort.Interface
  - and adding a Less() method.

113.  json.Marshal() and json.MarshalIndent() can only encode primitive types.
  - Custom types can tell the encoder how to encode.
  - To do that satisfy the json.Marshaler interface.

- json.Unmarshal() can only decode primitive types.
  - Custom types can tell the decoder how to decode.
  - To do that satisfy the json.Unmarshaler interface.

- strconv.AppendInt() can append an int value to a []byte.
  - There are several other functions in the strconv package for other primitive types as well.
  - Do not make unnecessary string <-> []byte conversions.

- log.Fatal() can print the given error message and terminate the program.
  - Use it only from the main(). Do not use it in other functions.
  - main() is should be the main driver of a program.

114. 


	
   
