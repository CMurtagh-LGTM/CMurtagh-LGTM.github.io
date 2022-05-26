---
layout: post
title: "A Note on 3b1b Complex Numbers In Discrete Math"
date: 2022-05-24
katex: yes
categories: 3b1b Mathematics Fourier Group
---

## 3b1b's video

I recommend first watching the 3b1b video for some context.

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/bOXCLR3Wric" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

In 3b1b's latest video at the timestamp 17:23 3b1b notes that the complex trick is secretly a Fourier transform.
This made me, a student currently studying Fourier analysis, wonder what is this Fourier transform doing here.
For the past week I've been looking into more generalised Fourier transforms on groups after stumbling on Pontryagin duality.

## The Groups at play

Firstly I lay down what group is underpinning the problem at hand.

As we are dealing with divisibility by \\(5\\) the first group that came to my mind is the \\(5\\) cyclic group.
\\[\mathbb{Z}_5=\mathbb{Z}/5\mathbb{Z}=\\{0,1,2,3,4\\}\\]
Were the element \\(0\\) denotes our desired divisibility by \\(5\\) and
each other element denotes a number in the original problem that has a remainder when divided by \\(5\\).

I also note this is isomorphic to \\(\\{e^{2\pi i\frac{k}{5}}\\}_{k=0}^{4}\\), which is the complex numbers 3b1b was talking about.

