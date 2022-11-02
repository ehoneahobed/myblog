# ALX AirBnB Clone - The Console Project: Challenges & Lessons learned

One of the major projects that students in the ALX Software Engineering program and Holberton School are requested to undertake is **cloning of the AIrBnB website**.

This happens to be the first web development related project. The project is, however, divided into different sub-projects which include:

- AirBnB Clone - The Console
- AirBnB Clone - Web static
- AirBnB Clone - MySQL
- AirBnB Clone - Deploy static
- AirBnB Clone - Web framework
- AirBnB Clone - RESTful API
- AirBnB Clone - Web Dynamic

As you can see this project is a very comprehensive one but we have just started with the very first one and that's what I want to share with you. Let's get into it then.

## How we tackled the project
At ALX, most of our projects are broken into tasks. For this project, we had about 18 different tasks to solve. The good thing about these tasks is that they break down the whole project into smaller parts and you only need to worry about one task at a time.

Also, since the tasks provide prompts for you to follow, it becomes quite easy to implement sometimes.

The project was a seven-day project and required a team of two members. I paired up with a very good friend of mine for the project.

We started off by reading the concept  pages and brainstorming how we were going to approach the project. We finally decided to meet on a daily basis for as many hours as we could possibly have at or disposal to work on it.

Since, I had previous web development experience, it came in handy when we started the project. I was able to anticipate what will be required of us. We started solving them task by task.

The very first few tasks were easy going. For some of them we didn't have previous knowledge on them so we had to check online to find resources that could explain them to us. One particular one that I can remember is "How to use the UUID module in python".

At the end of each task, we used the test cases that were provided to check our codes to make sure that we were getting the required output.

During the project some of the tasks become very challenging and this was because we had done everything as we were asked too but still getting some errors (output different from the required one). Unfortunately, we couldn't pinpoint where the errors where coming from.

The interesting thing about what was happening was that prior to that step it was working fine and we didn't know exactly what we changed that caused the problem. But we had made a lot of changes along the line so if we wanted to figure it out then we needed to undo all the changes.

Can you imagine getting to task 15 and realizing that what you had working after task 5 is no longer working that same way and you needed to find a way to correct it?

It was very very frustrating. Eventually, I had to revert to the commit for task 5 and track the changes that I have made through to task 15. Unfortunately, I realized that I didn't commit my code after task 5 but rather after task 6.

The task 6 however was still showing the same error so I reverted to the commit for task 4 and started task 5 all over again. Unfortunately, I got the same error after solving it again. Meanwhile, it wasn't so the first time I solved it.

> That was when I learned the lesson of committing your codes as often as possible

Tasks 15 and 16 took us more than 2 days to solve. We moved from one error to the other. We spent a lot of time debugging, searching Google and also watching videos to help us resolve the errors.

> One particular error that kept us wandering for long was the issue of **"partially imported module due to circular import"**

Finally, we got around it but after the checker (the software ALX uses to mark our projects) was released, a lot more frustration set in. Our working code was now not getting or checked for various requirement checks. Funny enough, we just could't figure out which requirements we were missing.

With less than 4 hours to the deadline, we realize that we misnamed one of our directories (tests_modules instead of test_modules) and had to make some of our test scripts executable.

In our quest to getting everything checked we get changing things and that experience wasn't good at all. Frustration at it peak.

Now let's take a look at the actual project and what it entails.

## Breakdown of the AirBnB Clone - The Console Project
I have always maintained that you can solve a problem that you don't understand. Even though prompts in the form of tasks were provided for us to solve and help us build the project, it was going to be difficult for one to successfully get through it without understanding what it entailed.

This means, that you have to start by finding out exactly how the AirBnB website work and what they required to build it, what users can or cannot do on their website and many more.

