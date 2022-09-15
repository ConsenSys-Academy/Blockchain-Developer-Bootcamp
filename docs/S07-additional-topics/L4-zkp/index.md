# Zero-Knowledge Proofs

In our section on scalability later in the course, we will discuss Zero-Knowledge Proof rollups, but we won't go into detail about *what* ZKPs are. In this section, we'll discuss the basics of ZKPs and compare two common implementations of ZKPs you'll see in blockchain.

Zero-Knowledge Proofs have been researched since the 1980s—the initial researchers of ZKPs [received the Turing Award,](https://amturing.acm.org/award_winners/goldwasser_8627889.cfm){target=_blank} the highest award in computer science, for their work. Their development stems from the field of computational complexity and, while most of the work of ZKPs is very technical, we'll try to provide a broad overview.

* * *

The goal of zero-knowledge proofs (ZKPs) is for a **verifier** to be able to convince themselves that a **prover** possesses knowledge of a secret parameter, called a **witness**, satisfying some relation, without revealing the witness to the verifier or anyone else. Zero-knowledge proofs are currently being researched as solutions to two main issues in public blockchains:

1.  Privacy: All essential information within a blockchain network must be public. ZKPs allow users to verify / prove certain elements of information (such as the answer to a crossword puzzle) while not revealing the information itself (to not give the answer to someone else). Certain tools, such as AZTEC, promise to use ZKPs to provide channels which shield the entire nature of certain transactions from the public blockchain while still using the public blockchain's security promises.

2.  Scalability: As blockchain networks grow, the amount of data they require to be maintained grows as well. ZKPs compress large amounts of data into compact, verifiable proofs, a characteristic scalability researchers hope to use to dramatically reduce the data required to maintain security on a public blockchain.[From ZCash:](https://z.cash/technology/zksnarks/){target=_blank}“Succinct” zero-knowledge proofs (SNARKs, STARKs) can be verified within a few milliseconds, with a proof length of only a few hundred bytes even for statements about programs that are very large.

* * *

A common way Zero-Knowledge Proofs are used in blockchain is as follows. A Verifier will take the piece of data to be verified and put it through a private process (ZK-SNARK or STARK, for example) which produces a program called a Proof Circuit. This Proof Circuit can then be posted openly (such as in a Smart Contract) as it reveals no meaningful information about the nature of the data it represents. A Prover can then use the Proof Circuit to irrefutably prove they know the piece of data by publicly "solving" the Proof Circuit, a process that also reveals nothing about the nature of the data.

The Ethereum Foundation described the impact of this privacy would have on a blockchain:

> Imagine, for example, an election or auction conducted on the blockchain via a smart contract such that the results can be verified by any observer of the blockchain, but the individual votes or bids are not revealed. Another possible scenario may involve selective disclosure where users would have the ability to prove they are in a certain city without disclosing their exact location. ([source](https://blog.ethereum.org/2017/01/19/update-integrating-zcash-ethereum/){target=_blank})

## ZKPs in Action

### zk-SNARKs

**S**uccinct **N**on-Interactive **AR**gument of **K**nowledge, or SNARKs, were first widely implemented on a blockchain by [ZCash,](https://en.wikipedia.org/wiki/Zcash){target=_blank} a fork of Bitcoin. Ethereum introduced SNARK capacity with the Byzantium fork by including [precompiled contracts](https://medium.com/coinmonks/ethereum-support-for-zk-snarks-1236c0dfd3b4){target=_blank} that allowed efficient SNARK verification on-chain. SNARKs are being discussed in terms of privacy (as in ZCash) and scalability (as in [SNARK roll-ups](https://medium.com/@trenton.v/transcript-scalable-blockchains-as-data-layers-vitalik-buterin-11aa18b37e07){target=_blank})

**Pros:**

*   Small, constant proof size
*   Constant-time verification costs ([source](https://eprint.iacr.org/2019/099.pdf){target=_blank})

**Cons:**

*   Trusted setup required (see [ZCash parameter generation ceremony](https://www.youtube.com/watch?v=D6dY-3x3teM){target=_blank})
*   Relies on Elliptic Curve Cryptography, which is not quantum-resistant

### zk-STARKs

**S**calable and **T**ransparent **AR**gument of **K**nowledge, or STARKs, share a similar fundamental ideas with SNARKs but differ in execution. Their development and advocacy is done chiefly by STARKware, a private company led by Eli Ben Sasson, with assistance from the Ethereum Foundation.  

**Pros:**

*   No trusted setup required
*   Faster proving time relative to SNARKs ([source](https://youtu.be/aEqhjpjoaEA){target=_blank})

**Cons:**

*   STARKs have a larger proof size than SNARKs
*   As of June 2019, STARKs still in development


## ZKP Tutorials

* ["Hello World" of zk-SNARKS with Zokrates](https://zokrates.github.io/gettingstarted.html){target=_blank}
* [Creating a zk-SNARKS version of "Mastermind" in the Browser — Koh Wei Jie](https://medium.com/@weijiek/how-i-learned-zk-snarks-from-scratch-177a01c5514e){target=_blank}
* [GitHub Repo for Creating a zk-SNARKS version of "Mastermind" in the Browser](https://github.com/weijiekoh/zkmm){target=_blank}
* [Developing Confidential Tokens on AZTEC(requires access to Rinkeby Testnet)](https://medium.com/@PaulRBerg/how-to-code-your-own-confidential-token-on-ethereum-4a8c045c8651){target=_blank}
* [Docs: Cairo — a Turing-complete STARK generation](https://www.cairo-lang.org/) Cairo, Starkware's ZKP language, has a great doc repository here, including a great introductory tutorial.
* Reddit Scaling Bake-Off ZKP Submissions: [STARKWare](https://www.reddit.com/r/ethereum/comments/i01sjk/starkwares_submission_to_reddits_scaling_bakeoff/){target=_blank}, [Fuel Labs](https://www.reddit.com/r/ethereum/comments/i1cimc/the_great_reddit_scaling_bakeoff_submission_by/){target=_blank}, [AZTEC](https://www.reddit.com/r/ethereum/comments/i1j6ck/the_reddit_bakeoff_zkreddit_by_aztec/){target=_blank}

## More Resources

* [Article: NYTimes 1987 article discussing the discovery of ZK Proofs](https://www.nytimes.com/1987/02/17/science/a-new-approach-to-protecting-secrets-is-discovered.html){target=_blank}
* [Article: Why and How zk-SNARK Works](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160){target=_blank}
* [Article: Introduction to zk-SNARKS with Examples](https://media.consensys.net/introduction-to-zksnarks-with-examples-3283b554fc3b){target=_blank}
* [Wiki: Zero Knowledge Starter Pack (S[NT]ARK focused)](https://ethresear.ch/t/zero-knowledge-proofs-starter-pack){target=_blank}
* [Wiki: Zero Knowledge Proof Science Resources](https://zkp.science/){target=_blank}
* [Article: Not-so-gentle Introduction to the PCP Theorem](https://web.archive.org/web/20190422154614/https://pegasys.tech/a-not-so-gentle-introduction-to-the-pcp-theorem-part-1/){target=_blank} (PCP Theorem underpins many ZKPs)
* [Series: The Math behind STARKs](https://medium.com/starkware/stark-math-the-journey-begins-51bd2b063c71){target=_blank} (abstract but still technical)
* [Article: An Approximate Introduction to how zk-SNARKs are possible](https://vitalik.ca/general/2021/01/26/snarks.html){target=_blank}
* [Video: Vitalik Buterin: Scalable Blockchains as Data Layers](https://youtu.be/mOm47gBMfg8){target=_blank}
