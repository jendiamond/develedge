---
title: "ELM"
date: 2019-05-19T21:29:48-07:00
draft: true
---

# ELM

+ :reset
+ :exit
+ :help


+ http://localhost:4000/The%20Basic%20Building%20Blocks%20of%20Elm.html
+ https://elmbridge.github.io/curriculum/Getting%20Started.html
+ https://github.com/elmbridge/curriculum
http://localhost:4000/Building%20User%20Interfaces.html
http://localhost:8000/Main.elm
https://github.com/elmbridge/elmoji-translator/releases/tag/release-6

https://elmbridge.github.io/curriculum/The%20Elm%20Architecture.html



---

#### [currying](https://en.wikipedia.org/wiki/Currying)
Currying is when you break down a function that takes multiple arguments into a series of functions that take part of the arguments.
+ https://stackoverflow.com/questions/36314/what-is-currying

<details><summary>Here's an example in JavaScript:</summary>
  
```  
function add (a, b) {
  return a + b;
}

add(3, 4); // returns 7
```
This is a function that takes two arguments, a and b, and returns their sum. We will now curry this function:
```
function add (a) {
  return function (b) {
    return a + b;
  }
}
```

This is a function that takes one argument, a, and returns a function that takes another argument, b, and that function returns their sum.

```
add(3)(4);

var add3 = add(3);

add3(4);
```

The first statement returns 7, like the add(3, 4) statement. The second statement defines a new function called add3 that will add 3 to its argument. This is what some people may call a closure. The third statement uses the add3 operation to add 3 to 4, again producing 7 as a result.

</details>

---

#### [bitwise](https://en.wikipedia.org/wiki/Bitwise_operation)
In digital computer programming, a bitwise operation operates on one or more bit patterns or binary numerals at the level of their individual bits. It is a fast and simple action, directly supported by the processor, and is used to manipulate values for comparisons and calculations.

On simple low-cost processors, typically, bitwise operations are substantially faster than division, several times faster than multiplication, and sometimes significantly faster than addition.[clarification needed] While modern processors usually perform addition and multiplication just as fast as bitwise operations due to their longer instruction pipelines and other architectural design choices, bitwise operations do commonly use less power because of the reduced use of resources.

---

### What's next?
elm-camp.md https://github.com/ElmLA/org/blob/primary/resources/elm-camp.md

Elm LA

#elm-la elmlangslack.com | elmlang.herokuapp.com

+ Elm in the Spring (Chicago)
+ elm-Europe (Paris)
+ elm-conf(st.loius)

---

Elm resources & information from ElmBridge:

ElmBridge curriculum: https://elmbridge.github.io/curriculum/ - this is the main curriculum that we were following today, which includes links to the code we were working with. The curriculum is open-sourced and maintained by Elm community organizers around the world; you're very encouraged to contribute to it!
ElmCamp tutorial: bit.ly/elm-camp - a tutorial which goes through making API requests and parsing JSON (it's still a work in process so it's way less fleshed out than the main curriculum, but we're in the process of updating it to make it more amenable to self-paced learning); also links to tons of learning resources as well.
Keep in touch on Slack
elmlang.herokuapp.com will get you an invite to the Elm language Slack
stay in touch with Elm LA people at #elm-la (your organizers today were @zack, @anup, @emma)
the #beginners channel is full of folx eager to help those new to Elm
Meetups:
Elm LA - meetup.com/elm-la/
Elm OC - meetup.com/elm-oc
Conferences:
Elm in the Spring (Chicago 4/26): elminthespring.org
Attendee & ticket grants (due Tues, April 16 at 3:00 pm EST): https://forms.gle/MLG3ybSoG9UAETqNA
Elm Europe (Paris 6/27-6/28): elmeurope.org
elm-conf (St. Louis 9/12): elm-conf.com
Call for proposals are now open and close 5/10 (if you submit by 5/5, you'll get personalized feedback). If you'd like support in coming up with a topic, crafting a proposal, etc. please fill out this form to let us know how we can best support you! https://emmacunningham.typeform.com/to/Mwf49r
Help organize a future ElmBridge LA! - We'd love to do more of these in the future. If you'd like to help organize a future event, please let us know!
We could not have done this without the support of our sponsors, Pivotal and findSisterhood.

Pivotal (with a shout out to Desmond & Mejin for everything they did to make the space available for us today!)

check out their open positions here: https://pivotal.io/careers
findSisterhood (many thanks to Ana, Maria, and Thereza for the food sponsorship & inspiring Q&A at lunch!)

LA launch event information (5/2 at Pivotal): https://www.eventbrite.com/e/join-us-to-celebrate-the-launch-of-findsisterhood-in-la-tickets-59494124528
as Ana mentioned during lunch, they are hiring across levels for developers!: https://www.findsisterhood.com/jobs

---

Emma Cunningham has something to say about a past event:
Hi all,

thank you so much for attending the ElmBridge workshop and congratulations for everything you were able to accomplish today. We hope to see you at an upcoming meetup, a future ElmBridge event, or speaking at a conference about your experiences with Elm!

As promised, here's a link to a list of all the resources and announcements from today:
https://github.com/ElmLA/org/blob/primary/resources/elm-bridge-resources.md

**We could not have done this without the support of our sponsors, Pivotal and findSisterhood!**
Links to their hiring pages & findSisterhood's launch event are also in the link above.

**Thank you again to our incredible mentors, Liz & James!**

And once more, thank YOU for attending today and helping us build a more diverse and inclusive community in Elm, functional programming, and the tech industry at large. It was a dream come true to be able to share this day with you all, and we hope to see you soon (and hear how your work with Elm is coming along!).

In gratitude,

Emma, Zack, & Anup

Check out this event on Bridge Troll by clicking this link!

