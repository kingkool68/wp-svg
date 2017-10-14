Good Morning! Today we're going to talk all about SVGs and how we can work with them in WordPress.

You can follow along with the slides if you want by visiting v.gd/wpsvg

Specifically this talk will cover 1) What SVGs are and how they work 2) Why SVGs are important 3) Icon fonts and why they are bad 4) How we can use SVGs 5) Questions

First things first, here's a little bit about me. My name is Russell Heimlich. During the day I'm the lead developer at Spirited Media, a local news startup. At night I'm a professional toddler chaser/YouTube Kids VJ. 

So what are scalable vector graphics or SVGs?

SVGs are XML based, so they're graphics that are built like HTML under the hood, they're vector based so the graphic can be scaled up or down infinitely without losing any resolution or quality, and SVGs are based on an open standard. Much like how you can view source of a webpage and pick apart the HTML, you can do the same thing with an SVG. You can open it in a text editor, make changes, and save your new creation back out. 

SVGs define points and shapes in relation to one another in space. Which is why you can scale it up infinetly.

What kind of graphics are SVGs are good for? Well, icons, logos, charts, pretty much any ttype of flat, low-color graphic is suitable as an SVG. 

Contrast that with a bitmap graphic. What is a bitmap? A bitmap is a grid of pixel values, will get in to what that means in just a second. Bitmaps are distributed as a binary file format. You can't just open up a bitmap in a text editor to make changes. You would typically use a grahics editing program like Photoshop to make changes to the image. And essentially bitmaps are a "fixed set of dots." 

Jpegs, gifs, tiffs, bmp are all bitmap image formats.

Getting back to that grid of pixel values. Here is a simple example of how bitmaps work. We have two colors, black and white, and the white pixels have a value of 0 and the black pixels have a value of 1. The image on the right is how the pixels are arranged to construct the image on the left. 

The same thing applies to color bitmaps. Instead of a grid of 1's and 0's we have a grid of hexadecimal color values. Bitmaps describe every single pixel in the image. Which is why when you scale bitmaps up they look fuzzy or blurry. Data needs to be interpolated, or guessed, by the computer because there simply isn't a specific value for a pixel. 

What are bitmaps good for? Photos, things with continuous tones and blending of color. 

Here is an example to really drive this home. The tiger growling on the left is best suited as an SVG because it has flat colors and is a line graphic. The image of the tiger growling on the right is a jpeg bitmap to capture all the detail and shading. The image on the right would be much, much, larger as an SVG to represent all that detail.

Now that we have a good idea of what SVGs are and how they compare to bitmaps, why are SVGs important?

The websites we build need to work everywhere the web does. Duh.

Well this is what the web looks like. Different devices, different capabilities, and importantly for graphics, all kinds of different screen sizes and resolutions. The web isn't some sort of fixed, one size fits all medium. 

This multi-screen web of ours puts some constraints on graphics. We need to be aware of different screen sizes where our images will be viewed on, different resolutions like Retina, or HiDPI screens. And we need to be aware of bandwidth constraints. We can't be sending various different sized images down our connections depending on the screen size. 

Graphics need to be as crisp and performant as possible at different sizes. And SVGs are a great format for this.

You might be saying "well we've got icon fonts", what's wrong with that?

Icon fonts are font files that contain graphic symbols instead of letters or numbers. Font awesome is a prime example of an icon font.

Icon fonts are an ugly hack! Within a font we can map a character to a shape. So instead of a 1, we can show a picture of a pumpkin for example.

So what is wrong with them? Well accessibiity issues for one. Font icons use characters that get read aloud by screen readers that offers no context. Many times the character is such a weird and esoteritc unicode character that the screen reader gives up and just says "UNPRONOUNCEABLE". 

Icon fonts can clash with emoji. If a font maps with a character code occupied by an emoji the emoji could overrule.

This happened on Etsy once and became known as the 4 stars and a horse bug. Etsy developers were using an icon font and they wanted to display 4 and half stars but the half star icon occupied the same space as the horse emoji on some systems. Hilarity ensued. 

When icon fonts fail, you're left with empty black squares. Opera Mini famously doesn't render icon fonts which results in something like this on the font awesome page. Also if your font fails to load for whatever reason you'll also run in to this issue.

But icon fonts are so easy for me to use, you might say. Well SVGs can be just as flexible as icon fonts without the downsides.

For further reading about why icon fonts are bad check out "Seriously, don't use icon fonts" and "Ten reasons we switched from an icon font to SVG".

Can we even use SVGs today?

YES! OMG yes we can. 97.88% support globally. If you need to support IE8 and below or Android 2.3 and below then you'll need to worry about fallbacks. Sucks for you. 

