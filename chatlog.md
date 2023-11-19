1.0 : 981e0991dc5e4a29137101f7d08d6080bbb87807
Grace Snow and Chamu on Discord Help.
Question: Semantics / ARIA checkout.
GitHub Repo: https://github.com/Cesar-Moran/stats-preview-challenge

I'm currently building this challenge (https://www.frontendmentor.io/challenges/stats-preview-card-component-8JqbgoU62) and trying to go careful with the semantics and aria elements even if it's not the biggest challenge at all.

I'm currently doubting if it's properly written (the semantics) and also the aria-label attribute in line 28 and 32. I asked myself: What happens if I'm not able to see but hear a screen-reader say this specific text? and then decided that I had to go with the "aria-label" attribute. I don't think it would be appropiate to a visually impaired individual to hear "10K+" instead of "More than 10 thousand." and similar with the "12M+".

Answers Received:
Chamu : aria-label should be associated with an interactive element, check out MDN, https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-label

### I shouldn't be placing aria-labels on elements unless they're interactive elements (like buttons, or any other decorative).

Grace Snow : Nothing in this channel should have aria- on it.

It is fine for screenreader users to hear exactly the same as anyone else for abbreviated text.

Assistive tech users will have their own settings to control how common abbreviations and acronyms are announced

Also, aria is not just for screen readers - it is for the accessibility tree and is used by the whole host of assistive tech out there; And remember that screenreader users are not all blind - those who are hard of hearing, have mobility disabilities, have cognitive or learning disabilities, have speech impairments all use screen readers.

## It is important for accessible names and labels to match what is visible on the screen

#################
The most important things with html semantics are
appropriate use of headings and landmarks
correctly ordered headings
appropriate use of interactive elements
labelling form controls and associating any errors to them
#################

### It's ok for screenreaders to hear exactly the same as anyone else.

### Aria is not for screen readers but for accessibility tree. https://developer.mozilla.org/en-US/docs/Glossary/Accessibility_tree

### Assistive users will have settings to control abbreviations and acronyms.

<!-- ____________________________________________ -->

Grace Snow: In this, you do not have the best html at the moment because

- the component is wrapped in an article for no reason. Luckily this article isnt labelled so it hasn't given the article any extra affordance, but in my opinion there is no reason at all for this to be an article. It would not sit on multiple sites or on multiple pages
- text is inside divs alone instead of using meaningful elements
- unnecessary and confusing aria-labels (these are used on invalid elements too - you can't aria-label a div)

When it comes to writing well structured html imagine the content with no styling. Completely separate it from the design.
Doing that, this component becomes
a heading
a paragraph
a list with 3 bullet points (list items)
an image (as there are two for different screen sizes, the picture element makes most sense)

That's all you need for good accessible html. Don't over-complicate it

### Consider the usage of `article` element.

### Always use meaningful elements. No empty text or similar.

### No aria-labels unless you're pointing up a interactive element.

### Consider using lists more often. You're not using it enough. When you see a group of related stuff, try using a list instead.

<!-- ____________________________________________ -->

Grace Snow: And landmarks @Chamu Aria-label/aria-labelledby is sometimes very important on landmarks (like aside or when a page has extra navigations)

Also fieldset or items with a group role...

The MDN article isnt the clearest about this tbh.

But overall, the important thing for @CiMoran to know is you won't need aria-label often at all

### Also consider using aria-label/aria-labelledby for landmarks, fieldset or items with a group role too.

### We won't often use aria-label at all.

---

Grace Snow: Don't worry about this when you haven't got the design files. Getting it close enough is fine.
With line breaks they should happen naturally based off the max width on the component (well, the space within it)
That max width should be in rem not px as you have currently.
And the h1 should not have margin top. Use padding on main text div instead of margin top on its first child.

Remove the pseudo. That's not how this image effect is meant to be done. Instead make that half of the component have the violet background colour; then use mix-blend-mode multiply and opacity 0.7 on the img

---

Other important bits of feedback
avoid using such complex css selectors. They are a nightmare to read, nightmare to maintain and can cause cascade/specificity issues later on bigger projects. Instead, place classes on what you want to style so you can use single class selectors in css
you don't need to set border radius on the children elements. Place it once on the component along with overflow hidden to crop out the corners of the children that are overflowing it. Much simpler!

### Always use REM for scalable components instead of PX.

### If you want to reach for a certain image effect you can use the `mix-blend-mode` with an overlay element above the image.

### Avoid complex CSS selectors.

### Don't set border radius on children. Do it on the component with overflow hidden to crop the corners. It's a lot more simpler.

#####NOTES#####

In this project, I firstly made the overlay with a pseudo element and re-positioned it above the main image, but I couldn't reach the color goal, which had some kind of darker background.
Apparently, to adapt the image effect a different overlay had to be done. Built a div below the image, then gave it the properties to place it above the image and then for the overlay-effect
The property mix-blend-mode: multiply; worked very well.
