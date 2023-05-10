
I’ve written about how to use web components with Angular Elements, but I think the discussion about web components goes a lot deeper than just how to use them. Web components provide a standardized way to export components and functionality across web platforms. In the last article, we created a contact form using Angular Elements and saw just how easy it is to integrate them into a website. It could be said that this is the exact same kind of thing an iFrame would have been used for. In this article, I want to discuss these two technologies, how they differ, where they’re similar, and what the future may hold for them both.

What is an iFrame?
In short, an iFrame is an HTML document embedded inside another HTML document. You’ve probably come across loads of different kinds of iFrames even if you weren’t fully aware of it. The humble iFrame has been around since the late 90s and was first introduced by Microsoft. It became the standard for embedding one site inside another for decades. Today we still see a boatload of sites using iFrames. The reason for that is that no one had really come up with something better! There was no real way to do what an iFrame does and make it completely cross-platform.

At its core, an iFrame isn’t truly embedding anything in any website. It merely provides a window to view another website. There are a number of issues that come along with that.

The first issue is that the iFrame will not look like it’s meant to be there. It looks out of place as you could have two sites with very large style differences and if you use an iFrame in one to link to the other then it’s going to look weird. Your iFrame also has to be of a fixed width and length and it can be difficult to properly position it on a site that makes it look more natural.

The second issue is the performance impact of an iFrame. Since you’re embedding another site the client still needs to load all that content. If the owner of the site you’re embedding does a bad job your site will also suffer as a result. This comes from the issue of not being able to defer an iFrame like you could a script tag.

The third issue is a security issue. Literally, you could take any site and embed it as an iFrame with only the link to the site. This presents an issue like any open window would in your home. Since your site is communicating with another site that opens up a security hole. If the site you’re embedding has a security issue then so does yours.

What are Web Components
Web components are literally custom components you can use anywhere. Rather than using the Microsoft-created iFrame tag Web Components allow you to make your own custom tag. You can even export web components as NPM packages if you so choose.

So at a high level, iFrames and web components seem pretty similar. I can tell you they are worlds different. While an iFrame is basically a window into another website a web component is literally a single component that can be used by the consumer. Unlike an iFrame, you can’t just make anything into a Web Component. Web components are based around modern web standards and are a set of APIs that allow you to embed components into a website using an HTML tag.

Web components seem to solve all the problems that iFrames have. Let’s look at them one at a time. The first issue I brought up was the look at feel. Since web components are literally just simple components like a button, an input field, or a whole form, they are small enough to be designed to look more homogenous with the site they’re used on. Also, depending on how you make the component, it can inherit certain attributes (like text style) from the parent site while maintaining its own styling that is more explicit. What does that mean? Using text style as an example, if your style sheet does not specify a font it will use the font of the parent site. That gives a really smooth transition in a website from the native website to a web component. A user would have no idea they’re interacting with a web component.

Thinking about performance you import a web component using a script tag. Unlike an iFrame, you can defer a script tag. The defer keyword waits until a site is loaded and then runs the script. This means that the web component, even if it’s large, will not block the initial render. Since we’re not loading 2 websites the packages will generally be smaller as well. That’s not to say there is no performance impact, but it’s negligible.

The third issue is security. I mentioned earlier that you can’t just take any website and embed it as a web component. Using web components is more like installing an NPM package because they can also be NPM packages. So security certainly isn’t perfect, but it’s going to be a whole lot better than using an iFrame. If you want to use a web component you can use API keys to secure it, that does mean a lot more work but security is worth it.

If you’re interested in how to make a web component I have a whole article about that here: Using Web Components in Angular.

So What?
This is the question, so what? Will web components make the iFrame a relic of the past? The simple answer is, I sure hope so! I see a bright future for web components and I hope part of that future is making iFrames outdated. You can do pretty much everything an iFrame does but better. The only thing iFrames can do is easily and quickly embed one website in another one. In today’s day and age, I don’t see that as a good thing. I see iFrames as security and performance holes. However, I do not see iFrames going away soon, unfortunately (no matter how much I want them to). Any time there is a new technology, which web components aren’t really new, but they’re coming back around, adoption takes time. It takes time to become popular and more widely used. Until we start using web components more often I don’t think we’ll see it phase out iFrames any time soon.

Let me know what you think in the comments I’d be interested to hear what you guys think about web components vs iFrames.

