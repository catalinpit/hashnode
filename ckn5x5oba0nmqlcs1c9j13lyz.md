## Canonical URL - What Is It And Why Should You Care

The canonical URL is vital when you publish the same content on multiple platforms. The problem is not many people are aware, and they hurt their SEO.

Before going into the nitty-gritty, let's start with an elementary example. Let's say you publish the same article on three platforms. Without a canonical URL, search engines see your content as duplicate, and it becomes confused:
* which article should I index?
* to which article should I sent traffic?
* which one is the original article?

If you do not specify the canonical URL, search engines choose randomly between the links, and your pieces of content might compete between themselves. Also, if the search engines see duplicate content, it might penalise your website!

**So, what?** You might ask. If you have a preferred platform or a blog, you want the article from that platform/blog to get all the SEO! You do not want to split it with the other platforms or, even worse, get nothing. **Thus, canonical URL helps with that!**

## What is a canonical URL?
A canonical link is an HTML element - `rel=canonical` - that specifies the original source of an article; or the preferred version of the article. The canonical URL tells search engines which version to index and send the SEO juice to.

A canonical URL looks as follows:

```
<link rel="canonical" href="https://catalins.tech/10-programming-project-ideas-for-beginners">
```

Of course, the `href` value is different for each case, depending on your article. Working with the same example, if I re-publish the same article on other blogging platforms, I need to use this URL - from my blog
![Copy of Cream, Pink and Purple Brushstrokes Musician Collection YouTube Thumbnail.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1617707265812/WVTmX3jKp.png)
 As a result, I avoid confusing search engines and getting penalised. It also ensures that I get all the SEO benefits.

## How to use the canonical URL
Thankfully, you do not have to add all the HTML when you re-publish your content on other platforms. 

Most platforms *(if not all of them)* need the original article URL, and they set the canonical tag automatically to the link provided by you.

> ![chrome-capture (1).jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1617706391372/Y6H3mVBx5.jpeg)

The figure above shows an example from Hashnode. You simply add the article URL and Hashnode (and other platforms) do the rest.

## What do you need to remember
Before going, I want to reinforce the following ideas in your mind:

1. If you publish the same piece of content on multiple platforms, use a canonical URL.
2. The canonical link should be the link to your preferred platform (e.g. your blog).
3. Canonical URLs help to consolidate page ranking to your preferred URL.
4. Using a canonical, you get all the SEO benefits.
5. If you do not use a canonical, search engines see duplicate content and might penalise you.

## Further reading
[Source 1](https://yoast.com/rel-canonical/), [Source 2](https://developers.google.com/search/docs/advanced/crawling/consolidate-duplicate-urls), [Source 3](https://yoast.com/duplicate-content/)