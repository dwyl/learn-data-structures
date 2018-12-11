# learn-data-structures
Learn about data structures and algorithms, and the effects they can have on code performance

## *Why*?

Data structures and algorithms play a massive role in any and every programming
language. With a better understanding of both you can pick the ones that best
suit your needs and massively speed up your applications.

**Better hardware is not a solution**

Better hardware can only do so much. No matter how powerful your hardware is,
it is not going to make up for an inefficient algorithm.

The right choices in data structure and algorithm could be the difference
between something being processed in seconds or hours.

## *What*?

### Data Structures

> Data is a broad term that refers to all types of information down to the most
basic numbers and strings.

[Data structures](https://en.wikipedia.org/wiki/Data_structure), refer to how
data is organised.

```elixir
hello = "hello" # data
world = "world" # data

[hello, world] # data structure
```

### Algorithms

Simply put, an [algorithm](https://en.wikipedia.org/wiki/Algorithm) is a set of
steps for solving a problem. You would used an algorithm for making a sandwich
for example:

```
1 - Grab 2 slices of bread
2 - Butter each slice
3 - Put filling on top of one of the slices
4 - Put other slice on top of filling 🥪
```

In computing an algorithm is the same thing. Just a set of steps for a computer
program to accomplish a task.

There are often a number of ways your could accomplish a task so learning to
pick the right algorithm is a key.

## *How*?

Most examples of code in this README will be in elixir. If you would like to
learn a little more about elixir, head over to
[learn-elixir](https://github.com/dwyl/learn-elixir).

## Data Structures

As we mentioned earlier, data structures refer to how data is organised. This
organisation is not just for organisations sake however. The data structures you
use could massively effect the speed at which your application runs. It could
even be the difference between whether you app runs at all or errors because it
cannot handle the load.

Learning about the different types of data structures and the pros/cons of each
will allow you to pick the one that best suits the needs of your application.

### Operations

Operations are how we interact with data structures. Some of the common
operations are as follows:

 - Insert: To add a value to a data structure
 - Delete: To remove a value from a data structure
 - Read: Looking something up from a specific spot in a data structure
 - Search: Looking for a value in a data structure

Different operations run at different speeds. However, speed is not measured in
time as you expect. It is measured in the number of steps that the operation
takes to complete.

The reason for this is because the time an operation will take can vary from
machine to machine. It may take 5 seconds to search for a value on an older
computer compared to 2 seconds on a newer one, despite the fact that they are
using the same operation.

If the operation is measured in the number of steps that it takes though, this
is a constant value that will not vary no matter the machine. If a operation
takes 2 steps on 'machine a', it will take 2 steps on 'machine b'. And an
operation that take 2 steps will always be faster than an operation that
takes 200.

Now let's take a look at these operations being applied to an array (the first
data structure we are going to look at)

### Array

An [array](https://en.wikipedia.org/wiki/Array_data_structure) is just a list of
data elements.

```
array = ["one", "two", "three", "four", "five"]
```

#### Reading
> The following examples are not 'exactly' how the computer store arrays in
memory. The computer actually stores all the elements of an array together in
memory, with each cell of the computers memory holding one elements value. The
computer records the memory address of where that array started and uses it to
jump straight to that spot in memory. How the computer store the information is
not the key point here so we will not go into much detail here.

Reading from an array takes one step. Each cell in an array is given an index.
The index always begins at 0 and increases by 1 with each element. The
computer is able to 'jump' to any index in an array and get the data from
inside.

So for using the array above, say we want to get the element from the 2nd index.
The computer knows that the first index is index 0 and that index 2 is exactly 2
over from index 0. With this the computer can jump right to the 2nd and then
grab the data from that point.

#### Searching
If we wanted to check if a value exists in this array then we would use the
search operation. Say we wanted to check if the value `"six"` was in the array.
We can just glance at the array and clearly see that it is not but the computer
does not have this skill. The computer needs to access every element
individually and check if the value it get's back is `"six"`. If it finds a
match it will stop and return true else it will continue till there are no more
elements, at which point it will return false.

Let's count the number of steps that searching our array for the value "six"
would take. The computer starts by checking index 0 and sees that the value it
contains is `"one"` so moves on to the next index. At index 1 it checks the
value and sees that it is `"two"`. This is not what we are looking for so the
computer again moves on....
(the computer repeats these steps until it gets to the end of the array).

In total the computer had to check 5 elements before it could be sure that the
value was not there so this operation took 5 steps to complete. If the array
had a million values then the operation could potentially take million steps to
complete. However, if the element we were searching for was the first element in
the array, then the operation would only take 1 step. The number of steps is
dependent on where or if the element is in the array.

This type of search is known as a linear search. There are other, more complex
types of search as well but this is just a basic search that will work will all
array types.

#### Inserting and deleting
Inserting and deleting from an array work fairly similarly to one another so
I'll cover both here.

Say we want to insert a value into our array. Similar to how the number of
steps in searching is dependent on where the value is in the array, inserting
depends on where you want to insert the element into the array. If you want to
insert an element on the the end of an array then this is considered the 'best
case scenario' as it only take the computer one step.

The number of steps increase when you want to insert an element anywhere else in
the array. Say for example you want to insert the `"ten"` into our array from
earlier at index 2. Currently, index 2 has a value. It has a the value
`"three"`. As we do not want to replace any of the values in our array, we only
want to add to it, we first need to shift all the values over to make space.

This means that `"five"` would become index 5, `"four"` would become index 4 and
`"three"` would become index 3. Each one of these is an individual step as the
next index cannot be shifted until the former has been complete. Now index 2 is
free and we can insert the new value `"ten"` in.

Our array looks like this now...
```
["one", "two", "ten", "three", "four", "five"]
```

This insert would have taken 4 steps in total.
```
step 1 - shifting value "five" from index 4 to index 5
step 2 - shifting value "four" from index 3 to index 4
step 1 - shifting value "three" from index 2 to index 3
step 1 - inserting value "ten" in index 2
```

The worst case for inserting into an array would be inserting into the start of
it as all elements would have to be shifted before the insert could take place.
This would mean that in our array of 5 elements the number of steps to take
would be 6. Put another way, if `N` is the number of elements, the number of
steps in the worst case for inserting is `N + 1`.

Deleting is very similar to the above. The best case is to delete an element
from the end of the array and this will only take 1 step.

If we want to delete the value at index 2 from our array (the value `"ten"`)
then the following steps would be taken...
```
step 1 - deleting value "ten" in index 2
step 1 - shifting value "three" from index 3 to index 2
step 2 - shifting value "four" from index 4 to index 3
step 1 - shifting value "five" from index 5 to index 4
```

The worst case for deleting, just like inserting, is to delete the first
element from the array.

### Set (array-based set)

An array based set is very similar to an array but with one key difference, it
never allows duplicate values to be inserted.
