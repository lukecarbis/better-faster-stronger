name: title
class: center, middle, inverse, inverse-dark

# .green[Better] .red[Faster] .blue[Stronger]
### Best Practices for Coding in WordPress

[View this presentation on [GitHub](https://github.com/lukecarbis/better-faster-stronger)]

[Press .magenta[P] to view notes]

???

There is so much to learn when you're first starting out with WordPress development.

Most of us start out by copying some code into our themes functions.php file. It's quick and dirty, but it works. You might not even understand *how* it works, but that's okay for now.

* https://github.com/lukecarbis/better-faster-stronger

---

name: contents
class: center, middle

## .blue[Scripts & Styles]
## .magenta[AJAX]
## .cyan[Namespacing]
## .yellow[Database Queries]
## .violet[Coding Standards]

???

There are many conventions and standards in WordPress development. We can't remember them all. These are the most important ones (IMHO).

---

name: wait
class: center, middle, inverse, inverse-red
background-image: url(assets/img/wait.gif)

# Wait... what, why?
## If it 'aint broke, why fix it?

???

One of the first steps you'll need to take toward becoming a more competent WordPress developer is ensuring your code works, and works the way it should.

But if your code already works, why would we ever bother to change it?

---

name: capital-p-dangit
class: center, middle, inverse

# Wordpress

What's wrong here?

![Picard is ashamed](assets/img/lower-p.gif)

???

Does anyone know what's wrong with this screen?

---

name: capital-p-fixed
class: center, middle, inverse

# WordPress

Capital P, dangit!

![Well done, number one](assets/img/upper-p.gif)

???

It's not Wordpress with a small P, it's WordPress with a capital P. This is so important to some people that there is actually code inside your WordPress site that will correct this mistake without even asking you.

Before I begin explaining some of these best practices to you, it's worth mentioning why they're worthwhile.

---

name: why

## Why are these conventions so important, anyway?

---

name: why-prevent-conflicts

## Why are these conventions so important, anyway?

.contents[
* Prevent conflicts
]

???

We recently discovered a bug in Stream Reports, which was causing our reports page to go crazy if another plugin was enabled. This happened because the other plugin wasn't including their javascripts properly, and they were conflicting with some of the scripts on our page, causing errors.

---

name: why-prevent-loading-unecessary-files

## Why are these conventions so important, anyway?

.contents[
* Prevent conflicts
* Prevent loading unecessary files
]

???

Doing things according to standards will speed up and streamline your site

---

name: why-readability

## Why are these conventions so important, anyway?

.contents[
* Prevent conflicts
* Prevent loading unecessary files
* Readbility
]

???

There's a great talk on WordPress.tv by Nikolay Bachiyski, who talks about the way other developers read your code. It's not only about reading line by line, it's also about easily leading others through your thought process - so your process needs to make sense.

* http://wordpress.tv/2013/08/15/nikolay-bachiyski-writing-code-as-user-experience-design/

---

name: why-maintainability

## Why are these conventions so important, anyway?

.contents[
* Prevent conflicts
* Prevent loading unecessary files
* Readbility
* Maintainability
]

???

Sticking to the standards ensures that your code makes sense to the most important developer: Future You.

---

name: why-list-goes-on

## Why are these conventions so important, anyway?

.contents[
* Prevent conflicts
* Prevent loading unecessary files
* Readbility
* Maintainability
* Load scripts in the correct order
* Play nice with other plugins
* Automatic minification
* Dependencies loaded
* Include all WordPress functionality
* Handling nonces correctly
* Prevent SQL injection attacks
* Encourage community support
* And so on...
]

???

The list goes on.

---

name: simple-reason
class: center, middle, inverse

## Best practices exist to make your code
# .green[Better], .red[Faster] and .blue[Stronger].

???

The simple reason is that these sorts of conventions aren't (usually) arbitrary. They're designed to make your code better, faster and stronger.

---

name: break
class: center, middle, inverse
background-image: url(assets/img/break.gif)

Learn to write code you can be proud of.

???

Let's take 30 seconds to let that sink in, before we get to talking about the first topic: Enqueuing scripts and styles.

---

name: scripts-and-styles
class: center, middle, inverse, inverse-blue

# Scripts & Styles

---

name: coding-standards-kitten
background-image: url(assets/img/coding-standards.jpg)

???

## Coding Standards
### Why Bother?

