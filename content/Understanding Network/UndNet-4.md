---
title: "UndNet: Week4"
draft: false
---
#### Reading
**Small Power, Big Grid: Part 1**
- transmission v.s. distribution grid
- I like that they pointed out that new technologies (solar cars, smart homes) are directly related to the power grid and might require updates to the system. I always wonder, for basic infrastructure, how companies manage to keep adding distribution to the old system. How do they know there won't be an overload?
- But I guess that's what the author was arguing about? When all these new things add up and people are doing similar things during the same time frame, or the collected energy is resold, the transmission system will need to have a corresponding ability to handle such tasks.
<div align = "center">
<img src = "/media/und/transmission.png" width = 300px>
</div>

[**Bridging the Gap: How Smart Demand Management Can Forestall the AI Energy Crisis**](https://www.goldmansachs.com/what-we-do/goldman-sachs-global-institute/articles/smart-demand-management-can-forestall-the-ai-energy-crisis)
- This flexibility opens the door to "**curtailment programs**," where datacenters run at full throttle for most of the year but are dialed back for a few hours at a time when the grid is under stress.
- "The key question for power companies and infrastructure investors then isn’t just whether to build new power, but also how to bridge the gap until that power comes online. The US power grid is built for peak demand, such as the hottest day of summer when air conditioners strain the system, rather than average demand. This strategy means there is excess slack capacity most of the time."

[**Internet data centers are fueling drive to old power source: Coal**](https://www.washingtonpost.com/business/interactive/2024/data-centers-internet-power-source-coal/)
- Massive data centers with computers processing nearly 70 percent of global digital traffic are gobbling up electricity at a rate officials overseeing the power grid say is unsustainable unless two things happen: Several hundred miles of new transmission lines must be built, slicing through neighborhoods and farms in Virginia and three neighboring states. And antiquated coal-powered electricity plants that had been scheduled to go offline will need to keep running to fuel the increasing need for more power, undermining clean energy goals."
- Once more renewable energy is available, some of the power lines being built to address the energy gap may no longer be needed as the coal plants ultimately shut down, clean energy advocates say — though utility companies contend the extra capacity brought by the lines will always be useful....“Their planning is just about maintaining the status quo,” Tom Rutigliano, a senior advocate for clean energy at the Natural Resources Defense Council, said about PJM. “They do nothing proactive about really trying to get a handle on the future and get ready for it.”
- 

[**Power measurement & management on Chamelon**](https://blog.chameleoncloud.org/posts/power-measurement-and-management-on-chameleon/)
- A bunch of commands


**Network Connections and Colocation Facilities** (Oops this is for nextweek...)
- ISP : Verizon, AT&T...
- Major networks connect through Internet Exchange Points (IXP)
- IXPs are company-owned ***physical network access points***, providing access to a patch panel which connects to other networks. They might own their buildings, or just patch panels in other buildings—such as in a third-party colocation facility.
- transfer data/internet access
<div align = "center">
<img src = "/media/und/infra-1.png" width = 300px>
</div>

- Do IXP facilities looks like this??
<div align = "center">
<img src = "/media/und/infra-2.png" width = 300px>
</div>

- The necessity of a physical connection–whether at a patch panel or access switch–between different networks underscores the often-forgotten tangibility of networks. Although the exchange of bits and bytes can seem abstract–their transfer is only possible through vast physical infrastructure, evident in the windowless buildings filled with conduit, lights, and tubes."
- The conclusion is nice. It reminded me of last semester, when we were talking about the power grid. When it comes to resources that are not that tangible or visible, we often forget the massive infrastructure that goes behind them. It is important to keep reminding ourselves that these resources aren't something that comes easily, but require plenty of people and communities getting involved, putting in effort to build them, or even sacrificing something.

**Fiber Optics**
![[fiber-1.png]]
- Is bandwidth related to the thickness of the fiber optic filaments?
#### Lecture
`nc 10.20.35.169 8080`
`nc -kl 8080`
[netcat (nc)](https://linuxize.com/post/netcat-nc-command-with-examples/)

**histname**
![[packet-9.png]]
tell us whats our address is locally and for the outside work

**Whats ICMP**
portocal behind ping

#### Assignment
Explain how this organization involve the internet society

