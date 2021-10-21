# DAO - Decentralized Autonomous Organizations

“If you want to go fast, go alone.
If you want to go far, go together.”

– African proverb.

## Manage and Scale a DAO

### Soft Skills

Decentralization doesn’t just have smart contracts. DAO are about people, and thus soft skills are essential. Jono Bacon has written the best book on community management called [“The Art of Community”](https://www.amazon.com/Art-Community-Building-New-Participation/dp/1449312063){target=\_blank}. It is HIGHLY recommended to read. A great way to get the soft skills to manage a DAO is to join a meetup and perhaps co-organize an event. You can find Ethereum meetups with like-minded individuals around the world via the [ConsenSys BUDIL Network](https://www.meetup.com/pro/BUIDL/){target=\_blank}. In addition, you can become a valued member of a community by joining the ConsenSys Discord.

Another way is by joining a project like [AirSwap](https://www.airswap.io/){target=\_blank}! AirSwap is dedicated to creating tools for frictionless trade. They have an excellent governance system and need devs like you! [Join their Discord](https://chat.airswap.io/){target=\_blank} and check out their roadmap. If NFTs are your thing, check out [Megaliths](https://www.metaliths.com/){target=\_blank}. Or check out the DAOs on DAOHaus.

DAOs also need clear lines of communication, transparency of information, and an inclusive governance structure. This means a transparent voting process and consensus making mechanism.

### Code of Conduct

Along with a mission statement, a Code of Conduct is a must. A great one that can be built off is the [Berlin Code of Conduct](https://berlincodeofconduct.org/){target=\_blank} which is open source, modifiable and extensible. A code of conduct is a MUST.

As groups start to scale, there will inevitably be issues with certain members. Remarkably, most people are chill, and you can set the tone very easily by having clear expectations written in a code of conduct. The clearer your rules are, the easier it is to collaborate.

### Governance Structure

Decentralization means clear governance structures. Luckily we have some [prior history with specific DeFi projects](https://www.gemini.com/cryptopedia/defi-solutions-decentralized-governance-meaning){target=\_blank} from which we can learn. For example, yearn Finance, Synthetix, Compound Finance and MakerDAO have great governance models worth studying.

![dao-flow.png](../../img/S06/dao-flow.png)

### Improvement Process

The improvement process is the method by which projects like Ethereum, protocols and DAO manage change.

There are typically three types of proposals. Improvement proposals involve adding, removing, or improving some code, to the project or adjusting to governance. This could be adding a new feature for members or users. Configuration proposals involve adjusting variables in smart contracts, say the collateralization ratio. Finally, meta proposals involve proposals around the improvement process itself.

The general process for creating a proposal is:

#### Discussion

Discussions start informally via chat platforms, online forums and meetings. Eventually, the ideas begin to coalesce into something tangible. The next move could be a temperature check, where a quick poll can gauge support said idea. During this process, the ideas are refined as they are still in a nascent stage.

It is interesting to note that Discord and chat platforms, in general, are great for creating community building, brainstorming and getting immediate feedback. However, due to a chat platform's UX/UI, they are NOT a great place to host binding votes or establish long-form conversations.

Discourse allows for long-form threads, which allow for more well thought out conversations. However, this comes at the cost of a lack of immediacy in response. Discourse can also be configured to be found on search engines, which help with attracting potential members.

Some Discourse forums are more technically focused on catering to their audiences, like [Ethresear.ch](https://ethresear.ch/){target=\_blank} or [research.synthetix.io](https://research.synthetix.io/categories){target=\_blank}. Others are more informal. Tailor it to suit your needs. Side note, you can customize your Discourse template to make it more UX/UI friendly and organized. That effort will go a long way.

#### Write up of Improvement Proposal

Once the idea has been discussed, a draft is created. There are various tags for proposals. The general gist of these are:

**Draft** - still in draft stage

**Review** - finalized and open for further community input. It can go back to the draft stage.

**Submitted** - staged to go through the proposal process. The voting period is set.

**Pending Vote** - in vote stage

**Accepted** - went through with a number of votes needed

**Rejected** - rejected. Back to the drawing boards or abandoned

**Completed** - Team has implemented the proposal

There can be other tags like **On Roadmap**. Again, you can customize these as your community sees fit.

#### Voting

Usually, voting occurs with a governance token. This corresponds to 1 token = 1 vote. Although this may seem unfair, it is the only method known to prevent Sybil attacks. Perhaps once the industry figures out how to use decentralized identities, we can see more typical voting forms.

The leading DeFi Protocols use Snapshot as their tool of choice to avoid gas fees. However, as Layer 2 solutions begin to roll out in 2021 and onward, we shall see more on-chain voting as a result. For example, Aragon is already looking to roll out Optimism.

There are several issues with voting. One is low turnout and engagement. This plagues many protocols and DAOs as users wish to get the financial upside without commensurate voting. As a result, some protocols are turning to using vote boosting and locking mechanisms like [veCRV](https://resources.curve.fi/faq/vote-locking-boost){target=\_blank} from Curve and [oSUSHI](https://forum.sushi.com/t/sushinomics-introducing-osushi/4055){target=\_blank}.

The reason is twofold. First, it helps reduce the dumping pressure from tokens by restricting supply and locking tokens up. Second, it gives an earning and/or voting boost to long term stakers who are more engaged. This works well with inflationary tokens as it subtly transfers value from passive and inactive participants to more active members.

Another technique to deal with voter apathy is vote delegation. Some protocols allow token holders to delegate their votes to a representative. One version of this is [liquid democracy](https://medium.com/@memetic007/liquid-democracy-9cf7a4cb7f){target=\_blank}. Adressen Horowitz, which has several billion-dollar funds to invest in crypto, has a great post on [designing token delegation systems](https://a16z.com/2021/08/26/open-sourcing-our-token-delegate-program){target=\_blank}.

Another is the frequency of votes. Too many votes in a period could wear out existing engaged users. Too frequent will make them passive. Having a consistent cadence of votes allows for predictability and the creation of habits.

Another issue can be around voting in general. What is fairness in voting? How can one allocate resources optimally? Voting can go beyond just one entity, one vote. What about minority votes? Here is where we get into game theory, systems design and political theory, which are outside the scope of this write-up. However, there are some rabbit holes to go into and explore. Web3 has something for everyone 😁.

[Vitalik Buterin](https://vitalik.ca/){target=\_blank} wrote a great piece on [quadratic voting](https://vitalik.ca/general/2019/12/07/quadratic.html){target=\_blank}, [coin voting governance](https://vitalik.ca/general/2021/08/16/voting3.html){target=\_blank}, and [blockchain voting](https://vitalik.ca/general/2021/05/25/voting2.html){target=\_blank}. A great twitter follow related to governance and funding of public goods are the awesome folks at [Gitcoin](https://twitter.com/gitcoin){target=\_blank}, especially [Kevin Owocki](https://twitter.com/owocki?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor){target=\_blank}. Check out [his website](https://owocki.com/){target=\_blank}.

#### Implementation

Once an improvement proposal is passed, it's placed on the roadmap. Having a clear roadmap helps with communication and expectations. A community builds social capital with itself if it's able to make a promise, aka pass a proposal, and deliver on it. Roadmaps don't have to have exact time dates, but having a clear hierarchy of what is important and a rough time estimate is essential.

Implementation can be done by the core team/organizers or by community members. Typically the more decentralized the work, the more coordination is needed. However, if done right, things can move fast. Aiming for [good communication with clear roles and responsibilities between teams helps to reduce burnout and increases engagement](https://blog.synthetix.io/an-old-dictator-appears/){target=\_blank}.

Be warned that community organizing can be time-intensive and involve work. However, having clear incentives, good treasury management skills, and memes can help members step up to the plate and help while fostering community.

### Treasury Management

Treasury management is part of community management. How we manage the treasury affects the sustainability of the DAO. A practical example can be in the [diversification of funds](https://forum.sushi.com/t/treasury-portfolio-a-suggestion-for-diversification/2828){target=\_blank}. If a DAO holds [a large percentage of their own tokens, it creates risk](https://newsletter.banklesshq.com/p/how-daos-should-approach-treasury){target=\_blank}. The value of the token could drop, affecting the ability to fund operations. It could also affect the incentive structure to keep members. Because of this, projects like [SushiSwap have tried to diversify their assets into stablecoins](https://thedefiant.io/sushiswap-treasury-sale-proposal-draws-community-ire/){target=\_blank}. Another method is to take a cut of economic activity happening in the network to fund operations like [SushiSwap's Kanpai](https://forum.sushi.com/t/kanpai-bear-market-protection-with-treasury-revenue/4310){target=\_blank}.

Another practical method of treasury management is the inflation rate of the token. Inflation rates via yield farming can be a great tool to get new members. For utility tokens, they help move capital from passive holders to active contributors who create value. However, if used incorrectly, inflation rewards can spin out of control and follow a predictable [ponzinomics](https://www.youtube.com/watch?v=dH5mostDrv4){target=\_blank} of [inflation and collapse](https://youtu.be/piohteKgMXc?t=2962){target=\_blank}.

At the end of the day, no amount of clever financial engineering can substitute for authentic community engagement and the value they provide.

## And more

There is so much more that can be covered; however, the best way to learn is to join a DAO and start your own! Have fun and experiment!

There is still more to learn about raising funds and such. However, let's call it a day and revisit this in Part 2 sometime.

### Learn more

[DAO Virtual Summit](https://youtu.be/5xQLiVbz3EM){target=\_blank}
[DAO research papers](https://mobile.twitter.com/officer_cia/status/1421239988574949376){target=\_blank}
[Fair Launch Summit](https://fairlaunchsummit.wtf/){target=\_blank}
[DAOTalk.org](https://daotalk.org/){target=\_blank}

🎉 🥳 You made it this far! You get an Easter Egg 🥚.

Bonus! After the bootcamp check out some cool videos around [a16z’s Crypto School](https://a16z.com/crypto-startup-school/){target=\_blank} and check out [ConsenSys Tachyon](https://mesh.xyz/tachyon/){target=\_blank}, our blockchain accelerator.
