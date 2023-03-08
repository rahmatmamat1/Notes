## Communication and Storytelling

Communication is a big part of a Data Scientist’s job — whether it is technical communication with peers or translating technical concepts to business audiences and stakeholders. The more senior the role, the more influencing you need to do, which all comes down to your storytelling capability. You may be the strongest technical candidate, but you need to clearly articulate why you made certain decisions, identify caveats and limitations, and be concise in your answers, especially when you talk about the impact and route to the value of the work completed. The interview panel eliminated most candidates due to poor or inadequate communication for the level they were interviewing for (from entry-level Graduate Data Scientist to the most senior role of a Principal Data Scientist).

**Recommendations to solve this potential pitfall:** in preparation for the interview, write down the context of the things you highlighted on your resume, why you picked this solution over another, and most importantly, what the impact or outcome was, including whether or not the business implemented your solution. The more you practice with technical and non-technical audiences, the easier it will get. An additional tip for your practice rounds is to change the level of detail, going from executive and high-level summaries to detailed technical deep dives.

Second, take advantage of resources like Toastmasters International, where you can practice public speaking and improve your communication skills or dive into the great content published by the likes of TED Talks. I’m not affiliated with or sponsored by either organization.

## Company and Business Understanding

As Data Scientist, your job is to create real solutions that help advance the business. This means either enhancing or optimizing a process, identifying new opportunities for growth and innovation, or more altruistically leaving the world a better place (e.g., as Mars Petcare, one of our objectives is to create a better world for pets). Since these are your objectives as Data Scientist, it is critical to understand the fundamentals of the company you are interviewing for. In addition to not being able to connect with the interviewing panel about the problems that matter the most to them, how will you know if this position is the right fit for you as you progress in your career? How will you be able to ask meaningful questions and engage with the interviewer? Also, candidates who didn’t have any questions to ask at the end of an interview, not a single one, ended up not making it to the offer stage. I’m not saying this was the reason. Still, it appears like a strong indicator of having some basic understanding and curiosity about the business, its challenges, and how you, as a Data Scientist, are expected to support it.

**Recommendations to solve this potential pitfall**: to stand out, you need to invest some time to understand the company you are interviewing for, including its primary purpose and positioning in the market, source of revenue, and significant competitors. As you advance in your interview process, continue to dedicate more time to discovering the company. This investment will allow you to better connect with the interviewer and enable you to understand if this is a suitable workplace. Regarding resources, start with the corporate website to get a feel for the brand and what it stands for. Look for some financial information through the investor relations section or other publically available resources, including Wikipedia or Yahoo Finance. Seeing the environment where the product or service is being sold could also lead to some significant observations and talking points during the interview — for instance, going to a retail store, or browsing the eCommerce website. Lastly, your Linkedin network could be a more utilized resource. Reach out to your first and second-degree contacts, convey your interest in the firm, and ask for 15 minutes of their time to learn more. Yes, you will be rejected or not replied to, but in the end, you only need one or two chats to distinguish yourself from other candidates.

## Two more things that kept getting high marks from the interview panel

* **Demonstrating you have a keen sense for identifying pragmatic solutions and a strong product sense**: this would, for instance, come through you demonstrating a strong focus on the impact and outcome of the work rather than the work itself. I talk about the importance of product sense here, in case you want to learn more.
* **Be your authentic self, and don’t assume anything in the conversation**: ask clarifying questions when needed, as this will provide a good insight into how you will engage and speak with senior and executive stakeholders.

## Conclusion

Where we work and what we do most of our day are so important. Your preparation will set you apart from other candidates, especially in how you communicate, tell your story, and demonstrate your grasp of the company. Ultimately, the hiring manager will decide whether he trusts you to do the following — the more senior, the higher the required trust.

As the hiring manager, I ask myself whether I can trust the candidate to:
1. complete an assignment
2. solve a problem
3. work well with others to solve a problem
4. figure out which are the correct problems to solve
5. inspire other people to solve the correct problems




## Interview structure

I actually did not apply myself, instead a recruiter reached out via LinkedIn. This is a good reminder to keep your LinkedIn profile polished and up-to-date. I did one phone screen and one virtual on-site:

