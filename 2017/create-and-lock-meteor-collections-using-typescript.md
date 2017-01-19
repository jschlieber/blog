# Create and secure your Meteor collections with TypeScript

This is about how to use the power of static type checking with TypeScript to secure your Meteor collections once and for all. According to [The Meteor Guide](https://guide.meteor.com/security.html#allow-deny) it is recommended to deny all client-side operations on your collections. So let's create a reusable helper that does that.

<script src="https://gist.github.com/jschlieber/ac6a8cd9d8456fdb429caf8db6f78568.js?file=lockCollectionOops.js"></script>

Did you notice it? I've made a horrible mistake there. I used `create` instead of `insert` and `delete` instead of `remove`. I'm just so used to that CRUD term that this naming felt very natural. My Editor silently ignores that mistake.

Seems my collections aren't really locked. Can a user insert and delete documents from the client at will now? Well, no. Thankfully Meteor implemented it's own runtime safeguard in this case. So your Meteor application won't even run but complain: `Error: allow: Invalid key: create`. But what if not? Are there runtime checks for every possible property in every possible function call? No.

## TypeScript to the rescue

Let's implement the same helper with TypeScript. It's a little bit more verbose, but I really like the self documentation of the code.

<script src="https://gist.github.com/jschlieber/ac6a8cd9d8456fdb429caf8db6f78568.js?file=lockCollectionOops.ts"></script>

"What's the real difference now?", you might ask. Let's check our TypeScript enabled Editor.

![lockcollection ts - admin - visual studio code_017](https://cloud.githubusercontent.com/assets/11458212/22119792/364a994c-de7d-11e6-8164-597d1bd73574.png)

It complains that I cannot assign my Object literal to the type `AllowDenyOptions` and my TypeScript file won't compile. That means catching the error before it can happen. That's nothing new for e.g. Java, C++ or C#. But for JavaScript it's a big improvement. There are many cases where JavaScript developers are debugging their code for hours just because of a typo in an Object literal or flipped parameters in a function call. With TypeScript all this belongs to the past. Beautiful!

It's time to correct the mistake and have some beer.

<script src="https://gist.github.com/jschlieber/ac6a8cd9d8456fdb429caf8db6f78568.js?file=lockCollection.ts"></script>

But before we have a beer, let's create another helper that will create locked down Meteor collections for us.

<script src="https://gist.github.com/jschlieber/ac6a8cd9d8456fdb429caf8db6f78568.js?file=createCollection.ts"></script>

Now it's time to have some beers.

<script src="https://gist.github.com/jschlieber/ac6a8cd9d8456fdb429caf8db6f78568.js?file=beers.ts"></script>

Simply beautiful!

Cheers!