Now we need a dual group and Haar measure for \\(\mathbb{Z}_5\\), after a quick but confusing look at [wikipedia](https://wikipedia.org/wiki/Pontryagin_duality),
I found that \\(\hat{\mathbb{Z}}_5=\mathbb{Z}_5\\) and the measure we're dealing with is just the counting measure.

But what *are* dual groups and what *is* the counting measure.
The counting measure is simple it's just the cardinality of the set.
Well, from someone who just discovered this, a dual group is isomorphic to the group of homomorphisms from the original
group to the complex plain.

I then decided to convince myself of this dual group.
A good target group is \\(T=\\{e^{2\pi i\frac{k}{5}}\\}_{k=0}^{4}\\) with multiplication, as it is isomorphic to \\(\mathbb{Z}_5\\).
For ease of writing let \\(\zeta_k=e^{2\pi i\frac{k}{5}}\\), \\(\zeta_0=\zeta_5=1\\) and \\(w(x)=e^{2\pi i\frac{x}{5}}\\)
Now I can define some homomorphisms

|     | 0 | 1 | 2 | 3 | 4 | T |
|-----|---|---|---|---|---|--:|
| \\(h_0\\) | \\(\zeta_0\\) | \\(\zeta_0\\) | \\(\zeta_0\\) | \\(\zeta_0\\) | \\(\zeta_0\\) | w(0) = w(5x) |
| \\(h_1\\) | \\(\zeta_0\\) | \\(\zeta_1\\) | \\(\zeta_2\\) | \\(\zeta_3\\) | \\(\zeta_4\\) | w(x)  |
| \\(h_2\\) | \\(\zeta_0\\) | \\(\zeta_2\\) | \\(\zeta_4\\) | \\(\zeta_1\\) | \\(\zeta_3\\) | w(2x) |
| \\(h_3\\) | \\(\zeta_0\\) | \\(\zeta_3\\) | \\(\zeta_1\\) | \\(\zeta_4\\) | \\(\zeta_2\\) | w(3x) |
| \\(h_4\\) | \\(\zeta_0\\) | \\(\zeta_4\\) | \\(\zeta_3\\) | \\(\zeta_2\\) | \\(\zeta_1\\) | w(4x) |

## Lets Fourier these Groups

I need to define \\(L^2(\mathbb{Z}_5)\\).
Starting with the inner product \\(\langle a, b\rangle = \int_0^4 a(n)\hat{b}(n)dn = \sum_0^4a(n)b(n)\\)
I then can define the norm for a function \\(f:\mathbb{Z}_5\to\mathbb{R}\\) by \\(\|f\|^2 = \sqrt{\sum_0^4f^2(n)}\\).
Now clearly any function \\(f:\mathbb{Z}_5\to\mathbb{R}\in L^2{\mathbb{Z}_5}\\).

Now the Fourier transform of \\(f\\) is \\(\sum_0^4f(n)h_n(\xi)\\), with \\(\xi \in \mathbb{Z}_5\\).

## The Problem from the Video

From the video I redefined the problem as, finding \\(c_0\\) from the sequence \\(s=\\{c_0, c_1, c_2, c_3, c_4\\}\\)
where \\(c_n\\) is the number of subsets with remainder \\(n\\).

Then I take the Fourier series of \\(s\\).
* \\(\mathcal{F}(s)(0) = c_0 + c_1 + c_2 + c_3 + c_4\\)
* \\(\mathcal{F}(s)(1) = c_0 + c_1\zeta_1 + c_2\zeta_2 + c_3\zeta_3 + c_4\zeta_4\\)
* \\(\mathcal{F}(s)(2) = c_0 + c_1\zeta_2 + c_2\zeta_4 + c_3\zeta_1 + c_4\zeta_3\\)
* \\(\mathcal{F}(s)(3) = c_0 + c_1\zeta_3 + c_2\zeta_1 + c_3\zeta_4 + c_4\zeta_2\\)
* \\(\mathcal{F}(s)(4) = c_0 + c_1\zeta_4 + c_2\zeta_3 + c_3\zeta_2 + c_4\zeta_1\\)

I stole from the video that \\(c_0+c_1+c_2+c_3+c_4=2^{2000}\\).
Due to the cyclic nature of \\(\zeta_k\\), \\((\mathcal{F}(s)(k))^5=\mathcal{F}(s)(0)\\) for \\(k\in\\{1,2,3,4\\}\\)
and as the answer is going to be real \\(=2^{400}\\), just like the video.

Then I did an inverse Fourier series \\(s^\prime=\frac{1}{5}\sum_0^4\mathcal{F}(s)(n)\zeta_n\\).
Note that the \\(\frac{1}{5}\\) comes from normalising the basis.
As there are cognate pairs I simplified this to \\(s^\prime = \frac{1}{5}(\mathcal{F}(s)(0) + \sum_1^4\mathcal{F}(s)(n)\cos(\frac{2\pi n}{5}))\\).

So I found an alternate proof that gives us \\(c_0 = s(0) = s^\prime(0) = \frac{1}{5}(2^{2000}+4*2^{400})\\).

## The Note from the Title

I'm going to focus on subsets of \\(\\{1,2,3,4,5\\}\\) with Fourier series \\(s_5^\prime\\).

In the video 3b1b uses the generating polynomial \\((1+\zeta)(1+\zeta^2)(1+\zeta^3)(1+\zeta^4)(1+\zeta^5)\\)
and claims that the power refers to the elements of the set.
In the video is expanded to \\(1+x+x^2+2x^3+2x^4+3x^5+3x^6+3x^7+3x^8+4x^9+4x^{10}+2x^{11}+2x^{12}+x^{13}+x^{14}+x^{15}\\)
and it claimed that the powers refer to the sums of the subsets.
I had the idea that we should also apply modular arithmetic to the powers as we only care about remainders when dividing by \\(5\\).
\\[8+6x+6x^2+6x^3+6x^4\\]
We can see that the coefficients of these polynomial correspond to \\(s_5\\).

So the note is that we can expand and simplify large polynomial, mod something, using Fourier analysis.

Now that I've done it, it seems very mundane, but that's the way with mathematics anything that you can prove will seem mundane to you.
At least it does for me.

## Some Thoughts

In Fourier analysis we usually have a time domain and a frequency, or for physics (I think) position and momentum.
Here we have some sort of counting domain and some other domain, I honestly don't know and if you have any ideas my email is in the footer.

For \\(s^\prime\\) we can actually have this definition on \\([0,5]\subset\mathbb{R}\\) with
\\(\|s^\prime\|_{L^2(\mathbb{Z}\_5)}=\|s^\prime\|\_{L^2[0,5]}\\).
This conversion to continuous fails when we reapply reality \\(s_5^\prime(1.5)=5.5056\ldots\\),
is not zero as we can't have a non-integer remainder.
We also extend the binomial coefficients to a continuous function as well which has some similarities.
This also gives an alternate interpolation to using the cardinal sine function.

