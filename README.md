# The `for` Loop

## Objectives

1. Identify when to employ looping.
2. Learn the anatomy of a loop.
3. Walk through how to build a `for` loop.

## Loop-de-loop

Unlike most humans, computers are really great at performing repetitive tasks quickly and accurately. This is a lot of why we find them so useful!

So far, everything that we've covered has a simple flow—what we've typed only gets executed once. We can copy/paste easily enough, but that only works for a handful of repetitions and can quickly make our code difficult to read.

```objc
NSLog(@"To the rolling of the bells--");
NSLog(@"Of the bells, bells, bells--");
NSLog(@"To the tolling of the bells,");
NSLog(@"Of the bells, bells, bells, bells--");
NSLog(@"Bells, bells, bells--");
NSLog(@"To the moaning and the groaning of the bells.");
```

**//Flat-fact:** *Generating the last few lines of Edgar Allan Poe's poem "Bells" is a common code-challenge among programmers.*

So what happens when we want to perform the same action multiple times without retyping it? We create a loop!

## Loop Anatomy 101

In structured programming, a "loop" is the concept of repeating a set of instructions until a condition or set of conditions is met. They are generally governed by a "counter" variable that is set at run time so that the number of iterations that the loop performs is dynamic and correct for its present situation. Although there are different types of looping constructs in Objective-C, we'll be taking a look at the `for` loop in this lesson. Let's take a look at an example, and then we'll break down the different components of a loop:

```objc
for (NSUInteger i; i < n; i++) {
    // instructions for each pass through the loop go here.
}
```

The `for` loop, so named  because it begins with the key word "for", has three parts: 

  * The name of the loop construct, in this case `for`.
  * A parenthetical `(` `)`,  which is comprised of three short statements separated by semicolons (`;`):
      - the variable "initialization" (usually `NSUInteger i`),
      - the "conditional" check (usually `i < n` for some value `n`),
      - the "increment" step for each pass of the loop (usually `i++`).
  * The body of instruction "statements" inside the curly braces `{` `}`.

**Note:** *The "increment operator" (* `++` *) means "add one" and is equivalent to setting the integer to itself plus one, as in* `i = i + 1`.

## Implementing A Loop

### Buffalo buffalo Buffalo buffalo buffalo buffalo Buffalo buffalo.

The English language permits some rather odd sentences to be grammatically correct—albeit, in bad style due to their confusing nature. This repetitive sentence first appeared in print in 1967 in Dmitri Borgmann's *Beyond Language: Adventures in Word and Thought*. This [Wikipedia](https://en.wikipedia.org/wiki/Buffalo_buffalo_Buffalo_buffalo_buffalo_buffalo_Buffalo_buffalo) page parses out its structure and meaning which translates to "Bison from Buffalo, New York, who are intimidated by other bison in their community, also happen to intimidate other bison in their community."

Let's use this sentence as an example problem for writing a `for` loop. We need to print the word "buffalo" eight times, with a space between each one and a period at the end. Also, you'll notice that the first, third, and seventh repetitions of the the word are capitalized. This is important to the grammar of the sentence, indicating that they're proper nouns. Let's be sure to factor that into our solution as well.

Before we start on our `for` loop, we're going to need a container to hold the sentence as we build it. Let's use an `NSMutableString` object for this purpose. We'll need to declare and initialize it *before* we start the loop, however, since anything created within the **scope** of the loop will get destroyed at the end of each pass, or *iteration*, through it. (We'll explain scope in more detail in a future reading.)

```objc
NSMutableString *grammarQuirk = [[NSMutableString alloc] init];
```

Remember that when creating a mutable string, we can't use the literal string syntax directly since it only creates *immutable* (or "static") `NSString` objects. The line above will generate an empty mutable string, which is exactly what we want to start with in this case.
    
### Setting The Counter
    
Now, let's start writing that `for` loop. Notice that when you type in `for`, Xcode offers you an autocomplete field that looks like this:

```objc
for (initialization; condition; increment) {
    statements
}
```

This is really handy for reminding us what goes where. In this first line, we need to declare our counter, its end point check, and the increment of the counts between each loop. Filled in, that first line should look like this:

```objc
for (NSUInteger i = 0; i < 8; i++) {
    statements
}
```

**Note:** *It's a general practice to start the loop's counter at* `0` *since loops are often used for passing through arrays by index which begins at* `0`. *We'll discuss arrays in the next reading.*

### Develop The Behavior

Now that we have our counter set up to govern our loop for eight passes, let's build the loop's body of statements. We want to add the word "buffalo" each time, so let's use the `appendString:` method to add it to our sentence within the loop:

```objc
NSMutableString *grammarQuirk = [[NSMutableString alloc] init];

for (NSUInteger i = 0; i < 8; i++) {
    NSString *buffalo = @"buffalo";
    [grammarQuirk appendString:buffalo];
}

NSLog(@"%@", grammarQuirk);
```

This will print: 
`buffalobuffalobuffalobuffalobuffalobuffalobuffalobuffalo`.

Hm, well that's a good start, but it's not really a sentence yet. Let's use the `appendFormat:` method instead in order to add a space between each word.

```objc
NSMutableString *grammarQuirk = [[NSMutableString alloc] init];

for (NSUInteger i = 0; i < 8; i++) {
    NSString *buffalo = @"buffalo";
    [grammarQuirk appendFormat:@"%@ ", buffalo];
}

NSLog(@"%@", grammarQuirk);
```

This will print: 
`buffalo buffalo buffalo buffalo buffalo buffalo buffalo buffalo `.

### Adding Conditionals

That's better, but we need to add some checks. We can actualy put conditionals *within* the loop's body that will only perform the given actions on certain iterations of the loop. Let's use an `if` statement and the `capitalizedString` method to turn the first, third, and seventh words into proper nouns:

```objc
NSMutableString *grammarQuirk = [[NSMutableString alloc] init];

for (NSUInteger i = 0; i < 8; i++) {
    NSString *buffalo = @"buffalo";
    if (i == 0 || i == 2 || i == 6) {
        buffalo = [buffalo capitalizedString];
    }
    [grammarQuirk appendFormat:@"%@ ", buffalo];
}
    
NSLog(@"%@", grammarQuirk);
```

This will print: 
`Buffalo buffalo Buffalo buffalo buffalo buffalo Buffalo buffalo `.

We're almost there! For it to be a truly correct sentence, however, we need to end it with a period. Let's add a separate check to see if the loop is on the final word so it can decide whether to add either a space before the next word or the period that ends the sentence. Since we only need to add one period, we can write our check against the final word, and allow adding a space to remain the default behavior:

```objc
NSMutableString *grammarQuirk = [[NSMutableString alloc] init];

for (NSUInteger i = 0; i < 8; i++) {
    NSString *buffalo = @"buffalo";
    if (i == 0 || i == 2 || i == 6) {
        buffalo = [buffalo capitalizedString];
    }
    
    if (i == 7) {
        [grammarQuirk appendFormat:@"%@.", buffalo];
    } else {
        [grammarQuirk appendFormat:@"%@ ", buffalo];
    }
}
    
    NSLog(@"%@", grammarQuirk);
```

This will print: 
`Buffalo buffalo Buffalo buffalo buffalo buffalo Buffalo buffalo.`.

Perfect!

Take a look at this post by [MentalFloss](http://mentalfloss.com/article/49238/7-sentences-sound-crazy-are-still-grammatical) which lists a handful of other quirky sentences which are grammatically correct. None of the others lend themselves quite so well to looping, however.
