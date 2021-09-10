## Center Vertically A Container With A Column Of Flex Items

Figure 1, below, shows how the application looks before centering the content with Flexbox. **What I want to do**, is to center the content section of the web page - that is, everything between the header and footer.

> ![ss1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1618204483319/MBnT31Eme.png)
Figure 1

The second picture, figure 2, illustrates what I want to achieve with Flexboox.

> ![ss2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1618204533353/D3p40g8Cx.png)
Figure 2

# The solution
The solution to achieve the result in figure 2 is to use the Flexbox property `align-items` and set it to `center`. The code snippet below shows how I solved the issue.

```
.main {
  display: flex;
  flex-direction: column;
  align-items: center;
}
```

Below, you can see the full code used for the webpage. The code is from a Vue component, but it's mostly HTML and CSS so it should look somewhat familiar. The only exception is the `<CourseCard/>`, which might look a bit unfamiliar. Think of it as three different divs wrapped inside `.main`.

```
<template>
  <div class="main">
    <h1>Courses</h1>

    <div class="courses">
      <CourseCard
        v-for="(course, index) in courses"
        :key="index"
        :course="course"
        :data-index="index"
      />
    </div>
  </div>
</template>

<style>
.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 50px 0px;
}

.courses {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(3, auto);
  grid-auto-flow: row;
  grid-gap: 10px;
  justify-items: center;
}
</style>
```
