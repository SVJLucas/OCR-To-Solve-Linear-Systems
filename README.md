# Optical Character Recognition (OCR) To Solve Linear Systems
The system works by taking the images of a set of linear equations and using Optical Character Recognition (OCR) technology to extract the equations from the images. The system then applies machine learning algorithms to parse and analyze the equations, determining the type of equation and the appropriate method to solve it.

# Contextualizing the Problem


Given two images of linear equations, as below:


![first_equation](https://user-images.githubusercontent.com/60625769/228858278-75710929-2cde-41f6-ac97-ce3b653445ec.png)

![second_equation](https://user-images.githubusercontent.com/60625769/228858312-d1bdbd65-b03c-4fc3-8bc3-7824459080a0.png)


We must construct a model that solves the system and gives us:

![output](https://user-images.githubusercontent.com/60625769/228867273-ba16c141-7344-469c-aead-25927e5eed38.png)


# Strategy to Solve the Problem

The most difficult part of the problem is getting the matrix's and vector's system. For exemple:

![first_equation](https://user-images.githubusercontent.com/60625769/228858278-75710929-2cde-41f6-ac97-ce3b653445ec.png)

![second_equation](https://user-images.githubusercontent.com/60625769/228858312-d1bdbd65-b03c-4fc3-8bc3-7824459080a0.png)

We can rewrite as:


![system](https://user-images.githubusercontent.com/60625769/228858412-318d59fe-1521-4dac-bd43-ea7dc1e58eee.png)




To get these numbers to solve the system, we'll excute two strategies to parser the figure.

Given the exemple image:


![second_equation](https://user-images.githubusercontent.com/60625769/228858711-68587e1f-0456-4968-99a7-ef9935ab92d5.png)



1. First, we'll get the "groups" of the image, that is, for this image, we'll get a cropped image with the x's group (**'9x'** in the image), the signal group (**'+'** in the image), the y's group (**'19y'** in the image), the equal group (**'='** in the image) and the constant group (**'223'** in the image, but it could include a the signal of the number like '-233', if it was '-233' instead '233').


![group_image](https://user-images.githubusercontent.com/60625769/228858782-da691325-5b18-4383-a0f6-e8f6417039ae.png)


2. With this groups, we'll parser every group's image to get the "elements" in every group. **For exemple, for the x's group ('9x' in the image), we'll get an image for '9' and one for 'x'**:

    2.1 For the cropped image of the x's group:

      
      
      ![xgroup](https://user-images.githubusercontent.com/60625769/228858907-2cb54896-83ff-411c-8228-7f2d18fe00a1.png)

      
    2.2 We'll get the two images:
    

      ![nine](https://user-images.githubusercontent.com/60625769/228858978-13d9e1cf-b187-4291-a495-be659f9091b3.png)
      ![x](https://user-images.githubusercontent.com/60625769/228859073-42beec79-2fe9-4afb-9379-2eb5fd5c49db.png)
       

      
      
After the image parsing, we can train a model o identify the element's images (we'll utilize a Random Forest, because it's simple problem. But, if the equations were manuscript, we could utilize a Convolutional Neural Network to handle with the complexity):


![rf_nine](https://user-images.githubusercontent.com/60625769/228859397-dbe1095f-1502-40f4-b4c6-c0fb9369c48b.png)

![rf_x](https://user-images.githubusercontent.com/60625769/228859423-8311b9e3-aba9-4cee-b1f3-0c15991f9426.png)

![rf_plus](https://user-images.githubusercontent.com/60625769/228859461-7dcb40ee-ef91-4f34-bef2-6673b5697b54.png)

And convert the **original equation image** into a **string** with the model:

![first_equation](https://user-images.githubusercontent.com/60625769/228859680-7211c94e-e7ab-49e7-bc83-945cf1e92023.png)

Converting:

<h3>     '20x+7y=249'</h3>

After converting the image into string (**making an Optical Character Recognition - OCR**), we can parser the string with **Regular Expressions** and finally get the system in the matrix form, which can be solved with the numerical numpy solver to linear systems.
