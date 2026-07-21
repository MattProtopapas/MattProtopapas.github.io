Generally speaking there are 3 kind of decisions: *strategic*, *tactical* and *operational* (day-to-day).

Data & Analytics have been useful to all of them, but with a varying degree of value.

To explain these types of decisions, I’ll use an example from football.

Let’s suppose we have a football team.

The owners of the team have to make the long-term decisions that will impact the future of the team in the next season and beyond. Setting the vision of where they want the team to be several years from now, who to hire as a coach, what budget to allocate for players, etc. These are strategic decisions.

The coach of the team makes the tactical decisions. They decide which players to start with in the next game, if the team is going to play 4-4-2, 3-5-2, or whatever, they make substitutions during the game, etc. These decisions have a mid-term horizon.

The players make the operational decisions, during play. Whether to pass the ball, or dribble, how to position themselves in order to help the team score or defend, when to shoot, etc. These decisions are short-term (typically within a single phase of a match).

This of course is a simplified example. Where I come from, it is not uncommon to see the owner of the team dictating to the coach who he should select for starting in the next match, or even getting down to the pitch to complain to the referee for their decision. But that’s not necessary to consider for understanding data-driven decision making.

### So in which types of decisions have Data & Analytics provided the most?

Actually it’s not strategic decisions as one might expect. While strategy has -by its definition- the most value as it determines to a large extend the future of the organization, setting a vision and making those complex decisions require more than simply analyzing data. So, while there are many pieces to the puzzle of strategic decision making, and most of them require a solid understanding of what’s involved - analytics provide a key impact there- it’s synthesis that makes a strategy. The decision makers must combine the insights from the data & analytics regarding the current -and potential future- state of both the company and the market, with their deep understanding of the business landscape to set a realistic vision and set the broad guidelines to make it happen. So analytics, while being extremely helpful to analyze the individual elements of strategic decisions, play a supportive role to the overall decision making itself.

It is actually tactical decision making, where analytical models have played a key role. In all aspects of business management, be it Finance, Marketing or Operations, analytical tools exist to provide insights on what has happened, why, how things might evolve, and what would be the appropriate response of the business. Numerous examples exist: marketing mix & customer acquisition / attribution / churn etc. models. Risk management, portfolio management, and financial models . Demand forecasting, inventory optimization, and production planning. And more…

In tactical decision making, data & analytics can help the decision maker end-to-end, from understanding the current state of affairs and the root causes, to making near-optimal decisions.

When it comes to operational decision making, analytics always help. Fraud detection has always been useful for banks and credit card companies, next-best-action models have always helped customer service agents, and inventory monitoring has always been key on retaining customers while optimizing costs at the same time.

There are however, many simple operational decisions a company has to make, where the impact of analytics to the bottom line is limited, as the impact of such decisions is limited. Also, there might be easier ways to make good decisions on those matters, that do not require that much of analysis.

For example, understanding which orders have been invoiced does not necessarily require the construction of a data warehouse to consolidate all the data produced from all the company’s processes in all their systems. Neither they require advanced mathematical concepts. Reconciling information from their ERP and perhaps some other operational system, using simple business rules, would most probably do the trick.

### Operational Decisions are easier for AI

That’s why operational decisions have been either made automatically through code that incorporated a fixed set of business rules, or manually, from company employees who simply knew what needed to be done through their experience and training.

In my view, that’s where AI could offer its most potential. By simplifying the code that would be implemented to set up that automation, or to save employees time - who have definitely more productive and creative things to do, than reconciling invoices and order information.

They are also rather simple decisions, at least in comparison to the intricacies of tactical decisions, or even more, to the broader understanding and visionary capabilities required for strategic decision making.

We would expect (and need) to see some great business impact on the day-to-day company operations, from AI, for it to be considered a viable and useful tool to decision making.

There have been important successes in such grounds. Companies like Amazon and Netflix have been using recommendation engines for quite some time, to suggest items (and shows) of potential interest to their users. Companies like Uber have been experimenting with reinforcement learning for dynamic prices during surge times. And more..

### But what about tactical decisions?

That's where analytics have been providing the most value. And while many attempts have been made to delegate such decisions to AI bots, there are important problems. 

First of all the AI bots and agents do not understand business context. The terminology, and information structure inherent in a company, has not been available in any LLM training set, as it is proprietary. To solve this problem, what is sometimes called a *semantic layer* is implemented, to 'translate' the business meaning to something the LLM's can understand.

This has allowed us to create *Analytical AI chatbots* (and also agents) that can reply to analytical questions the decision makers make in natural language. This way, a stakeholder can ask 'how many XYZ gadgets did we sell last month' and get an accurate answer. Furthermore, this kind of bots & agents can create visuals and perhaps even dashboards from a set of simple prompts, stated in natural language, from the company data.

However, we're still not there, when it comes to complex thinking and decision making at a tactical level, directly from an AI agent.

### ... productivity?

Another area where AI tools can help is on building analytical capabilities. Every data warehouse or pipeline that automatically populates it with data from source operational systems, is in effect, build using code. The same is true more or less for reports & dashboards, and definitely for advanced analytics and machine learning models. AI can help a lot when building such analytical capabilities. Productivity increases of > 10x are not uncommon. 

### Good practices are paramount

We’re still in the early days of applied AI, and much is going to be done so that companies get a clear assessment of how AI tools can be effective and the business community to have a clear set of effective practices on leveraging AI to make better business decisions. 

Some are already established. Even before the AI era. For example, data & code quality control has always been important - even more important when our code is generated by an AI tool. The good news is that we can implement a series of diverse automatic tests (unit tests, integration tests, etc.) using AI tools to help us set up the code for these tests as well. The important thing is to follow a meaningful Software Development Process.

Another good practice that many practitioners agree, is that it's better to use AI to write code for an analysis or a dashboard, instead of 'asking it' to do the analysis from scratch every time. This way you control the process better, you don't risk by moving potentially sensitive information to the LLM servers (which might even be outside the continent), and you save money on tokens.

Another effective practice is to use the semantic layer I've mentioned when building AI chatbots that need to provide sensible answers to business questions. An LLM that directly refers to the underlying data model is generally not able to translate the business terms directly into SQL queries, by using only the information provided in a database schema. The results would be that the chatbot would not be able to provide an answer, or even worse, to hallucinate an answer that looks plausible but has no sense whatsoever.


We’ll all be following those trends - and some of us even affecting them - of course, as the potential value looks quite promising. But we should never forget the saying: ‘if you only have a hammer, everything looks like a nail’.

Effective decision making has always had to do with being able to distinguish fact from hype, value from loss, and opportunity from risk. And those have always been human qualities, and in business decisions an extensive amount of relevant expertise is essential.