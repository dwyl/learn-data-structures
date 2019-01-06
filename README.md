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
pick the right algorithm is key.

## *How*?

Most examples of code in this README will be in elixir. If you would like to
learn a little more about elixir, head over to
[learn-elixir](https://github.com/dwyl/learn-elixir).

## Data Structures

As we mentioned earlier, data structures refer to how data is organised. This
organisation is not just for organisation's sake however. The data structures you
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
> The following examples are not 'exactly' how the computer stores arrays in
memory. The computer actually stores all the elements of an array together in
memory, with each cell of the computer's memory holding one element's value. The
computer records the memory address of where that array started and uses it to
jump straight to that spot in memory. How the computer stores the information is
not the key point here so we will not go into much detail here.

**Reading from an array takes one step**. Each cell in an array is given an index.
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
We can just glance at the array and clearly see that it is not, but the computer
does not have this skill. The computer needs to access every element
individually and check if the value it get's back is `"six"`. If it finds a
match it will stop and return `true` otherwise it will continue until there are no more
elements, at which point it will return `false`.

Let's count the number of steps that searching our array for the value `"six"`
would take. The computer starts by checking index 0 and sees that the value it
contains is `"one"` so moves on to the next index. At index 1 it checks the
value and sees that it is `"two"`. This is not what we are looking for so the
computer again moves on....
(the computer repeats these steps until it gets to the end of the array).

In total **the computer had to check 5 elements before it could be sure that the
value was not there so this operation took 5 steps to complete**. If the array
had a million values then the operation **could potentially take a million steps** to
complete. However, if the element we were searching for was the first element in
the array, then the operation would only take 1 step. **The number of steps is
dependent on where or if the element is in the array.**

This type of search is known as a **linear search**. There are other, more complex
types of search as well but this is just a basic search that will work with all
array types.

#### Inserting and deleting
Inserting and deleting from an array work fairly similarly to one another so
I'll cover both here.

Say we want to insert a value into our array. Similar to how the number of
steps in searching is dependent on where the value is in the array, inserting
depends on where you want to insert the element into the array. If you want to
insert an element onto the end of an array then this is considered the 'best
case scenario' as it only take the computer one step.

The number of steps increase when you want to insert an element anywhere else in
the array. Say for example you want to insert the value`"ten"` into our array near the
beginning at index 2. But index 2 already has a value, it has the value
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
step 3 - shifting value "three" from index 2 to index 3
step 4 - inserting value "ten" in index 2
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
step 2 - shifting value "three" from index 3 to index 2
step 3 - shifting value "four" from index 4 to index 3
step 4 - shifting value "five" from index 5 to index 4
```

The worst case for deleting, just like inserting, is to delete the first
element from the array.

### Set (array-based set)

An array based set is very similar to an array but with one key difference, **it
never allows duplicate values to be inserted.**

For example, what have the following set...
```
set = [1,2,3]
```

If we tried to add `1` to the set the computer would not let it happen as the
set already contains the value.

Sets come in handy when you need to make sure that you have no duplicate
data.

The operations that we used on our array all work in the same way on our set,
with the exception of insert.

When we call insert on our array based set it does work similarly to our example
above but, before it can insert, it first needs to check every cell to make sure
the value we want to insert is not already in the set.

Let's take our currently defined set and try to insert the value `4` onto the
end

```
step 1 - check the value at index 0
step 2 - check the value at index 1
step 3 - check the value at index 2
step 4 - insert value 4 onto the end of set
```

In the above example, we inserted onto the end of our set and it took 4 steps.
Like inserting onto the end of an array, this is the best case scenario. Unlike
the array, this took 4 steps compared to 1.

This means that if we had a set containing 1,000,000 items and we wanted to
insert onto the end of that set it would take 1,000,000 steps checking the
values in the indexes and then 1 step inserting. Number of steps is `N + 1`.

Remember, this is the best case scenario. The worst case scenario is if want to
insert into the first element of our set. If we so this, it has to first check
every index, then shift every index over by one (like inserting into the array
did).

Let's insert `4` into the start of our set this time...

```
step 1 - check the value at index 0
step 2 - check the value at index 1
step 3 - check the value at index 2
step 4 - shift the value 3 to index 3
step 5 - shift the value 2 to index 2
step 6 - shift the value 1 to index 1
step 7 - insert value 4 into index 0
```

This took 7 steps to complete. The way we could express this 'worst case
scenario' is `2N + 1`.

As you can see this is almost exactly double the number of steps needed to
insert into an array. That doesn't mean that sets are a bad data structure
however. If you need to make sure there is no duplicate data then this could be
the right fit for you. If not, you may be better off with an array.

### Ordered Array

An ordered array is again very similar to an array. The difference here, as the
name suggests, is that this array has to be ordered.

Lets take the following array...
```
[1,2,4,5]
```
and try to insert the value `3`.

Inserting works in a similar way to the set insert. First the computer would
have to go to index 0 and compare the value inside against the one we want to
insert. If the value we want to insert is greater than what is inside index 0,
then we move on. It repeats the steps until it comes across a value that is
greater than the value we want to insert. At this point it then shifts all the
values up an index and inserts the value.

In our case `3` would be inserted into index 2.

Search also works in a similar way to previous examples but with a key
difference. With an ordered array, a search can stop early if we know a value
could not possibly be contained in the array.

For example take the following array
```
[1, 10, 37, 85, 96]
```

Now we tell computer to search this for the value `26`. As we mentioned, the
computer will need to check each cell, one at a time, in order, so it sounds
pretty similar to the previous searches. The difference here is that when the
computer comes across a cell that has a larger value than the one we are
searching for, it can immediately stop looking as it knows it can not exist past
that point.

```
step 1 - check the value at index 0
step 2 - check the value at index 1
step 3 - check the value at index 2
```

Only 3 steps needed. Once the computer gets to `index 2` and sees the value `37`
it knows that is larger than the `26` we are looking for and can stop searching
at that point.

Of course this won't always be the case. If you were looking for 96, or greater,
the search would still have to check every cell.

However this assumes that our search always starts at the beginning of an array
and works its way through looking for the element in question. This is not true.
A linear search is just one of many algorithms that can be used for searching
arrays.

## Algorithms

An algorithm, as we mentioned earlier, is a set of steps for solving a problem.

There are many different algorithms, and there are often multiple algorithms
that can be used to achieve the same end results. How they work will be
different however.

Imagine you are travelling home and your travel options are, a combination of
public transport and walking, or riding a bike. Both will have the same result
of getting you home but one may be faster, safer, more convenient etc. For
example, if your journey home was 300 miles long and there was a super fast
train that took you within a 2 minute walk of your front door, this may be a
better option than riding your bike home (unless you like that kind of thing).
But this doesn't mean that public transport is always the way to go. Let's say
now your journey home is only 2 miles and there is no direct transport option.
In this situation it may be better for you to ride your bike.

The point of the above is to show that although both have the same result,
depending on the situation, each 'algorithm' has its purpose.

Picking the one that suites your needs is important as it can greatly effect the
performance of an application.

We have already seen how to perform a linear search on an array so let's check
out a new type of search. Binary.

Binary search works by checking the middle element of a list, checking if it
contains the value we are after, and depending on the value in that cell, knows
if is should check the first or second half of the array. This means that after
just one step, binary search has already found that it no longer needs to search
half of the elements in the list (because of the way it works binary search
can only be used on ordered arrays).

Let's look at an example array of 1 to 10.
```
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

And search for the value `7`.

If we were to use linear search the computer would check each cell, starting at
`index 0` and working its way up the indexes until it finds our value. We can see
that this would take `7` steps.

Let's see how binary search will effect this.

First the computer jumps to the middle of the array and checks the value there.
That value is `5`. As we are searching for the number `7`, and as this is an
ordered array, the computer knows that everything 'to the left' of index 4 is
also lower in value than 7. This means that is can remove these from the list of
possible indexes left to check.

Now we are left with the values 6 to 9 to check. The computer will again pick the middle index and check to see if it contains our number. In our case there is no exact middle. Could be index 6 or 7 (values 7 or 8) but we'll say in this case the computer picks the lower of the two middle choices and goes with index 6.

Binary search just found our number in 2 steps!!!!!


```
step 1 - check the value at index 4
  value is 5 so computer discards it and everything to the left away
  left with indexes of 5,6,7,8
step 2 - check the value at index 6
  value returned is 7
```

Let's do another example where we have to look for `1,000,000` from an array of
numbers ranging from 1 to 1,000,000. Remember, this is a worst case scenario.

As mentioned in the searching section above, the linear search would take
all `1,000,000` steps to complete this. Let's compare this to the binary search

Binary steps
```
  step 1 - check the value at 500,000
    value is less than we are looking for so discard it and everything less than
    it. (Just cleared HALF A MILLION STEPS IN ONE GO!!!!)
  step 2 - check the value at 750,000
    value is less than we are looking for so discard it and everything less than
    it.
  step 3 - check the value at 875,000 - too low, discard all to left
  step 4 - check the value at 937,500 - too low, discard all to left
  step 5 - check the value at 968,750 - you get the idea...
  step 6 - check the value at 968,750
  step 7 - check the value at 984,375
  step 8 - check the value at 992,187
  step 9 - check the value at 996,093
  step 10 - check the value at 998,046
  step 11 - check the value at 999,023
  step 12 - check the value at 999,511
  step 13 - check the value at 999,755 - getting close
  step 14 - check the value at 999,877
  step 15 - check the value at 999,938
  step 16 - check the value at 999,969
  step 17 - check the value at 999,984
  step 18 - check the value at 999,992
  step 19 - check the value at 999,996 - nearly there
  step 20 - check the value at 999,998
  step 21 - check the value at 999,999
  step 22 - check the value at 1,000,000 - WE MADE IT
```

This might seem like a lot of text/steps but just think about what this search
algorithm just managed to do. It took a worst case scenario of searching an
array of `1,000,000` values for its `1,000,000`th value and fount it in 22
steps.

This means the maximum number of steps searching an ordered array of a million
values with binary search is `22`. Quite the improvement over a million I'm sure
you'll agree.

Check out [this youtube video](https://www.youtube.com/watch?v=EXtkCmRXfMo) to
learn more about binary and linear search.
