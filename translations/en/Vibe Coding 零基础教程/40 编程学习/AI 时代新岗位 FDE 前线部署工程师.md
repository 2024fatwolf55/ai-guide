# The New AI-Era Role: FDE, the Forward Deployed Engineer

> An AI job paying 70,000 RMB a month, yet on your first day at work you’re sticking QR codes around a factory

Hello, I’m Yupi.

In the AI era, some people feel coding is becoming more and more boring.

In the past, writing one API could take forever. Now you hand the requirement to AI, go grab a glass of water, and it has already generated the code, comments, and tests. It feels amazing at first, but over time, the work starts to feel more and more like a mechanical assembly line: copy requirements, wait for generation, check errors, revise, commit. Hardly any thinking required.

![](https://pic.yupi.icu/1/01_AI%E6%97%B6%E4%BB%A3%E5%86%99%E4%BB%A3%E7%A0%81%E5%8F%98%E6%88%90%E6%B5%81%E6%B0%B4%E7%BA%BF_compressed_v3.png)

So is there a job where you can still do technical work without sitting at your desk all day waiting for requirements?

Yes. And over the past two years, it has become especially hot in the AI industry, with very strong pay. It’s called FDE.

At first glance, many people think FDE stands for Frontend Developer Engineering. But its full name is actually **Forward Deployed Engineer**.

![](https://pic.yupi.icu/1/image-20260807155727082.png)

Simply put, many companies want to use AI to improve efficiency, but they can’t even clearly explain the first step. What problem exactly should be solved? Where should they start? Who will use the final system? They may not have figured any of that out themselves. What an FDE does is go on-site, enter the client’s environment, and turn those vague requirements into a system that can actually go live and be used.

In this article, I’ll walk you through a full FDE delivery process using a fictional project story. You’ll see what this job really looks like, and you’ll also pick up several methods that are very useful for AI applications, such as how to narrow vague requirements into measurable goals and how to build an evaluation set for AI.



## 1. Understand the Client’s Real Goal

Imagine you’ve just joined an AI company, and on your very first project, your mentor assigns you a client: a garment factory that produces suspender pants.

Before the project begins, your mentor takes you and a sales colleague to a meeting at the factory. The production manager, maintenance supervisor, and the person responsible for the factory’s information systems are all there.

The production manager says: we want to build an AI repair-reporting assistant so workers can report machine issues more easily, and maintenance records can be stored properly. Once enough data accumulates, ideally it could even predict when a machine is about to break down.

Your mentor asks: how much machine operation data does the factory currently have?

The meeting room suddenly goes quiet. The maintenance supervisor flips through his notebook and says awkwardly: right now we only have the machine inventory, paper maintenance forms, and chat logs in the work group. We’ve never specifically collected data like temperature, vibration, or operating time.

Without that historical data, AI has no way to learn the patterns that occur before a machine fails, so predictive maintenance is impossible.

So your mentor proposes a new plan: first, streamline the repair-reporting process. Let AI help workers organize repair information while structurally storing each fault description and maintenance result. That solves the current efficiency problem while also accumulating data for future fault prediction.

![](https://pic.yupi.icu/1/02_%25E5%25AE%25A2%25E6%2588%25B7%25E6%2583%25B3%25E5%2581%259A%25E6%2595%2585%25E9%259A%259C%25E9%25A2%2584%25E6%25B5%258B%25E4%25BD%2586%25E6%25B2%25A1%25E6%259C%2589%25E6%2595%25B0%25E6%258D%25AE_compressed_v3.png)

This is the first core responsibility of an FDE: **pull unrealistic requirements back into the range that current data and conditions can actually support.**

Clients often tell you the final outcome they want right away. But as the technical side, you need to judge whether that result can actually be achieved right now. If it can’t, you need to say so clearly and provide an alternative that is feasible today while also paving the way for the future.

At the end of the meeting, the information systems staff adds another requirement: the repair-reporting voice data and maintenance records must stay on the factory’s internal server, and the new system must not directly modify the original data.

So the meeting ends with only one confirmed goal: get the repair-reporting workflow running smoothly first, so workers can report faults faster and maintenance records become more complete. As for how exactly to do it, that won’t be clear until you enter the workshop.



## 2. Go On-Site for Research

The next day, the production manager arranges for Master Wu from Workshop A to show you around. He has worked at the factory for many years. He operates a sewing machine more naturally than you type on a keyboard, and if a machine sounds even slightly off, he can immediately tell.

You follow Master Wu through the entire repair-reporting workflow:

1. When a machine has a problem, the worker first calls the team leader, who then contacts maintenance. The call itself takes only a few seconds, but the fault details must be retold again and again.
2. When maintenance arrives on site, they still need to reconfirm which machine it is, when the issue started, and what the exact symptoms are.
3. After the machine is repaired, the worker still needs to fill out a repair form. Some write it on paper, some post it in the work chat group, and some get busy and forget entirely. The next time a similar fault happens, maintenance has a hard time finding the previous solution from these scattered records.

![](https://pic.yupi.icu/1/03b_%E6%97%A7%E6%8A%A5%E4%BF%AE%E6%B5%81%E7%A8%8B%E7%9A%84%E4%B8%89%E4%B8%AA%E5%8D%A1%E7%82%B9_compressed_v3.png)

After seeing the process, the idea seems clear: the worker speaks into a phone, AI automatically organizes it into a repair form, and then pushes the work order to maintenance. Once the machine is fixed, the maintenance staff record the result through voice or quick options.

The whole process looks like just three steps, not that hard at all.

But as you talk more deeply with Master Wu, you realize it’s not that simple.

The same machine is called “Machine No. 3” by Master Wu, “the old flat machine” by another worker nearby, and “Workshop A Flat Sewing Machine No. 03” in the factory computer system.

If AI can’t even tell which machine the worker is referring to, everything else falls apart. So your mentor tells you to first record all the names workers use for each machine and figure out the mapping between those nicknames and the official IDs.

To your surprise, instead of going back to write code as soon as the project started, you’re standing in the workshop with a notebook, recording machine nicknames.

![](https://pic.yupi.icu/pine/03-ai-%E6%9C%BA%E5%99%A8%E4%B8%89%E7%A7%8D%E5%8F%AB%E6%B3%95.png)

But this exact step leads to an important adjustment in the goal.

Back in the meeting room, the client thought the goal was “use AI to help workers report repairs.” But on-site, it becomes clear that the real bottleneck is the flow of information from workers to maintenance: workers can’t clearly identify the machine, fault descriptions get distorted during retelling, and post-repair records don’t stay preserved.

So the goal is revised to this: workers only need to clearly describe the problem. AI is responsible for organizing the work order, filling in missing information, and helping maintenance find similar past records. As for why the machine broke and how to repair it, that remains the maintenance staff’s judgment.

**This is exactly why FDEs must go on site.** What you hear in a meeting room is what the client thinks the problem is. What you see in the workshop is the real problem.



## 3. Define Measurable Acceptance Criteria

Back in the meeting room, your mentor asks a question: two weeks from now, what exactly do we need to deliver for the client to be satisfied?

You might say: build the AI repair-reporting system and deploy it, right?

But “deploy it” is not an acceptance criterion. The client doesn’t care what you deployed. They care whether workers can report faults faster and whether maintenance records are actually being preserved. Both sides need to agree in advance on concrete numbers. Only then can delivery be considered successful.

So you review the repair records from the past week and find that maintenance staff take an average of more than 6 minutes to receive complete fault information, and after a machine is fixed, fewer than half the tasks leave a recorded result.

Based on that data, you and the client agree on four acceptance metrics:

- Repair information must reach maintenance within 2 minutes, and work orders must no longer be sent to the wrong workshop
- At least 90% of maintenance tasks must leave complete records
- At least 80% of pilot workers must actually use the new process
- The AI’s accuracy in organizing key information must reach 90% before the system can enter workshop trial use

![四个可量化的验收指标](https://pic.yupi.icu/1/04_%E5%9B%9B%E4%B8%AA%E5%8F%AF%E9%87%8F%E5%8C%96%E7%9A%84%E9%AA%8C%E6%94%B6%E6%8C%87%E6%A0%87_compressed_v1.png)

This way of working is actually very enlightening for our own projects too. Whether you’re doing outsourced work or building your own product, if the goal is only “make it,” you’ll never know when it’s really done. But once the goal becomes specific numbers, the direction and priorities instantly become clear.

After confirming the criteria, you and Master Wu first run a test in a quiet office.

Master Wu says into the phone: Machine No. 3 has been making clicking sounds lately.

AI hears every word correctly, but matches the work order to Workshop B. The reason is simple: both workshops have a machine called “Machine No. 3.”

AI understood the Mandarin, but not the factory’s own internal “dialect.”

So you abandon the idea of having AI identify the machine purely from spoken descriptions and switch to putting QR codes on each machine. This is actually very common in manufacturing. Many factory equipment systems rely on scanning codes to identify machines. Workers scan first to confirm the machine, then describe the fault.

After confirming the machine IDs and locations with the information systems staff, and binding each QR code to its machine, you spend an entire day sticking them up one by one around the workshop.

Before joining the job, you thought the FDE tech stack was frontend, backend, data, and AI. After entering the factory, you realize it also includes sticking QR codes.

![](https://pic.yupi.icu/pine/04-ai-%E8%B9%B2%E8%B4%B4%E4%BA%8C%E7%BB%B4%E7%A0%81.png)

It sounds a little funny, but this step captures the value of an FDE perfectly: **when model capability can’t solve a problem, using an engineering workaround is often more effective than stubbornly fighting the model.**



## 4. Build an Evaluation Set

Once QR-code identification solves the “AI can’t tell which machine it is” problem, you feel like the biggest obstacle has been removed.

Your mentor disagrees. He says: if Master Wu says one sentence and AI happens to get it right, that only means you have a demo. To truly meet delivery standards, you need to test hundreds of real repair records and see whether the overall accuracy is high enough.

In the AI industry, this kind of testing is generally called **Evals**. You can think of it as preparing a fixed test set for AI. Every time you adjust the prompt, model, or processing logic, you rerun the same batch of cases and check whether the accuracy has improved.

Evals are a crucial part of AI projects for FDEs. When the client accepts the system, they won’t just watch you demo one or two examples. They want to know the actual accuracy across hundreds of real data points.

So you and the factory’s maintenance supervisor dig out a stack of paper repair forms from the past year. Many sheets are already yellowed and stained with machine oil. The records in the work chat are also messy: some people wrote “needle broke,” some wrote “broken needle,” and some only left “same as last time.”

After two full days, you finally sorted 300 real cases out of that pile of materials.

As expected, the first test round quickly crashes and burns.

What can be heard clearly in an office is not necessarily clear in a workshop. With hundreds of sewing machines running at the same time, the background noise is heavy. AI often mistakes “broken thread” for “power outage,” and “skipped stitches” for “dropped needle.” After all 300 test cases are run, only 81% of the key information is extracted correctly, still far from the 90% acceptance target.

And past maintenance records are hard to search as well. The same fault can be described in multiple ways by different workers, so AI fails to retrieve the truly relevant historical records.

To address these issues, you run several targeted optimization rounds: first add noise reduction at the speech-recognition stage, then supplement a correction dictionary for common workshop expressions, and finally reorganize the paper maintenance forms and group-chat records into a structured database with unified terminology.

After rerunning the full test set, the accuracy rises from 81% to 93%, meeting the acceptance standard.

![评估集跑测试，准确率从 81% 优化到 93%](https://pic.yupi.icu/1/05_%E8%AF%84%E4%BC%B0%E9%9B%86%E8%B7%91%E6%B5%8B%E8%AF%95%E4%BB%8E81%25%E4%BC%98%E5%8C%96%E5%88%B093%25_compressed_v2.png)

And this evaluation set is not something you use once and throw away. After the system really goes live, new failure cases continue to be added to it as the basis for the next round of optimization.



## 5. On-Site Trial and Iteration

Once the evaluation set passes, the system enters a trial in Workshop A. And it fails again.

Although the overall accuracy has reached 93%, there are still 7% of cases where AI gets things wrong. You feel uneasy, so you add a confirmation form to the interface. After the worker speaks, they now have to check the machine name, issue type, and occurrence time that AI filled in, confirm each item, and only then submit.

After swiping through two screens on the page, Master Wu asks you: I used to make a phone call in a few seconds. With your thing, I now have to stare at a whole form?

The client originally wanted to reduce the time workers spend reporting issues and filling out forms, but because you were afraid AI might make mistakes, you added a bunch of extra confirmation steps for workers.

After your mentor hears what happened, he says: 93% accuracy already exceeds the acceptance standard. To guard against that 7% error rate, you’re making 100% of workers operate an entire extra page every single time. That tradeoff doesn’t make sense. It would be better to let AI judge when it is uncertain, and only ask one follow-up question when it lacks confidence. In most cases, it should just submit directly.

![确认表格与 AI 主动追问的对比](https://pic.yupi.icu/1/06_%E7%A1%AE%E8%AE%A4%E8%A1%A8%E6%A0%BC%E4%B8%8EAI%E4%B8%BB%E5%8A%A8%E8%BF%BD%E9%97%AE%E7%9A%84%E5%AF%B9%E6%AF%94_compressed_v1.png)

This is actually a very valuable idea to remember: **when building AI products, don’t make every user pay an extra cost just to cover a small minority of errors.** A better approach is to let AI detect uncertain scenarios itself and interrupt the user only when necessary.

After the redesign, AI only asks one follow-up question when it didn’t hear clearly or key information is missing. And after fixing the machine, maintenance staff can also leave the handling result via quick options or voice input.

During the on-site trial period, you and your mentor report progress every two days to the production manager and sales colleague. During the day, you accompany workers in testing and collect feedback. At night, you go back, revise the system, and rerun the evaluation set.

But coordinating all sides is much harder than writing code. The production manager wants results as quickly as possible, the information systems staff worry the new system may affect normal production, and frontline workers don’t want extra operational steps. All these concerns pull in different directions, and each one has to be addressed clearly before the system has a real chance to be adopted.



## 6. Launch, Acceptance, and Handover

After the two-week pilot ends, acceptance is carried out item by item according to the agreed metrics.

Repair information delivery time is reduced from over 6 minutes to under 2 minutes. Work orders are no longer sent to the wrong workshop. The complete-record rate for maintenance results rises from under half to above 90%. And more than 80% of pilot workers start using the new repair-reporting process.

![上线验收的数据前后对比](https://pic.yupi.icu/1/07b_%E4%B8%8A%E7%BA%BF%E9%AA%8C%E6%94%B6%E7%9A%84%E6%95%B0%E6%8D%AE%E5%89%8D%E5%90%8E%E5%AF%B9%E6%AF%94_compressed_v1.png)

Once the acceptance standards are met, the production manager agrees to roll the system out to other workshops, and the sales colleague uses the acceptance results to continue discussing follow-up cooperation with the client.

But the story still isn’t over. On the second day after the system is rolled out to Workshop B, the maintenance supervisor calls. Workshop B has several special machine models, and the workers there describe faults in completely different terms from Workshop A. AI starts matching things incorrectly again.

So you rush to the site that very day, add a new batch of correction rules, incorporate the failed cases into the evaluation set, rerun the tests, and only then does the system for Workshop B become stable.

An FDE is not like a typical outsourcing team that leaves once delivery is done. If problems arise after the system goes live, you need to get to the client site immediately and solve them yourself.

At the end of the project, your mentor asks you to organize the system’s configuration methods and common issues into documentation, and to walk through the daily maintenance process with the factory’s information systems staff. He says: an FDE cannot leave the client unable to use the system without you. Their own team must be able to take over.

After returning to the company, you bring the lessons from this project back to the product team, including the QR-code binding plan, speech correction methods for noisy workshop environments, and the approach for structurally organizing maintenance records. The product manager decides that the speech-processing capability for noisy environments can become a general module in the product, so other manufacturing clients can use it directly too.



## 7. Is the FDE Role Right for You?

After walking through this entire process, you should now be able to feel the full working loop of an FDE:

1. Confirm the client’s real goal and pull unrealistic demands back within what current conditions can support
2. Follow frontline users through the real process and find the true problems hidden in everyday operations
3. Define the solution and measurable acceptance metrics
4. Build the system and the evaluation set, and validate the results with real data
5. Enter on-site trial use, revise repeatedly based on user feedback, until the system is truly adopted
6. Bring the on-site experience back to the product team so the product becomes better

![FDE 完整工作闭环六步](https://pic.yupi.icu/1/08_FDE%E5%AE%8C%E6%95%B4%E5%B7%A5%E4%BD%9C%E9%97%AD%E7%8E%AF%E5%85%AD%E6%AD%A5_compressed_v1.png)

The specific work of FDEs varies a lot from company to company. Some focus purely on technical delivery, with dedicated people handling business matters. But in many companies, FDEs also participate in pre-sales technical evaluation, and may even help clients discover new AI use cases to drive further cooperation. Some FDEs serve several clients at the same time, while others stay embedded with one client for several months.

But the core is always the same: stand between the client and the technology, and turn vague problems into systems that can go live, be used, and generate business value.

**This job is not easy. In fact, it is highly challenging.**

Current OpenAI FDE roles may require up to 50% travel, and in real projects you may need to stay on-site with a client for weeks or even months. In addition to frontend, backend, and AI application development ability, you also need to be able to break down vague problems, build evaluation methods, handle enterprise-grade system integration and production deployment, and communicate smoothly with the client’s technical leads, business leads, and frontline staff at the same time.



## Final Thoughts

If you enjoy studying real business scenarios, are willing to work with people from different industries, and like personally building systems and watching them get used, then being an FDE can be deeply rewarding.

If you only want to quietly write code, don’t want to travel on-site or deal with vague requirements, then FDE may not be the right fit for you. In that case, steadily learning AI coding and AI application development can still lead you to very good paths.

Whether or not you ever take this role, the methods in this article are worth remembering: confirm the real goal instead of blindly accepting requirements, turn delivery standards into measurable numbers, validate AI with an evaluation set instead of a few demos, and don’t make all users pay to cover a small number of errors.

**These are the truly scarce abilities in the AI era**, because they happen to be the very parts AI still cannot do well.
