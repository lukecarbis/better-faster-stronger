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
## .cyan[Prefixing]
## .yellow[Database Queries]
## .violet[Coding Standards]

???

There are many conventions and standards in WordPress development. We can't remember them all. These are the most important ones (IMHO).

---

name: wait
class: center, middle, inverse, inverse-red
background-image: url(assets/img/wait.gif)

# Wait... what, why?

???

One of the first steps you'll need to take toward becoming a more competent WordPress developer is ensuring your code works, and works the way it should.

---

name: aint-broke
class: center, middle, inverse

# If it 'aint broke, why fix it?

???

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
* Readability
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

???

Now we've covered the why, let's cover some practical examples. The first is enqueuing scripts and styles. What does that mean?

---

name: scripts-and-styles-do-not

## Do not...

add html directly into your theme:
```html
<link href="style.css" rel="stylesheet" type="text/css" />
```
or
```html
<script type="text/javascript">
	var foo = 'bar';
</script>
```
or even
```html
<script src="//code.jquery.com/jquery-latest.min.js"></script>
```

???

Suppose you wanted to include a new javascript file or stylesheet in your theme or plugin. How would you go about doing that? You might be tempted to go ahead and edit your theme's `header.php` or `footer.php`. That's not the best way of doing things.

---

name: scripts-and-styles-better

## This is better:

In your plugin, or in your functions.php file, use the `wp_enqueue_script` and `wp_enqueue_style` functions:
```php
wp_register_script( 'select2', 'ui/select2/select2.min.js', array( 'jquery' ), '3.4.5', true );
wp_register_style( 'select2', 'ui/select2/select2.css', array(), '3.4.5' );

wp_enqueue_script( 'select2' );
wp_enqueue_style( 'select2' );
```
or
```php
wp_enqueue_script( 'my-script', 'ui/main.js', array( 'jquery', 'select2', 'heartbeat' ), 1.0 );
```

???

You can register your script first, then enqueue it if you like (as in the first example). Or you can register and enqueue it all at once (as in the second).

What we're doing here is telling WordPress "This is the name of my script / style, here is where to find it, it needs x and y to work, and it's version x. Oh, and by the way, put it in the footer if you wouldn't mind".

This method will ensure that our scripts and styles will automatically be included in the right place, with all their dependencies, and they will be cached properly by WordPress.

* http://codex.wordpress.org/Function_Reference/wp_enqueue_script
* http://codex.wordpress.org/Function_Reference/wp_enqueue_style

---

name: scripts-and-styles-even-better

## This is even better:

Wrap your `wp_enqueue_script` and `wp_enqueue_style` calls in a function, which fires at the right time.

```php
add_action( 'wp_enqueue_scripts', 'my_plugin_enqueue_scripts' ) );

my_plugin_enqueue_scripts() {
	wp_register_script( 'select2', 'ui/select2/select2.min.js', array( 'jquery' ), '3.4.5', true );
	wp_register_style( 'select2', 'ui/select2/select2.css', array(), '3.4.5' );
	
	wp_enqueue_script( 'select2' );
	wp_enqueue_style( 'select2' );
}
```
Or for scripts which are used in the admin area:
```php
add_action( 'admin_enqueue_scripts', 'my_plugin_admin_enqueue_scripts' ) );

my_plugin_admin_enqueue_scripts( $hook ) {
	if ( 'index.php' === $hook ) {
		wp_register_script( 'select2', 'ui/select2/select2.min.js', array( 'jquery' ), '3.4.5', true );
		wp_register_style( 'select2', 'ui/select2/select2.css', array(), '3.4.5' );
		
		wp_enqueue_script( 'select2' );
		wp_enqueue_style( 'select2' );
	}
}
```

???

You should also put these enqueue script lines into their own function, which fires on the `wp_enqueue_scripts` hook.

For scripts and styles which are used in the admin area, use the `admin_enqueue_scripts` hook instead.

It's also a good idea to check if you're on the right page. This will help to avoid conflicts with other plugins.

* http://codex.wordpress.org/Plugin_API/Action_Reference/wp_enqueue_scripts
* http://codex.wordpress.org/Plugin_API/Action_Reference/admin_enqueue_scripts

---

name: ajax
class: center, middle, inverse, inverse-magenta

# AJAX

???

Let's talk about making an ajax call from Javascript. I've seen people create a new file in their plugin or theme to handle AJAX requests, which gets messy quickly.

WordPress has some built in features that make this very easy. There are only three steps involved.

* http://codex.wordpress.org/AJAX_in_Plugins

---

name: ajax-localize

## 3 Step AJAX calls

### Step 1: Localize your script.

```php
add_action( 'wp_enqueue_scripts', 'my_plugin_enqueue_scripts' ) );

my_plugin_enqueue_scripts() {
	wp_enqueue_script( 'my-script', 'ui/main.js', array( 'jquery', 'select2', 'heartbeat' ), 1.0 );

	wp_localize_script(
		'my-script',
		'my_script_object',
		array(
			'ajaxurl' => admin_url( 'admin-ajax.php' ),
			'foo'      => 'bar',
		)
	);
}
```

???

Remember how we enqueued our scripts just now? There's another added bonus to that. We can assign values to our own Javascript global variables from PHP.

This is called localization, because it's typically used to send translatable strings into Javascript. We're going to send WordPress's default ajax handler.

We specify which script it is that this localization applies to, and then we create an object containing the correct ajax url. We can also send other data to our script from here.

If you're in the admin area, ajaxurl is already defined, so you may be able to skip this step entirely.

* http://codex.wordpress.org/Function_Reference/wp_localize_script

---

name: ajax-send

## 3 Step AJAX calls

### Step 2: Make an AJAX call from your Javascript file.

The `ajaxurl` variable is already defined by WordPress if you're in the admin area, and will point to the right place (which is `wp-content/admin-ajax.php`).

```javascript
var data = {
	action: 'my_action',
	whatever: 1234
};

$.post( my_script_object.ajaxurl, data, function( response ) {
	alert( 'Got this from the server: ' + response );
});
```

???

The second step is actually making the AJAX call. A couple of things to note here:
* You must always specify an action (this is used in step 3)
* The `ajaxurl` variable is already defined by WordPress if you're in the admin area

---

name: ajax-recieve

## 3 Step AJAX calls

### Step 3: Receive and return a response.

The request goes to `admin-ajax.php`, which provides an action for you to hook into.

```php
add_action( 'wp_ajax_my_action', 'my_action_callback' );

function my_action_callback() {
	$whatever = intval( $_POST['whatever'] );

	$whatever += 10;

	$success = update_option( 'whatever', $whatever );

	if ( $success ) {
		wp_send_json_success( 'It worked!' );
	} else {
		wp_send_json_error( 'It no work. :(' );
	}
}
```

???

The action name used by PHP here is based on the `action` variable you sent from Javascript.

* http://codex.wordpress.org/Function_Reference/wp_send_json_success
* http://codex.wordpress.org/Function_Reference/wp_send_json_error

---

name: ajax
class: center, middle, inverse, inverse-cyan

# Prefixing

???

This is one that anyone who pastes code can do, no matter what level of skill you have.

It’s a simple concept. Any functions you write have the potential to conflict with a theme, another plugin, or WordPress core itself.

You simply need to make sure your functions have a unique name!

* http://nacin.com/2010/05/11/in-wordpress-prefix-everything/

---

name: coding-standards-kitten
background-image: url(assets/img/coding-standards.jpg)

???

## Coding Standards
### Why Bother?

