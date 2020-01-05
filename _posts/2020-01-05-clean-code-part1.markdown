---
layout: post
title:  "Clean and Testable Code Part-1"
date:   2020-01-05 00:31:52 -0500
categories: jekyll update
---
A musician on his way to play got lost and asked an old man "_How to reach Carnegie Hall?_". He said "_Practice son. Practice_".

That sums up on how to write clean code. Writing a beautiful code according to me is an art a programmer needs to have. When I write code and  read it, I try and change it many times so that it does not give me a headache and am actually proud of it. It comes through practice or say in corporate terms continuous internal improvement. It is personal and everyone has different views.

This article is for me to remember few important principles that I look to have when I code something. There are more things to understand on writing cleaner code. But below are the few things I find one need to tackle first.

Readability
No duplication
Less clutter
Error Handling
Unit test cases

### Readability ###

"Say what you mean. Mean what you say" Clean Code, Martin, Robert C.

By this I merely mean on have meaningful names. This is the most I struggle with, could be because I cannot articulate my feelings enough. Who knows!! However, I think I am trying to find some thumb-rules to follow
- We want short and meaningful names. But it is okay to have long names(Indian, of course!!) as long as it provides context. I prefer longer names for my test cases and functions. It increases readability.
   - getUsers vs getUsersByGender(trying to be less controversial)
- Avoid using similar words for variables UserInfo and UserData  in the same scope. 
- Class Names : Nouns and Noun Phrases Method names: Verb  and Verb Phrases
- Use jargon, FactoryMethod, Handler, Observer.
- Use names from the problem domain
- Do not add unnecessary context.  Add it think twice and see if you are telling exactly what is necessary, Not a word more Not a word less. 
- Consistency is key. Use same words for same context. 
You might ask, do we need to do so much thinking? I think we should if we care and respect the code.

### Less Clutter and No Duplication ###

>"_Functions should do one thing. They should do it well. They should do it only_" -SRP

There is lot of clutter in functions. And this is a very arguable topic in my team. Two word answer: Small functions, No Duplication. Okay, more like 4 words. But you get the point!!
 
#### Why small? ####
Smaller functions follow Single Responsibility Principle well.<br/>
Enables us to keep our functions more generic<br/>
Helps us to keep duplication in check<br/>
Also, if you have written any competitive exams, 80% of the time longer reading comprehensions - look apprehensive and tough. A function should not do that to any body.<br/>
Rule of Thumb: Any code more than 10(arbitrary) should be refactored.Like the author William Zinsser says in "On Writing Well". The hardest part is not editing 3 pages of text to 1.5 pages, but 1.5 pages to 1 page. So, write 3 pages of code, refactor and refactor.


#### Function Arguments ####
More than two should be avoided. A strict rule to employ. Personally it is the second most difficult thing to apply.

#### Side Effects ####
Something functional programming promises. Doing more than a function supposed to. Effecting variables outside its scope in short.

{% highlight ruby %}
List<Order> orders;
//No Side effects
void getUserOrders(String userId){

return orders.stream().filter(order->order.getUserId().equals(userId)).collect(Collectors.toList());
}

//Side effects
void getUserOrders(String userId){
orders = orders.stream().filter(order->order.getUserId().equals(userId)).collect(Collectors.toList());
return orders;
}
{% endhighlight %}

- Function should either do operations or answer something not both
- Main problem exists when we start dealing with error handling. I would rather do error handling in the main service and the other lower operations by themselves. Also, allowing functions to throw application specific exception is always nicer so that they could be nicely packaged and customized for logging. 
- Also how to handle error handling when we deal with I/O operations. Wo!! I/O operations are nasty. May be we deal with a separate section.


#### Error Handling ####
First thing I do always is a null check or a code review comment is a null check. I think this is where I like people to chime in and give me ideas. 
And lets just say that we should ask the creator of null, like a French waiter asked me when I said "No fish", "Why? Why woman, why? Arghhhhh!"

- I honestly think we should get rid of null check everywhere and or may be some programmers do use Assert for readability and means of handling it. We should use it wisely like for I/O operations.
- Remove all null return and null arguments. 

Separate try-catch handling from the actual code and wrap it in a separate function. Also, smaller functions helps to handle less exception situations.

#### Unit Tests ####
Books are written on this and software models are created on this. It is not debatable, you cant have a code with out test cases. I think, it is very important to have test cases to have a maintainable application. Well named test cases could act as a document for a newly on-boarded developer.

Clean code is important here too. 

- Readable and meaningful test functions names. Tell people what are we testing? 
  - confusing one: testGood() or testBad()
  - more detailed name:  givenShortPassWordThenReturnInValid() or givenShortPassWordThenThrowException()
- Like one function does one thing one test should do one thing. 
- With changes to code, update the tests too
- Keep test code updated and clean. It is more important here.
- Never code, before writing tests. And please, please, please always write tests.


These are for me to understand some of my thoughts. Also, I want to end by saying "_Always leave your code and Our Earth cleaner than you found it._" (Read somewhere and added my philosophy)
