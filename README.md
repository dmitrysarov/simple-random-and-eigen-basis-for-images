# simple-random-and-eigen-basis-for-images
my experience in variants basis for images.

This little example can help in understanding of images vector space. 
We can consider an image as vector, which dimensionality equal to number of pixels. Let's consider images with just three pixels. Easy to see that simpleast basis for such space (1,0,0), (0,1,0) and (0,0,1), but what if our images lie on one surface or even one line in this space? Then we can transfere to another, more compact basis, for which we can store two (surface) or even one (line) rather three numbers (for each pixel). That's how compression  works.

Another case - we truncate our basis (simply throwing elements of basis - basis vectors). In straightforward case ((1,0,0), ...) we simply will throw pixels, but what will happen in more fitted basis case? In this sketch I tried to cover this questions.

I consider human face images. To form eigen basis I use this database http://vis-www.cs.umass.edu/lfw/. **dataPrepere.py** helps to form **referenceImages.dat** which consist of face images as columns in one matrix (you can grab **referenceImages.dat** here https://goo.gl/2nzNEq). Main file is  **simple_random_eigen_basis.py**.  File **inputImage.dat** consists of examine image separated from the database. 

Then we use simple straightforward basis where only one element equal to 1 and other to 0. Expectedly reconstruction from such image projection gives us the same image.
![figure_1](https://cloud.githubusercontent.com/assets/19648595/26155243/98dfd678-3b23-11e7-9a0e-57b60e7f8a60.png)

If we try to throw basis vector away we will get image without corresponding pixels. This dependence shows how MSE changes corresponding to basis restriction (in random order).

![figure_2](https://cloud.githubusercontent.com/assets/19648595/26155245/98ff2816-3b23-11e7-87f9-ee444b3bee4c.png)

And how image will look like when we leave only 60% of basis vectors.

![figure_3](https://cloud.githubusercontent.com/assets/19648595/26155244/98fa2b9a-3b23-11e7-94b1-82cdc5538ed3.png)

Well, actually instead of this basis we can use any orthonormal basis, for example random orthogonal vectors which norm equal to 1. And then let's restrict basis.

![figure_4](https://cloud.githubusercontent.com/assets/19648595/26155239/98d2a962-3b23-11e7-9e15-d207a39b00a5.png)

MSE grow faster, right? It can be seen on the next pic.
It also remains 60% of basis but for new (random) one. Barely noticeable face.

![figure_5](https://cloud.githubusercontent.com/assets/19648595/26155240/98d4bf0e-3b23-11e7-946c-9a8da286ad2c.png)

And now, the most interesting thing. What if we will choose the most suitable basis for such kind of images. For this purpose I get images of various faces, and get directions (vectors) where such data have the most variance. To read here [PCA](https://en.wikipedia.org/wiki/Principal_component_analysis). Such vectors will be our basis vectors, indeed. Here how they look like, order shows value of variance of data at such directions (vectors), e.g. the first one is the most valuable.

![figure_6](https://cloud.githubusercontent.com/assets/19648595/26155238/98d1f04e-3b23-11e7-83f2-b9759d47f645.png)

Now if I restrict basis, at this time not in random order, but from last vectros, it will be left the most valuable.

![figure_7](https://cloud.githubusercontent.com/assets/19648595/26155241/98d9d1c4-3b23-11e7-9cca-bfa6d85063c2.png)

And check how image will look like if we leave only 20% of basis. The face is still possible to recognize.

![figure_8](https://cloud.githubusercontent.com/assets/19648595/26155242/98db416c-3b23-11e7-8c35-7bb53820a593.png)

That's pretty all.
Thanx for reading. 