Cool. How can we use SVG files, then?

We can point to an SVG using an image element just like any other image format.

Ok. That's nice.

We can also use SVGs as a background image in CSS. We need to specify a width and height and include some off screen text as a sort of pseudo alt attribute for this techniuqe. But you can use SVGs the same way you would use any other image format. 

Not bad. Not bad. 

We can use SVGs like a sprite map. We can group all of our SVGs into one SVG and define it with an ID.

Then to use that SVG in our markup we would reference that ID and our icon would display.

Huh? Ok. That's an idea. 

Finally, we can just embed the SVG we want inline to our markup whever we want it to be used. It is almost just like HTML afterall.

Yea. Ok. I guess. Uh huh.

There are some downsides to each of these techniques. 

If you use an SVG in HTML as an image or in CSS as a background-image you have no control over what is inside the SVG element. And there is a lot of neat things you can do inside of an SVG element. 

With SVG sprites you need to load all of the SVG elements on the page whether you use them or not. Or you can build your SVG sprite dynamically which is a lot of work.

And inline SVG requires a lot of copy and pasting. What if the SVG icon changes? I need to go back and find all of the instances of that SVG icon and replace them.

But loading SVGs inline is awesome. We can treat our icons like any other text element on the page. Like changing the size and color of the icon on hover, for example.

And with just a pinch of CSS we can make our SVG icons take on the font size and color of their parent. If you scale the size of your text up, the SVG icon will scale up proportionaly as well. It will also take on the font color of the surrounding text by default as well.

WOW. Neat, right?

The pros of inlinging SVG are 1) you only use an SVG when you need it 2) No extra HTTP requests are needed like an image element 3) you get control to manipulate stuff inside of the SVG elements 4) they can take on the size and color of the parent element so they can blend in.

But what about all of that copy and pasting? I'll get back to this.

SVGs sound great. I'm convinced. How can I use SVGs in WordPress?

By default WordPress doesn't support SVG files in the media library. You can install a plugin like SVG Support to enable SVGs in the media library. 

Or you can add this snippet to your functions.php if you don't want to use a plugin. And then you can insert SVGs into posts just like any other image format. 

But for you theme designers and plugin developers if you want to inline SVGs easily we can use a handy PHP function. There is a lot of detail in this I want to skip over but the important part is here where we check if the path to the SVG on the server exists and then we tell PHP to open the SVG file, copy the contents of the SVG, clean it up a little bit, and spit out the SVG as a string. 

So I wouldn't use that function by itself, I like to create a little helper function that goes around it to specify a path to a specific directory and some CSS classes we can attach to the SVG. And that looks like this...

When we use the wp_svg_icon function in our templates it looks like this...

And then the final markup that gets read by our visitor's browser looks like this. The SVG is inline, we attach a class to the icon so we can style it if need be. And we specify a role of image to the SVG for accessibility reasons so screen readers don't try and read every element within the SVG.

We can add more icons to this icons directory and then call them with our wp_svg_icon() function just by referencing the name of the file.

And we can make as many helper functions as we want for different kinds of SVGs. I usually make a separate one for logos called wp_svg_logo() for example.

Hopefully this gives you some ideas for how you can work with SVGs in WordPress.

Wrapping up. A few extra resources to help you.

Where can I get SVG icons?

IcoMoon is my go to place for SVG icons. You can build a collection of icons and download them all at once. They have different icon families like Font Awesome.

Icon Pharm is another one

The Noun Project has been around for a long time and they have a bunch of different icons to choose from.

iconmonster is yet another icon search engine.

And Endless Icons is another destination.

Optimizing SVGs. Since SVGs are essentially just text files there are ways to optimize them so they are smaller in file size. There is SVGO which is a command line tool. You point it to your SVG or a folder of SVGs and SVGO will strip out some of the junk you don't need that comes from editors like Adobe Illustrator, it will reduce the decimals becuase SVGs are a lot of math and numbers. By reducing the precision of numbers you can save some file sizes. And there is a user interface version of the tool for those that are command line averse.

Even More resources. Using SVG from CSS-Tricks.com and the Mega List of SVG Information are a goto resource. There's the SVG pocket guide book that is freely available to read online. Or if you want you can, you know, buy a physical book. It comes with unlimited battery life. And Amelia Ballamy-Royds has a ton of SVG examples that she hosts on CodePen. She's an SVG guru. Worth a follow on Twitter.

In Conclusion

Why aren't you using SVGs? Now you can't say you didn't know how

Thank you! You can tweet me @kingkool68

Any questions?




