#The High Cost of Low-Friction Infrastructure#

The impact that cloud computing is having on technology organizations is undeniable. It's allowing companies to move at an unprecedented speed, churning out infrastructure as effortlessly as pushing a button in a Jenkins job. Gone are the days of counting infrastructure delivery time in quarters. Now the timescale is in minutes.  While the agony of endless change gates for hardware has been applauded by most of us in the industry, our zeal for the speed gained has left us unaware of what's been lost. There are no perfect systems. **Everything** comes with a cost.

##Systems Aren't Always Code##

When we talk about Systems design in technology, we're often discussing some computer-to-computer or computer-to-human interactions. But in-between these sophisticated transactions lies the original system, two-humans directly interacting with each other. (Albeit that interaction is increasingly becoming digital as well)

These systems exist as approval processes, peer review and the often vilified meeting. These human touch points however serve as *signals* within the human system. If you make a purchase order request for new hardware, that signals to the operations group that something within the organization has changed. Are we expecting an increase in demand? Has a new project started? Questions begin to flow, the human network does its thing and people begin to interpret the *signal* and take action. More than a handful of organizations have processes that are initiated as a result of these signals, to ensure broad involvement, risk assessment and impact. 

In the world of the cloud though, many organizations haven't thought through their human systems and where these gated signals will now come from. An engineer can spin-up a system, make a DNS entry, share a link and have a "production" system up and running before lunch. A self contained team has all the tools necessary to go to production. It's a blessing if you've accounted for it and a curse if you haven't. 

[Conway's Law](https://en.wikipedia.org/Conways_Law) has often been used as a cautionary tale. What we fail to realize however is how often a company uses Conway's law as a control mechanism for certain actions. By creating a barrier between systems, development and design, you've forced an interaction that improves communication. The quality of that communication is debatable, but the fact that it exists at all is a win in this context. I'm not arguing whether that limiter is good or bad, but your organization has to understand where and by what degree it **depends** on that limiter.  How does the security organization become aware of new instances? 

Who is responsible for patching those instances? Monitoring them? These questions are typically birthed at the point of that forced interaction. Could the team deploying the system ask and answer these questions internally? Absolutely. And often they do. But that is **extremely** company dependent and comes with its own set of challenges that are outside the scope of this post. 

The issues I have outlined all have workable solutions, but you can't solve a problem unless you're aware it exists. Be honest about your gates and checkpoints. You wouldn't have added them unless they provided some value. Maybe that value has been over or under estimated, but the move to the cloud is a great time to re-asses them.

##Do More With More##

Something I've always found ironically hilarious in the virtual server space is why it came about and where we're at now. Tech organizations saw all this underutilized hardware and thought virtual machines would be able to help address this and save cost. Now the industry has loads of under-utilized virtual machines on over-subscribed hardware. If you find yourself in this situation, the move to the cloud may not offer much relief.

During the days of gated hardware acquisition, there was a certain pain that went with ordering a server. Forms, inquiries from management, meetings and just a bit of your soul were all common prices to pay as someone rolling out new hardware. As a result, there was a sort of self-preservation like preference on using hardware your team already had. With the cloud, that friction is removed, making it easier and more attractive to simply spin-up a new server. There's value to that. A tidy separation of concerns, isolation for maintenance and a performance profile that is inline with your application's needs. 

The rub comes in when this mode of thinking becomes institutionalized. Before long, it's habit that every application gets its own set of servers. But does that make sense for every solution? If billing and marketing have an internal-only application, does it make sense for each of them to have their own server? And then if they've got one, they have to have two right? (Redundancy and all) What is the cost of a 30 person unit sitting on 4 servers? You may have hidden that cost in VMWare, but in the cloud it comes front and center.

There's that old economic principle, the [law of demand](https://en.wikipedia.org/wiki/Law_of_demand). As the price of a good reaches 0, demand becomes infinite. While the price of cloud computing is nowhere near zero, organizations have effectively removed the purchaser of the good from the consequence of that good's cost. We've trivialized the acquisition process to the point where need and want are synonymous. If you're not careful, you can quickly fail to deliver on the promise of cheaper infrastructure using the cloud. 

##Conclusion##

I bring up the topics above not as a deterrent to the cloud, but as a warning. Adopting the cloud isn't just about speed of delivery, but about a shift in how your organization thinks about the technology life cycle. There are no free lunches. With speed comes some added risk. Is it worth the payoff? Every company has to decide that for themselves. But a healthy dose of organizational pragmatism is good "one-size fits all" advice.
