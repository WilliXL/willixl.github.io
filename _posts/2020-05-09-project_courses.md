---
layout: post
title: My Favorite Course Projects
categories: [Projects]
tags: [compilers, machine learning, parallel algorithms, cmu]
comments: true
---

I personally quite enjoy learning maths and theory (still hate taking tests though). I find that working on a difficult problem set is extremely satisfying when you somehow contort your brain in just the right way to reach that epiphany moment. However, theory is not the only thing expected of most computer scientists (unfortunate), especially in industry. Aside from internships, course projects are a great way to learn a bunch of useful things like version control, debugging code that others wrote, and coming to terms with not being able to deliver on a core feature, etc.

As I am turning in my final project of my undergraduate career I thought I'd share some of my favorite course projects I did at CMU.

## Reducing Cache Pollution at Compile Time

Final report [here](../../assets/posts/course_pubs/15-745_Report.pdf).

This is the course project that I just turned in (and my final assignment of undergrad !!) for the course 15-745 Optimizing Compilers for Modern Architectures. My partner and I both had backgrounds in computer architecture so we knew we wanted to do a project related to that.

The core idea here is to use [non-temporal memory instructions](https://docs.oracle.com/cd/E19120-01/open.solaris/817-5477/eptyf/index.html), which write cache lines straight back to main memory, to reduce memory bus traffic during program execution. By removing this bus pressure, we hoped to speed up overall execution time.

The problem with using non-temporal memory instructions naively is that if a piece of data is reused very soon then the instruction would essentially eliminate the entire reason for caching. So our compiler passes needed to figure out when it was suitable and beneficial to use non-temporal memory instructions and modify the assembly accordingly.

## CNN Interpretability

Final report [here](../../assets/posts/course_pubs/10-707_Report.pdf).

For the course 10-707 Topics in Deep Learning, my partner and I went for a more theoretical project idea. The core idea of this project is to expand upon some prior research on CNN interpretability results that used L1-norm part templates to guide the convergence of the convolution kernels towards certain labeled features in an animal recognition dataset. By doing so, a model writer can be sure of what their CNN is actually doing rather than leaving the convergence gradients completely uninterpretable.

The training data was a bunch of different animals with their macro body parts labeled. The goal was to guide the convergence of the network while forcing each kernel to select only for pixels of a certain body part. We discovered benefits and drawbacks of using different geometric norms in the part templates compared to the publication this project was based upon.

## Parallel Galaxy Simulation

Final report [here](../../assets/posts/course_pubs/15-418_Report.pdf).

Galaxy simulation is a very computationally intense thing to do if you are to be 100% precise. It is also difficult to parallelize that process. For the course project in 15-418 Parallel Computer Architecture and Programming we implemented the famous Barnes-Hut algorithm using OpenMP. The uses a quad-tree (or an octree for 3D simulations) and a Hilbert curve to subdivide the simulation space, fill it with stellar bodies, and approximate nearby gravitational forces.

Most of the difficulty in doing parallel galaxy simulation is reducing how much time a process is locking up the tree in order to do its movement edits. So our final approach used a lock-free quad-tree that is able to use atomics at a much finer grain tree depth to prevent locking the entire tree up at the root and killing the parallelization.
