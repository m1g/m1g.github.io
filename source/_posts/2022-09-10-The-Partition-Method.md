---
title: The Partition Method
date: 2022-09-10 19:31:55
tags:
- Javascript
categories: 
- Tech
---

I went down a rabbit hole and found this method that had been hiding in plain sight. Partitioning a list  

 <!-- more -->

 ---

## What was the challenge?

I'd been looking for a way to separate a list of emails into two buckets, valid and invalid, so that I could log out the invalid emails and present that to the user. It'd already been a challenge because I'm working in Rails, but that just meant that I'm going to have to add some javascripty looking ruby code 😈


```ruby
# the heavy-handed operation I wrote looked something like this
valid = []
invalid = []

valid = emails.map {|email| validator.is_valid(email)}
invalid = emails.map {|email| !email.is_valid(email)}
```

But lo - and as I'd hoped, a patron saint of code feedback teammate of mine came through with some constructive feedback that ~~I could have used a year ago~~ changed everything.

## What was ['the way'][the way]?

Enter ruby's built-in partition method. It returns two arrays - the first containing the elements that return true and the second returns the rest 🔥 It made my day and now my method looks like: 

```ruby
valid, invalid = emails.partition {|email| validator.is_valid(email)}
```

So the next logical step is to ask myself, "does javascript have this?"

## Well, does Javascript have it?

The answer as of June in the year of our Lord 2021, is... **not out of the box**. But fortunately for me, our project is using lodash and sure enough, `_.partition` exists! [Lodash partition][lodash partition] behaves similar to the built-in ruby version, but with a slightly different syntax:

```javascript
// syntax
_.partition(collection, predicate)
```
It accepts two parameters. The **collection** to iterate over and the **predicate** which is the function to be invoked per iteration. Then it returns an array of grouped elements:

```javascript
// example from above where 'emailValidator' returns a bool
let [ valid, invalid ] = _.partition(emails, emailValidator(email))
```

_Just to note, I'm destructuring the arrays into separate buckets here for the purposes of my example._ 

And that's it! I've found a new tool to add to the toolbox, that I look forward to using much more of in the future.




<!-- LINKS -->

[lodash partition]: https://lodash.com/docs/#partition
[the way]: https://i.imgur.com/Fk69QjI.gif