-   The phone screen lasted for one hour and included two coding questions.
-   The virtual onsite was spread over 2 days. Day 1 included one coding interview, one behavior interview, and two design rounds: system design and ML system design. Day 2 included originally one coding round and one behavior round, but the latter was canceled in the last minute, so I ended up just doing a single coding round on Day 2.

## The coding interviews

I did in total 3 coding rounds, one in the phone screen and 2 during onsite. Each coding round had 2 Leetcode Medium questions that I needed to solve in around 1 hour, resulting in a total of 6 coding problems. Typically one interview had one very common question (within the Leetcode top-10 Facebook-tagged questions) and one more obscure question (within the top-300).

I practiced by studying the most frequent Facebook-tagged questions from the past 6 months on Leetcode (this functionality is a good reason for purchasing Leetcode Premium). Instead of quantity, I focused on quality: I tried to really understanding the different approaches to solve the most common questions, and why the different approaches worked, and why my first attempts did not work. Overall I practiced 137 / 350 Leetcode questions.

👉 A few tips:

-   **Communicate your thought process clearly**. Practice this during prep by talking to yourself as you solve problems. Drive the conversation. Make it as easy as possible for the interviewer. The outline shouldn’t be a surprise any more: (1) confirm you’re understanding the problem correctly with a few test cases, (2) describe the algorithm and complexity at a high level, (3) implement, and (4) test.
-   **Find your own bugs.** It’s ok if your code has bugs as long as you’re able to catch them yourself. After you’re done with the code, always run the algorithm by hand line-by-line with a test case. In at least 2 of my interview problems I found bugs in my code, but there was no time left to fix them. That was ok.
-   **Bias for speed.** If, during (2), you have the option between implementing a sub-optimal solution or brainstorming about a more optimal solution, I’d bias for speed and write the sub-optimal solution first. It’s much better to have a complete solution that’s not optimal than no solution at all. In at least one question I knew (and communicated) that my solution was not optimal, and that was ok.
-   **Take notes while studying.** During preparation, I found it useful to take notes in a simple markdown file. I created my own ‘curriculum’ with the most important questions and solution descriptions which I edited and refined over time. This helped me keep all the important questions in one place.
-   **Purchase Leetcode Premium**. It’s extremely useful to be able to see the most frequent questions being asked at the company you’re interviewing with.

## The design interviews

There are 2 design rounds, system design and ML system design. The system design interview is about how to solve a problem with a distributed system, and the ML design interview is about how to solve a problem with ML, such as how to build a classification system or a recommender system. Here is the prep material that I recommend:

