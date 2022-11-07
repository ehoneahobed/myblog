# AirBnB Clone Webstatic Project - Challenges & Lessons learned


This is the second part of the AirBnB project that students in the ALX software engineering program and Holberton school have to undertake.

If you are yet to check out the [part one](https://blog.ehoneahobed.com/alx-airbnb-clone-the-console-project), do check it out because I explained what the project was about and the various parts to that project.

This part involves creating the frontend of the AirBnB website using HTML and CSS. We were given various tasks to solve and pictures of what the finished tasks should look like.

I have publish the outcome of this project on GitHub pages, you can check it out with this link: [AirBnB webstatic project](https://ehoneahobed.github.io/airBnB_clone_Webstatic/)

Below are images of showing the progress I made working on the project.

![airbnb_clone1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1667662901290/8gPli8Sbh.png align="left")


![airbnb_clone_code.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1667662943630/8WfEGtEnL.png align="left")


![airbnb_clone2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1667663005267/HLSeC0GGK.png align="left")


![airbnb_clone6.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1667663099004/jek3DcFQw.png align="left")

After completing the initial design, I had to optimize it for mobile responsiveness and accessibility. Here are some images of when I was working on the responsiveness.


![airbnb_clone4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1667663238309/JnSUBGHuX.png align="left")


![airbnb_clone3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1667663356739/YQYS5qGKK.png align="left")


![airbnb_clone5.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1667663374683/Ynev55SkY.png align="left")

## Challenges faced during the project
1. We were limited to the various HTML tags that we could use. This means that you are given a set of HTML tags and an expected output for you to build it. We were allowed to use any kind of CSS styling.                                                                                          
Personally, the biggest challenge that I faced was not being able to use the HTML img tag but being asked to put some images on the webpage. Initially, I did that by creating empty paragraph tags and using CSS to set the background of those tags to the respective images.                                                                                                                     
Unfortunately, that solution wasn't scalable and distorted the alignments of some of the texts. I struggled to make them work but eventually, I realized that they weren't an optimal solution for the task.                                                                                                                       I did a lot of online searches and eventually got an idea. The new idea was to use the `before` pseudo-element to set the image as a content before the text. This worked perfectly.                                                                                                                                         I have therefore created a codepen to show how that can be achieved. You can check it out with this link: [Add images using CSS without the HTML img tag](https://codepen.io/ehoneahobed/pen/eYKdprj)

2. Centering text within a circle. On a number of occasions, I have seen people tweet about how even experienced programmers sometimes find it difficult to center a `div`. I usually laugh it off thinking that it wasn't true. During this project, I was supposed to have center text in a circle and that was really tough from the beginning.                                               This text was in a div and I used the `border` and `border-radius` properties to create the circle. To place the text at the center of the circle became a problem. This is because `paddings` and `margins` when used disturbed the orientation of some other elements on the page.                                                                                                                                              I later found that you can easily do that with the `text-align` and `line-height` property. Check the link below for a sample that I have created on Codepen: [How to center text in a circle](https://codepen.io/ehoneahobed/pen/PoaGqvY) 

3. Creating layouts with CSS can be a headache if you don't really understand various layout properties that you have at your disposal. I just to go with `CSS flexbox` and this project taught me a lot of things that I either didn't know or didn't understand much. I may challenge myself to also use `CSS grid` for the layout at my leisure time.                                    Two things (main axis and cross axis) is very important and not understanding them in the context of flexbox is the foundation for laying out your site. You should also know which of the flex properties aligns to the main axis and which aligns to the cross axis.

4. I didn't know (or had forgotten) how to add a favicon to a website. One Google search gave me the answer though.

## Lessons Learned from the project
- Stackoverflow is a lifesaver
- Trying to explain exactly what you are doing whiles coding can help you to easily debug the code when something isn't working the way you want it.
- You are likely to forget a lot of the things you are learning today but the important thing to remember is knowing where to get the information whenever you need them. This is one of the major reasons why I am always motivated to document the things I do so that if I forget them tomorrow, I will always have a place to find them.


## Conclusion
I enjoyed working on this project and became so excited when I completed it. The reason for the joy was that when I started I was wondering how I was going to build something like this with all the restrictions.

I am therefore happy that I was eventually able to come up with solutions to all the tasks. If you are a student at ALX or Holberton and yet to do this project, brace yourself for the challenges I mentioned here and get ready to fight them with all your might.

I'd love to get your feedback on this. Comment your thoughts and if you have already done this project, share your challenges or lessons learned in the comments. 

You can connect with me on [Twitter](https://ehoneahobed.com/twitter). If you love the content I put out and would love to support me:
- Follow this blog (@ehoneahobed) and subscribe to my [YouTube channel](https://youtube.com/@ehoneahobed) to show me that love. 