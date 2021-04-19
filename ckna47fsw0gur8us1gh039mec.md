## Vue JS CDN Link - How To Use Vue Without Installing It

There are a few scenarios where you might want to use Vue without installing it. Some examples of such scenarios are:

* learning Vue
* quickly prototyping an application

... and so on. As a result, you can include the Vue JS **CDN link** in your project rather than installing it.

---

# Vue CDN Link
There are two ways to use the Vue with the CDN link. 

If you want to use Vue for **learning purposes** or to **quickly prototype** an application, use the following link:

```
<script src="https://unpkg.com/vue@next"></script>
```

By including the above link in your application, you are using the latest version of Vue.

### Use Vue in production

If you decide to use Vue from a CDN link in production, you should link to a specific version to avoid issues with newer versions of Vue. 

The link should look as follows:

```
<script src="https://unpkg.com/vue@3.0.11"></script>
```

The version number `3.0.11` can be replaced with any version you want, though. 

It's important to note that both the above links use the Vue global file - `vue.global.js` - which is the whole build. That is, it includes the compiler and the runtime.

However, you can use other versions. Check the [dist folder](https://unpkg.com/browse/vue@3.0.11/dist/) to see which versions you can use. For example, you can use only the runtime file - `vue.runtime.global.js` - rather than the entire build.

You can do so by using the following link:

```
<script src="https://unpkg.com/vue@3.0.11/dist/vue.runtime.global.prod.js"></script>
```

---

# Conclusion

These are the two ways you can use Vue without installing it. However, I would recommend installing it through npm or yarn if you want to build a Vue application.

---

After learning how to use Vue without installing it, you might be interested in reading this article - [Learn the fundamentals of Vue JS](https://catalins.tech/learn-the-fundamentals-of-vue-js-with-vue-3)
