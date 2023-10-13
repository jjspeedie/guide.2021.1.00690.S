#  Introduction

This is a small sample book to give you a feel for how book content is
structured.
It shows off a few of the major file types, as well as some sample content.
It does not go in-depth into any particular topic - check out [the Jupyter Book documentation](https://jupyterbook.org) for more information.

Check out the content pages bundled with this sample book to see more.

```{tip}
My advice is to write your own implementation of the type of solver
you'll be using for your research once, even if you don't use it
for your actual work.

The process of figuring out how to organize and write the code
will demystify a lot of what takes place in a modern simulation code.
```

$$
a(x, t=0) = \left \{ \begin{array}{ll} 0 & \mbox{if } x < \frac{1}{3}\\
                                       1 & \mbox{if } \frac{1}{3} \le x < \frac{2}{3} \\
                                       0 & \mbox{if } x \ge \frac{2}{3}
                                       \end{array} \right .
$$

any initial profile $a(\xi)$ is simply advected to the right (for $u > 0$) at a velocity $u$.

<!-- ```{tableofcontents}
``` -->