Take a quick look at the [AirBnB](https://airbnb.com) website and see what they do before you begin your project.

I have broken the whole project into 4 major parts. These are:
- The backend
- The frontend
- Storage
- Testing

Before the end of this project, I held a live session upon the request of some iKrate Community SWE members. In the live session, I walked them through all these parts, how they work together and how they should approach each of them.

Here is a video recording of the live session.

%[https://youtu.be/P1cNeo-0ioM]

Let me try to explain in brief what each of the parts entails.

### The backend
This involves application of python OOP programming. It means to be able to tackle this, you need to know about the various OOP concepts which include but not limited to:
- Classes
- Objects
- Class and Instance attributes
- Methods
- Inheritance

You will also need to know how to work with Python packages and modules especially how to import a module and use it.

Two modules that we required for the project include:
- UUID module
- Datetime module

That means you need to learn about these two modules and how to use them.

In the project, you are required to build a base model class from which all the other backend related classes will inherit from. The other classes that you will be required to build include:
- User
- City
- State
- Amenity
- Place
- Review

If you have checked out the AirBnB website, you will realize that these are important things relating to their website and reflects what end users can do with their website.

For example, users can sign up which should be handled by your User class. They may leave reviews, others can list places. To list a Place you will have to indicate the State and the amenities that are available at your place.

So, essentially, your backend should be able to handle all those actions.

### The frontend
Your work wouldn't be useful if no user can interact with it unless reaching directly into your code. For that matter we require an interface for users to be able to communicate with our backend.

In this project we were asked to use the **CMD module in python** since we are yet to learn HTML, CSS and Javascript (the technologies for building frontend during web development).

You therefore need to read on the CMD module and learn how you can use it to build a simple interface for your project. I showed how to go about this during the live session, you you can watch it to see how to use it.

One resource that helped me learn about this module and be able to use it is the [PyMOTHW website](https://pymotw.com/3/cmd/). Check it out for yourself.

### Storage
Another important aspect of every web development project is storage of data. Ideally, you are supposed to make use of a database for such purposes. But in our case, we were yet to learn about databases so we were tasked to store our data in a JSON file.

To be able to do this, you need to learn about the **JSON Module** available in Python.

As part of using this module in the project, you need to learn about serialization and deserialization of python objects. I also explained these in the live session so do check the video out.

There were a few challenges that most of us faced working with the JSON module but then I cover some of the common ones during the live session showing how I overcame those challenges.

One key thing that eluded most people with regards to solving the storage part of the project was **knowing exactly how that part integrated with the other parts**.

It took me the effort of trying to use the same logic from this project on a different project to appreciate exactly how they worked together.


## Challenges
- It was difficult to appreciate why certain things were being done the way they were. You were told what to do but had no idea how to do it. This made it difficult to debug the code if something is not working the way you expect it.

- Collaborating with a remote team member can be challenging when both of you have challenges with network connectivity and electricity power outages.

- We tried to use VS code live sharing extension to enable us code together but we had a lot of set backs due to internet connectivity

- Having a good tool for remote collaboration is great but finding that tool can be challenging if you aren't experienced with them yet. We started off with Google meet for our meetings but we had a lot of challenges with it. We then switched to Telegram video call but that also didn't help matters. Eventually, I created a private telegram group that we used for livestreaming (only the two of us were on the call though). It looks like all these were so because we were struggling with internet connectivity.

## Lessons Learned
1. Sleep or enough rest can be the cure to the programmers worry. Sleep when you have too. Get some rest when you have tried severally and it isn't working. Come back to it after you are well rested and see how magical it can be. During one of the nights, I wanted to finish a certain number of tasks but this particular error was keeping me awake for nothing and I couldn't proceed without solving it. I sat on it for hours and eventually got tired and went to bed. I solved the problem in less than 5 minutes the following morning.

2. When coding, try to commit your code as often as you can. You never know when you will need to revert to a particular commit. What I took out of this project is that, anytime I try anything and find out that it is working, I have to commit that.

3. You get to learn better if you task yourself to explain concepts you think you know to others.

4. We made a conscious effort to learn how to use the Pull request feature in GitHub for our collaboration. So anytime any of us committed our code to GitHub, we had to send a Pull Request for the other to review before merging it to the main branch. This taught us a lot about working with branches in Git. If you are new to git and GitHub, you can check out my [explanatory article](https://blog.ehoneahobed.com/git-git-commands-github-explained-for-dummies) on them.

## Conclusion
I wish I could keep going and share with you all the little details but I don't have all the time and I believe that this will be a good read for you if you are yet to go through this project.

I keep writing these things to document my journey and serve as a reminder to me about how far I have come while also motivating others who are on their way. If you enjoy this and would like to connect with me, send me a DM on [Twitter @ehoneahobed](https://ehoneahobed.com/twitter).

You can also support me to keep publishing content by showing me love through following me here on my blog and subscribing to my [YouTube channel](https://youtube.com/@ehoneahobed)