-   Educative’s ‘[Grokking the system design interview](https://www.educative.io/courses/grokking-the-system-design-interview)’. While overall extremely useful, this course is also a mixed bag: some lessons are high-quality, others not so much (perhaps because different lessons are written by different authors). I focused more on learning the fundamental components such as REST API, load balancing, communication models, etc, instead of memorizing the design of particular systems.
-   Educative’s ‘[Grokking the Machine Learning Interview](https://www.educative.io/courses/grokking-the-machine-learning-interview)’. This course is also a mixed bag, some lessons are excellent and others not so much, but overall it is a great introduction to ML systems design.
-   Alex Xu’s system design YouTube channel, [ByteByteGo](https://www.youtube.com/c/ByteByteGo).
-   Chip Huyen’s “[Designing Machine Learning Systems](https://www.oreilly.com/library/view/designing-machine-learning/9781098107956/)” book. If you don’t want to purchase the book, check out her [website](https://huyenchip.com/machine-learning-systems-design/toc.html), which contains much of the same content that’s covered in the book.
-   My own e-book, “Machine Learning on the Ground: Design and Operations of Real-World ML Applications”, available on [Gumroad](https://samflender.gumroad.com/l/mlontheground). This book is a collection of articles on ML design and operations that I’ve been writing over the past few years, aggregated as a single, 50-page pdf.
-   Research papers: a great resource that I often consult is Eugene Yan’s [list of curated papers](https://applyingml.com/papers/). In particular, here are a few papers that I found insightful:

[Amazon Search: The Joy of Ranking Products](https://assets.amazon.science/89/cd/34289f1f4d25b5857d776bdf04d5/amazon-search-the-joy-of-ranking-products.pdf)  
[Deep Natural Language Processing for LinkedIn Search Systems  
](https://arxiv.org/pdf/2108.08252.pdf)[Embedding-based Retrieval in Facebook Search  
](https://arxiv.org/pdf/2006.11632.pdf)[Deep learning for recommender systems: A Netflix case study  
](https://ojs.aaai.org/index.php/aimagazine/article/view/18140)[Wide & Deep Learning for Recommender Systems  
](http://wide%20%26%20deep%20learning%20for%20recommender%20systems/)[Deep Neural Networks for YouTube Recommendations  
](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/45530.pdf)[Neural Collaborative Filtering](https://arxiv.org/abs/1708.05031)  
[150 Successful Machine Learning Models: 6 Lessons Learned at Booking.com](https://booking.ai/150-successful-machine-learning-models-6-lessons-learned-at-booking-com-681e09107bec)

👉 A few tips:

-   **Drive the conversation**. If you wait for the interviewer to drive the conversation it simply shows a lack of initiative, and you always want to show the opposite: that you are driven and take the initiative. You should be speaking most of the time. The rough outline for both design rounds is as follows: (1) clarify the problem, (2) propose a high-level design, (3) draw out the design (it’s always boxes and arrows), (4) zoom into certain components of the design.
-   **Practice drawing**. Prior to the interview practice drawing a few design diagrams on [Excalidraw](https://excalidraw.com/). This will make it a bit easier during the interview: if you can save a few seconds of figuring out how to draw a circle, that’s a few seconds more you can spend on brainstorming.
-   **Take notes as you study**. During prep, always take notes about what you’ve learned. Don’t just copy-paste, write things in your own words as a way to probe your understanding.

## The behavior interview

I had one behavior round during the virtual onsite, which lasted for 1 hour. Here are the questions I prepared for:

-   What project are you most proud of?
-   How did you handle conflict / disagreement with a colleague?
-   Tell me me about a time when you took initiative.
-   Tell me about a time where you started collaboration across teams.
-   Tell me about a time when you had competing priorities.
-   Tell me about a time when business requirements changed and you had to adapt.
-   Tell me about a time you accepted feedback from your manager.
-   Tell me about a time when the problem you were solving was ambiguous.

👉 A few tips:

-   **Follow the STAR method:** **S**ituation / **T**ask: what’s the problem, **A**ction: what initiative did you take? what was your reasoning? how did you convince others?, **R**esult: for example, “I improved business metric X by Y%”, “I resolved the bug which impacted N customers”, etc.
-   **Take a moment to think before answering**. That’s ok. You’re not a machine.
-   **Re-use**. It’s ok to use the same situation for multiple questions, and highlight a different facet of the situation.
-   **Exaggerate within reason**. It’s ok to exaggerate, as long as there’s a grain of truth to your story (otherwise you won’t be able to answer probing questions). The point is not so much to obtain a historical record of what really happened, but instead the interviewer wants to know what your personal values are.
-   **Write**. Prepare your stories by writing them down. It’s also ok to have them in front of you during the interview as a reminder (just don’t read them off the screen).

![](https://miro.medium.com/v2/resize:fit:700/1*Rr5-Qy06zo2ciKbozaHGQQ.png)

A long journey: visualization of my Leetcode submissions. (Image by the author)

## Final thoughts

My overall impression with Meta’s interview process is that it is fair. I was clearly told from the beginning what to prepare for and what to expect. The experience was very much like preparing for an exam in school. To be clear, this is a lot of material to cover. I personally spent several months on Leetcode alone, as you can see in the screenshot above.

That being said, tech interviews also include a significant component of luck. It is possible that with the same amount of preparation I would have failed with a different set of interviewers and questions, in the same way that a neural network arrives at different potential minima with different random seeds. That’s why I’d generally recommend to interview with not just one, but several companies at the same time, depending on how much spare time you have available.

Lastly, if there’s only one thing I want you to take away about interviewing, it’s this: **be driven and show initiative from the moment you start that call**. Don’t wait for the interviewer to instruct you what to do next, but steer the conversation yourself. Say things like “_next, I’m going to zoom into how the labels are being generated. Is that ok_?”, instead of “_what should I do next?_”. As an individual contributor in an organization you are expected to have an initiative towards solving problems, and the interview setting, in particular the design round, is a great opportunity for you to show that initiative.