# OCR-To-Solve-Linear-Systems
The system works by taking a picture of a set of linear equations and using OCR technology to extract the equations from the images. The system then applies machine learning algorithms to parse and analyze the equations, determining the type of equation and the appropriate method to solve it.


The most difficult part of the problem is getting the matrix's and vector's system. For exemple:

![image.png](attachment:4ead7067-ba78-48d8-9d81-671ab58dbff5.png)
![image.png](attachment:71cd822f-aab3-4f8b-8d47-ccc12eb86802.png)

We can rewrite as:

![image.png](attachment:03fc26dc-c597-4266-b6e7-e03b105722f8.png)

To get these numbers to solve the system, we'll excute two strategies to parser the figure.

Given the exemple image:

![image.png](attachment:71cd822f-aab3-4f8b-8d47-ccc12eb86802.png)

1. First, we'll get the "groups" of the image, that is, for this image, we'll get a cropped image with the x's group (**'9x'** in the image), the signal group (**'+'** in the image), the y's group (**'19y'** in the image), the equal group (**'='** in the image) and the constant group (**'223'** in the image, but it could include a the signal of the number like '-233', if it was '-233' instead '233').

![image.png](attachment:d1b40eef-6ace-4342-a38c-e238310022d7.png)

2. With this groups, we'll parser every group's image to get the "elements" in every group. **For exemple, for the x's group ('9x' in the image), we'll get an image for '9' and one for 'x'**:

    2.1 For the cropped image of the x's group:

      ![image.png](attachment:f51b3771-e942-45ed-8370-6b1090e6c63e.png)
      
    2.2 We'll get the two images:
    
      ![image.png](attachment:bda5d57e-3b62-4d9f-8667-6db1c566dc6e.png)
      ![image.png](attachment:ae13efe3-8646-42f0-8b0f-eb5fb175ccde.png)
      
      
After the image parsing, we can train a model o identify the element's images (we'll utilize a Random Forest, because it's simple problem. But, if the equations were manuscript, we could utilize a Convolutional Neural Network to handle with the complexity):

![Decision Tree.png](attachment:4352255f-9d6d-460b-bae3-1bae78719085.png)

![Decision Tree (3).png](attachment:a92e9c7f-a720-4214-b4f6-1154b1faed19.png)

![Decision Tree (4).png](attachment:60acbeb5-ae64-4a5b-b256-7928361ad4ed.png)


And convert the **original equation image** into a **string** with the model:

 ![image.png](attachment:4ead7067-ba78-48d8-9d81-671ab58dbff5.png)
 
Converting:

<h1><center><b>'20x+7y=249'</b></center></h1>
  

After converting the image into string (**making an Optical Character Recognition - OCR**), we can parser the string with **Regular Expressions** and finally get the system in the matrix form, which can be solved with the numerical numpy solver to linear systems.
