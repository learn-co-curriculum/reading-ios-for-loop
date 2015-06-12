# The `for` Loop

## Objectives

1. Identify when to employ looping.
1. Understand the anatomy of a `for` loop.
2. Learn the usages of `break`, `continue`, and `return` within loops.

## Loop-de-loop

Unlike most humans, computers are really great at performing repetitive tasks quickly and accurately. This is a lot of why we find them so useful!

So far, everything that we've covered has been single-instruction, meaning everything that we've typed only get run or executed once. We can copy/paste easily enough, but that only works for a handleful of repetitions and can quickly make our code difficult to read.

```objc
NSLog(@"To the tolling of the bells,");
NSLog(@"Of the bells,");
NSLog(@"bells,");
NSLog(@"bells,");
NSLog(@"bells--");

NSLog(@"Bells,");
NSLog(@"bells,");
NSLog(@"bells--");
NSLog(@"To the moaning and the groaning of the bells.");
```
So what happens when we want to perform the same action multiple times without retyping it? We create a loop!

![starfox](http://gph.is/1540ms8)





A loop is a concept in structured programming of repeating a set of instructions until a condition or set of conditions is met. They are generally governed by a counter that is set at run time so that the number of iterations that the loop performs is correct for the situation to which it is being applied. In Objective-C, the basic form of a loop is known as the `for` loop.

## Loop Anatomy 101

The `for` loop is named such because it begins with the key word "for". It has three parts: 

  * The function name, in this case `for`.
  * The conditional counter inside the parentheses `(` `)`, which is comprised of three short statements separated by semi-colons (`;`):
      - the variable "initialization" (usually `NSUInteger i`),
      - the "conditional" check (usually `i < n`),
      - the "increment" step for each pass of the loop (usually `i++`).
  * The body of instruction "statements" inside the curly braces `{` `}`.

**Note:** *The "increment operator" (* `++` *) means "add one" and is equivalent to the phrase* `+= 1`.

```objc
for (NSUInteger i; i < n; i++) {
    // instructions for each pass on the loop go here.
}
```



break

continue

return















